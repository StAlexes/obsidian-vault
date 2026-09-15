### Шаг 1. Устанавливаем нужные библиотеки

Чтобы Python умел читать HTML и переводить его в Markdown, нам нужны две библиотеки: `beautifulsoup4` (разбор HTML) и `markdownify` (конвертер в Markdown).

1. В VS Code открой терминал снизу (если закрыт: меню **Terminal** → **New Terminal** или `Ctrl +` `).
    
2. Вставь команду и нажми **Enter**:
    
    ```Bash
    pip install beautifulsoup4 markdownify
    ```
    
    _Появится полоса загрузки и надпись `Successfully installed...`._
    

### Шаг 2. Размещаем файлы

Самый удобный способ организовать файлы в твоей рабочей папке (которая открыта в VS Code):


```
📁 ТВОЯ_ПАПКА_ПРОЕКТА/
│
├── 📁 extracted_docs/    <-- сюда скопируй распакованные файлы из CHM (.htm, картинки и т.д.)
├── convert.py           <-- наш скрипт (создадим сейчас)
└── main.py              <-- твой прошлый файл с тестом
```

### Шаг 3. Создаем скрипт `convert.py`

1. В проводнике VS Code слева нажми **New File** и назови его `convert.py`.
    
2. Вставь в него следующий код:

```python
import os
import re
import shutil
import urllib.parse
from pathlib import Path
from bs4 import BeautifulSoup
from markdownify import MarkdownConverter

# 1. Пути к данным
INPUT_DIR = Path("./extracted_docs").resolve()
OUTPUT_DIR = Path("./markdown_docs").resolve()
ASSETS_DIR = OUTPUT_DIR / "_assets"

OUTPUT_DIR.mkdir(parents=True, exist_ok=True)
ASSETS_DIR.mkdir(parents=True, exist_ok=True)


def is_icon(src_value: str) -> bool:
    """Проверяет, относится ли картинка к интерфейсным иконкам."""
    src_lower = src_value.lower()
    return (
        "icons/" in src_lower
        or "/icon" in src_lower
        or src_lower.startswith("icon")
        or src_lower.endswith(".ico")
    )


def clean_and_prepare_html(soup: BeautifulSoup, html_file_path: Path, assets_dir: Path):
    """Глубокая нормализация структуры DOM HTML."""
    # 1. Удаляем невидимый мусор
    for tag in soup(["script", "style", "meta", "link", "noscript"]):
        tag.decompose()

    # 2. Вычищаем все кнопки копирования, плашки C# и Unicode-символы буфера
    copy_pattern = re.compile(r"(?:^\s*(?:копировать|copy|c#)\s*$|[\u25a0-\u25ff\u29c9\u274f\u2398])", re.IGNORECASE)
    for el in list(soup.find_all(string=copy_pattern)):
        parent = el.parent
        if parent and parent.name in ["button", "span", "a", "div", "p", "td"] and len(parent.get_text(strip=True)) <= 15:
            parent.decompose()

    # 3. Нормализация ссылок методов в inline-code
    for a in list(soup.find_all("a")):
        href = a.get("href", "")
        text = a.get_text(strip=True)
        if re.search(r"\.html?", href, re.IGNORECASE):
            if "(" in text or "." in text:
                code_tag = soup.new_tag("code")
                code_tag.string = text
                a.replace_with(code_tag)
            else:
                a.replace_with(text)

    # 4. РАСПАКОВКА ТАБЛИЦ С КОДОМ (главная причина слипаний и значков справа)
    # Если внутри таблицы есть <pre> или явный C#-код, извлекаем код наружу и удаляем таблицу-обертку
    for table in list(soup.find_all("table")):
        text_table = table.get_text()

        # Проверяем, таблица ли это с цитатой ("Внимание" / "Примечание")
        if "Внимание" in text_table or "Примечание" in text_table:
            cells = [td.get_text(strip=True) for td in table.find_all(["td", "th"]) if td.get_text(strip=True)]
            if cells:
                bquote = soup.new_tag("blockquote")
                bquote.string = " ".join(cells)
                table.replace_with(bquote)
                continue

        # Если таблица содержит блок кода <pre>
        pres = table.find_all("pre")
        if pres:
            # Извлекаем все блоки кода из ячеек таблицы и ставим их вместо самой таблицы
            replacement_div = soup.new_tag("div")
            for p in pres:
                replacement_div.append(p)
            table.replace_with(replacement_div)
            continue

        # Если кода <pre> нет, но ячейка содержит строки кода (ТекущийОбъект..., НайтиОбъект...)
        if any(marker in text_table for marker in ["ТекущийОбъект.", "Объект.", "НайтиОбъект(", "ИзменитьСтадию"]):
            lines = [l.strip() for l in text_table.strip().splitlines() if l.strip()]
            if lines and any(";" in l or "=" in l for l in lines):
                pre_tag = soup.new_tag("pre")
                pre_tag.string = "\n".join(lines)
                table.replace_with(pre_tag)
                continue

        # Удаляем пустые оформительские таблицы
        cells = table.find_all(["td", "th"])
        if len(cells) <= 2 and len(text_table.strip()) < 80:
            table.decompose()

    # 5. Обработка картинок и перемещение в _assets
    for img in list(soup.find_all("img")):
        src_raw = img.get("src", "").strip()
        if not src_raw:
            img.decompose()
            continue

        src_decoded = urllib.parse.unquote(src_raw)
        if is_icon(src_decoded):
            img.decompose()
            continue

        image_disk_path = (html_file_path.parent / src_decoded).resolve()
        if not image_disk_path.is_file():
            filename_only = Path(src_decoded).name
            matched = list(INPUT_DIR.glob(f"**/{filename_only}"))
            if matched:
                image_disk_path = matched[0]

        if image_disk_path.is_file():
            target_image_name = image_disk_path.name
            target_path = assets_dir / target_image_name
            if not target_path.exists():
                try:
                    shutil.copy2(image_disk_path, target_path)
                except Exception as e:
                    print(f"⚠️ Ошибка копирования {image_disk_path.name}: {e}")

            relative_html_dir = html_file_path.parent.relative_to(INPUT_DIR)
            output_current_dir = OUTPUT_DIR / relative_html_dir
            rel_path_to_assets = os.path.relpath(assets_dir, output_current_dir).replace("\\", "/")

            img["src"] = f"{rel_path_to_assets}/{target_image_name}"
            if not img.get("alt"):
                img["alt"] = img.get("title", "Иллюстрация")
        else:
            img["src"] = f"_assets/{Path(src_decoded).name}"
            if not img.get("alt"):
                img["alt"] = "Изображение"


class CustomConverter(MarkdownConverter):
    """Генерирует строго оформленные блоки ```csharp с отступами."""
    def convert_pre(self, el, text, convert_as_inline=False, parent_tags=None):
        code_text = el.get_text()
        # Вычищаем случайные слова csharp из самого исходного текста кода
        lines = [line.rstrip() for line in code_text.splitlines()]
        clean_lines = []
        for line in lines:
            if line.strip().lower() in ["c#", "csharp", "копировать"]:
                continue
            clean_lines.append(line)

        final_code = "\n".join(clean_lines).strip()
        if not final_code:
            return ""

        # Гарантируем чистый открывающий и закрывающий тег Markdown
        return f"\n\n```csharp\n{final_code}\n```\n\n"


def clean_markdown_text(text: str) -> str:
    """Удаление мусора разметки, колонтитулов и жесткое разведение блоков."""
    # 1. Колонтитулы
    text = re.sub(r"Руководство по T-FLEX DOCs.*?\n", "", text, flags=re.IGNORECASE)
    lines = []
    for line in text.splitlines():
        lower = line.lower()
        if "авторское право" in lower or "топ системы" in lower or "все права защищены" in lower:
            continue
        lines.append(line)
    text = "\n".join(lines)

    # 2. Удаление висячих значков копирования и меток C#
    text = re.sub(r"[\u25a0-\u25ff\u29c9\u274f\u2398]", "", text)
    text = re.sub(r"^\s*C#\s*$", "", text, flags=re.MULTILINE | re.IGNORECASE)

    # 3. Исправление деформированных тегов ```
    # Убирает паразитный пустой блок ``` перед ```csharp
    text = re.sub(r"```\s*\n+(?=```csharp)", "", text)
    # Убирает случайный мусор типа ```csharp\ncsharp\n
    text = re.sub(r"(```csharp\s*\n)\s*csharp\s*\n", r"\1", text, flags=re.IGNORECASE)

    # 4. ГАРАНТИРОВАННОЕ РАЗВЕДЕНИЕ БЛОКОВ И МЕТОДОВ:
    # Обязательно две пустые строки после закрывающего блока ``` перед любым текстом
    text = re.sub(r"(```)\n+(?=[^\s\n#])", r"\1\n\n", text)

    # Обязательно пустая строка перед блоком метода `Имя(...)`, если он прилип к предыдущей строке
    text = re.sub(r"([^\n])\n(`[A-Za-zА-Яа-я_][\w\.]*\s*\([^\)\n]*\)`\s*\n\s*[-–—])", r"\1\n\n\2", text)

    # 5. Сворачивание лишних пустых строк (не больше 2 подряд)
    text_lines = [line.rstrip() for line in text.splitlines()]
    cleaned = "\n".join(text_lines)
    while "\n\n\n" in cleaned:
        cleaned = cleaned.replace("\n\n\n", "\n\n")

    return cleaned.strip()


def convert_file(file_path: Path) -> bool:
    content = ""
    for encoding in ["utf-8", "cp1251", "windows-1252"]:
        try:
            content = file_path.read_text(encoding=encoding)
            break
        except (UnicodeDecodeError, LookupError):
            continue

    if not content:
        return False

    soup = BeautifulSoup(content, "html.parser")
    clean_and_prepare_html(soup, file_path, ASSETS_DIR)

    content_root = soup.body if soup.body else soup

    raw_md = CustomConverter(
        heading_style="ATX",
        bullets="-",
        strip=["span", "font", "div", "button"]
    ).convert(str(content_root))

    final_md = clean_markdown_text(raw_md)

    relative_path = file_path.relative_to(INPUT_DIR)
    output_file_path = (OUTPUT_DIR / relative_path).with_suffix(".md")
    output_file_path.parent.mkdir(parents=True, exist_ok=True)

    output_file_path.write_text(final_md, encoding="utf-8")
    return True


def scan_and_collect_all_media():
    """Сбор всех контентных изображений в папку _assets."""
    image_extensions = {".png", ".jpg", ".jpeg", ".gif", ".bmp", ".svg"}
    copied = 0
    for item in INPUT_DIR.glob("**/*"):
        if item.is_file() and item.suffix.lower() in image_extensions:
            if is_icon(str(item)):
                continue
            dest = ASSETS_DIR / item.name
            if not dest.exists():
                shutil.copy2(item, dest)
                copied += 1
    return copied


def main():
    if not INPUT_DIR.exists():
        print(f"❌ Папка '{INPUT_DIR}' не найдена!")
        return

    pre_copied = scan_and_collect_all_media()
    print(f"📦 Скопировано картинок в _assets: {pre_copied}")

    html_files = list(INPUT_DIR.glob("**/*.htm")) + list(INPUT_DIR.glob("**/*.html"))
    print(f"🔍 Найдено HTML-файлов: {len(html_files)}")

    converted_count = 0
    for file_path in html_files:
        if convert_file(file_path):
            converted_count += 1

    total_assets = len(list(ASSETS_DIR.glob("*")))
    print(f"\n🎉 Обработка завершена!")
    print(f"📄 Готово страниц: {converted_count}")
    print(f"🖼️ Изображений в _assets: {total_assets}")
    print(f"📁 Результат сохранен в: {OUTPUT_DIR}")


if __name__ == "__main__":
    main()
```