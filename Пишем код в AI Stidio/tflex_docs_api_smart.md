# Справочник API T-FLEX DOCs (Smart Edition)
> Приоритет: используй стандартные методы C# на английском языке. Пометки [RU alias] показывают русскоязычные аналоги, а [has Async] — наличие асинхронной версии метода.

## TFlex.DOCs.Model.dll

### `AbstractMarkReferenceObject`
**Свойства:** Name: StringParameter, Mark: StringParameter, NTDType: Int32Parameter, NTDCode: StringParameter, Code: StringParameter, Description: StringParameter, IsCoating: BooleanParameter, OKPCode: StringParameter, Density: DoubleParameter, HeatConductivity: DoubleParameter, HeatCapacity: DoubleParameter, HeatExpansionLinear: DoubleParameter, HeatExpansionVolume: DoubleParameter, ElectroConductivity: DoubleParameter, KickViscosity: DoubleParameter, HB: DoubleParameter, HR: DoubleParameter, HV: DoubleParameter, SpinSoundness: DoubleParameter, BreakSoundness: DoubleParameter, DielectricSoundness: DoubleParameter

### `AccessAccessor`
**Свойства:** IsInherit: Boolean [RU: Унаследован]
**Методы:**
- `Void SetForAllUsers(String accessName, AccessDirectionObj accessDirection)` [RU: НазначитьВсемПользователям]
- `Void Set(RefObj user, String accessName, AccessDirectionObj accessDirection) (+1)` [RU: Назначить]
- `Void Delete(RefObj user, String accessName) (+1)` [RU: НазначитьВсемПользователям]
- `Void DeleteAll()` [RU: УдалитьВсе]
- `Void Удалить(Объект пользователь, String доступ)` [RU alternative]

### `AccessCommand`
**Свойства:** Id: Int32, Name: String, Type: AccessType

### `AccessDirectionAccessor`
**Свойства:** Default: AccessDirectionObj, Children: AccessDirectionObj, Entity: AccessDirectionObj, ПоУмолчанию: НаправлениеДоступа [RU only], ДочерниеОбъекты: НаправлениеДоступа [RU only], Объект: НаправлениеДоступа [RU only]
**Методы:**
- `Object GetRealValue()`

### `AccessGroup`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, Name: String, Type: AccessType, IsTemporary: Boolean, IsModified: Boolean, CanEdit: Boolean, CanDelete: Boolean, Changing: Boolean
**Методы:**
- `Void SetIsModifiedOn()`
- `Boolean SetCommandState(AccessCommand command, AccessCommandState state)`
- `Boolean IsAllowed(AccessCommand command)`
- `Boolean IsForbidden(AccessCommand command)`
- `AccessCommandState GetCommandState(AccessCommand command)`
- `Void BeginChanges()`
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges()`
- `Void Delete()`
- `IEnumerator`1 GetEnumerator()`
- `List`1 GetGroups(ServerConnection connection)` [has Async]
- `AccessGroup Find(ServerConnection connection, Int32 id) (+2)`

### `AccessGroupCommand`
**Свойства:** Command: AccessCommand, State: AccessCommandState

### `AccessInfo`
**Свойства:** Editable: Boolean, Owner: UserReferenceObject, Access: AccessGroup, Link: ParameterGroup, StageID: Int32, IsAdded: Boolean, IsModified: Boolean, InheritedFrom: AccessInheritedFrom, AccessDirection: AccessDirection, StartDate: Nullable`1, EndDate: Nullable`1, xAccessObjectID: Int32, xReferenceID: Int32, CommandType: AccessCommandType, AccessTypeID: AccessTypeID, AutoGeneratePK: Boolean, PrimaryKey: Int32
**Методы:**
- `Void Clear()`
- `Void Assign(Object source)`
- `Void ResetAccessGroupKey()`
- `Boolean CanBeEditable(AccessTypeID editorTypeID, Boolean isInherited, Boolean isStageEditor)`
- `Boolean MustResetPrimaryKey(AccessTypeID editorTypeID, Boolean inherited, Boolean isStageEditor)`

### `AccessManager`
**Свойства:** Object: ReferenceObject, ParentAccessObject: ReferenceObject, ObjectId: Int32, HasParentAccessObject: Boolean, InheritAccess: AccessManager
**Методы:**
- `AccessInfo MakeInheritedFrom(AccessInfo access, AccessTypeID editorTypeID, AccessInheritedFrom from, Boolean inherited)`
- `Void SetInherit(Boolean inherit, Boolean copyInheritAccess)`
- `AccessManager GetSystemAccess(ServerConnection connection)` [has Async]
- `AccessManager GetReferenceAccess(ReferenceInfo reference)` [has Async]
- `AccessManager GetReferenceObjectAccess(ReferenceObject referenceObject, AccessRightsLoadOptions options) (+1)` [has Async]
- `AccessManager GetAllReferenceAccesses(ReferenceInfo reference)` [has Async]
- `AccessManager GetStageAccess(Stage stage)` [has Async]

### `AccessManagerBase`
**Свойства:** AccessTypeID: AccessTypeID, CommandType: AccessCommandType, AllowDuplicates: Boolean, Connection: ServerConnection, Reference: ReferenceInfo, Stage: Stage, ReferenceId: Int32, StageId: Int32, IsModified: Boolean, IsInherit: Boolean
**Методы:**
- `Void ReplacePrimaryKey(Int32 oldKey, Int32 newKey, Boolean replaceInList)`
- `Void SetInherit(Boolean inherit, Boolean copyInheritAccess)`
- `Boolean ExistsAccessInfo(List`1 accesses, Nullable`1 primaryKey, UserReferenceObject owner, AccessGroup group, ParameterGroup link, Nullable`1 commandType, Nullable`1 accessTypeID, Nullable`1 accessDirection, Nullable`1 stageID)`
- `AccessInfo FindAccessInfo(List`1 accesses, Nullable`1 primaryKey, UserReferenceObject owner, AccessGroup group, ParameterGroup link, Nullable`1 commandType, Nullable`1 accessTypeID, Nullable`1 accessDirection, Nullable`1 stageID, Int32 currentObjectId)`
- `List`1 FindAllAccessInfo(List`1 accesses, UserReferenceObject owner, AccessGroup group, ParameterGroup link, Nullable`1 commandType, Nullable`1 accessTypeID, Nullable`1 accessDirection, Nullable`1 stageID)`
- `Void SetAccess(Int32 primaryKey, UserReferenceObject owner, AccessGroup group, AccessGroup oldGroup, ParameterGroup link, AccessCommandType commandType, AccessTypeID accessTypeID, AccessDirection accessDirection, Nullable`1 oldAccessDirection, Nullable`1 startDate, Nullable`1 endDate) (+1)`
- `Void RemoveAccess(Nullable`1 primaryKey, UserReferenceObject owner, AccessGroup group, AccessType type, ParameterGroup link, Nullable`1 accessDirection) (+1)`
- `Boolean Save()` [has Async]
- `IEnumerator`1 GetEnumerator()`

### `AccessManagerExtensions`
**Методы:**
- `Void Set(AccessManager manager, UserReferenceObject user, AccessGroup accessGroup, AccessDirection accessDirection)`
- `Void Clear(AccessManager manager, AccessType type)`

### `AccessorCreator`
**Методы:**
- `ObjectAccessor CreateObject(ReferenceObject referenceObject, MacroContext context)`

### `AccessorDefaultType`
**Свойства:** Name: String, TypeClass: Type, SubClass: Type, RealClass: Type, DefaultType: DefaultSupportedType, EnumerableDefaultType: DefaultSupportedType, IconName: String, Image: Object, Reference: Guid, Classes: Guid[], CastFunc: Func`3, CastObjectFunc: Func`2
**Методы:**
- `List`1 GetTypeClasses(IEnumerable`1 types)`
- `String GetDefaultTypeName(IEnumerable`1 types, DefaultSupportedType defaultType)`
- `Type GetDefaultTypeClass(IEnumerable`1 types, DefaultSupportedType defaultType)`
- `Type GetDefaultSubClass(IEnumerable`1 types, DefaultSupportedType defaultType, Boolean strongType)`
- `DefaultSupportedType GetDefaultSupportedType(IEnumerable`1 types, Type type)`
- `Type GetRealType(IEnumerable`1 types, DefaultSupportedType defaultType) (+1)`
- `Type GetTypeByRealType(IEnumerable`1 types, Type realType)`
- `AccessorDefaultType GetAccessorType(IEnumerable`1 types, DefaultSupportedType defaultType) (+1)`
- `AccessorDefaultType GetAccessorTypeByRealType(IEnumerable`1 types, Type realType)`
- `AccessorDefaultType GetEnumerableAccessorType(IEnumerable`1 types, Type type)`
- `Object Convert(Object value)`

### `AccessorManager`
**Свойства:** Culture: Language, AccessorTypes: ReadOnlyCollection`1, AvailableAccessorTypes: ReadOnlyCollection`1, DefaultSupportedMacroTypes: List`1
**Методы:**
- `Tuple`2 CreateTypeDescription(Func`2 func) (+1)`
- `Void RegisterTypes(IEnumerable`1 accessorTypes)`
- `String GetDefaultTypeName(DefaultSupportedType defaultType)`
- `Type GetDefaultTypeClass(DefaultSupportedType defaultType, Language macrolanguage) (+1)`
- `Type GetDefaultSubClass(DefaultSupportedType defaultType, Boolean strongType)`
- `DefaultSupportedType GetDefaultSupportedType(Type type)`
- `Type GetRealType(DefaultSupportedType defaultType) (+1)`
- `Type GetTypeByRealType(Type realType)`
- `AccessorDefaultType GetEnumerableAccessorType(Type type)`
- `AccessorDefaultType GetAvailableAccessorType(Type type)`
- `AccessorDefaultType GetAccessorType(Type type) (+1)`
- `Type GetValueListType()`
- `List`1 GetObjects(Object desktopObject)`
- `List`1 GetHierarhyLinks(Object desktopObject)`
- `Boolean IsAccessorType(Type type)`
- `Object TryCast(Object value, Type toType)`
- `Object GetRealValue(Object value)`

### `AccessRights`
**Свойства:** ReferenceId: Int32, ObjectId: Int32, Type: AccessType, IsInherit: Boolean
**Методы:**
- `Int32 GetAccessRightPk(Int32 accessGroupId)`
- `Boolean IsAllowed(AccessCommand command, ParameterGroup link)`
- `AccessCommandState GetCommandState(AccessCommand command, ParameterGroup link)`
- `IEnumerable`1 GetAccessGroups()`
- `Boolean IsSpecialInstanceCommand(ParameterGroup group, AccessCommand command)`
- `AccessRights GetSystemAccess(ServerConnection connection)`
- `AccessRights GetReferenceAccess(ReferenceInfo reference)`
- `AccessRights GetReferenceObjectAccess(ReferenceInfo reference) (+2)`
- `IReadOnlyList`1 GetReferencesHasExplicitAccessesForUser(UserReferenceObject userObject)`
- `IReadOnlyList`1 GetReferencesStructureAccess(UserReferenceObject userObject, IEnumerable`1 references)`
- `IReadOnlyList`1 GetReferencesObjectsAccess(UserReferenceObject userObject, IEnumerable`1 references)`
- `IReadOnlyList`1 GetReferencesObjectsOwnerAccess(ServerConnection connection, IEnumerable`1 references)`
- `IReadOnlyList`1 FindExplicitlyAccessedObjects(UserReferenceObject userObject, ReferenceInfo reference)`
- `IReadOnlyList`1 FindObjectsWithOwnerAccess(UserReferenceObject userObject, ReferenceInfo reference)`
- `IReadOnlyList`1 LoadReferenceObjectsAccesses(UserReferenceObject userObject, ReferenceInfo reference, IEnumerable`1 objectsIds)`
- `Boolean IsCommandAllowed(AccessCommand command, ReferenceObject referenceObject, ParameterGroup link) (+7)` [has Async]
- `Boolean IsReferenceCommandsAllowed(ReferenceInfo referenceInfo, ServerConnection connection, AccessCommand[] commands)`
- `Boolean HasAdminAccess(ServerConnection connection, User user)` [has Async]

### `AccessType`
**Свойства:** AccessTypeID: AccessTypeID, Type: AccessCommandType, Id: Int32, IsSystem: Boolean, IsReference: Boolean, IsObject: Boolean, IsLink: Boolean, IsStage: Boolean, Name: String, Commands: ReadOnlyCollection`1, Item: AccessCommand, Reference: ReferenceAccessType, Object: ObjectAccessType, Stage: StageAccessType, Link: LinkAccessType, System: SystemAccessType
**Методы:**
- `List`1 GetTypes()`
- `List`1 GetGroups(ServerConnection connection)` [has Async]

### `Account`
**Свойства:** IsLoggedIn: Boolean, IsClientViewAccount: Boolean, OwnerId: Int32, Owner: User, Connection: ServerConnection, Guid: Guid, Folders: MailFolderCollection, Inbox: MailFolder, SentItems: MailFolder, Drafts: MailFolder, DeletedItems: MailFolder, Rules: IEnumerable`1, Name: String, MessagesAccess: MailMessagesAccess, CanSaveMessagesOnServer: Boolean
**Методы:**
- `Void ReloadFolders()` [has Async]
- `Void ReloadRules()`
- `Boolean IsSystemFolder(MailItemFolder folder)`
- `Void SendMessage(MailMessage message)`
- `Boolean SetMessageUnread(MailMessage message)`
- `Boolean SetMessageRead(MailMessage message)`
- `Boolean SetMessagesUnread(IEnumerable`1 messages)`
- `Boolean SetMessagesRead(IEnumerable`1 messages)`
- `Boolean SetFolderRead(MailItemFolder mailItemFolder)`
- `Boolean SetFolderUnread(MailItemFolder mailItemFolder)`
- `List`1 GetRootFolders()` [has Async]
- `Void AddRule(MailRule rule)`
- `Void RemoveRule(MailRule rule)`
- `Void MoveRuleUp(MailRule rule)`
- `Void MoveRuleDown(MailRule rule)`
- `Void SaveRules()`
- `Boolean SaveFolder(MailItemFolder folder)`
- `Boolean MoveMailFolderTo(MailFolder folder, MailFolder newParentFolder)`
- `Boolean DeleteFolder(MailItemFolder folder, Boolean useAccountSettings)`
- `Boolean MoveMessagesTo(MailFolder toFolder, IEnumerable`1 messages)`
- `Boolean DeleteMessages(IEnumerable`1 messages, Boolean useAccountSettings)`
- `MailMessage FindMessage(Int32 globalId, Int32 folderId)`

### `ActionReferenceObject`
**Свойства:** Class: ActionType, Name: StringParameter, IsAutomatic: Boolean, ChangingObj: NomenclatureReferenceObject, ActionDescription: StringParameter, ActionState: Int32Parameter
**Методы:**
- `DesktopOperationInfo GenerateDesktopOperationInfo(IEnumerable`1 items)`
- `NomenclatureObject GetChangingObject()`
- `Guid GetChangingObjectGuid()`
- `Guid GetChangingNodeGuid()`
- `Void SetApplyingState()`
- `Void SetAppliedState()`
- `Boolean Apply(Boolean& needCheckInNomenclatureObject)`

### `ActionsReference`
**Свойства:** Classes: ActionsTypes

### `ActionType`
**Свойства:** IsAssemblyAction: Boolean, IsDeleteAction: Boolean, IsAddAction: Boolean, IsEditAction: Boolean, IsEntrancesChangingAction: Boolean, IsReplaceAction: Boolean, IsVariantReplaceAction: Boolean, IsReplaceFileEditAction: Boolean, IsCancelEditAction: Boolean, Classes: ActionsTypes

### `ActiveDirectoryUsersGroup`
**Методы:**
- `Boolean CanCreateChildObject(ClassObject childClass)`
- `Boolean UpdateUsers(ICollection`1 updateList, CallbackSolutions callback)` [has Async]

### `ActivityContextExtensions`
**Методы:**
- `ReportMacroContext GetReportMacroContext(ActivityContext context)`
- `ReportMacroProvider GetReportMacroProvider(ActivityContext context)`

### `ActivityContextExtensions`
**Методы:**
- `MacroContext GetMacroContext(ActivityContext context)`
- `MacroProvider GetMacroProvider(ActivityContext context)`
- `FormulaMacro GetFormulaMacro(ActivityContext context)`
- `IFormulaMacroCreator GetFormulaCreator(ActivityContext context)`
- `ServerConnection GetConnection(ActivityContext context)`
- `Void Return(NativeActivityContext context, Object result)`
- `Object GetVariableValue(ActivityContext context, String variableName)`
- `Boolean TryVariableValue(ActivityContext context, String variableName, Object& value)`
- `Void SetVariableValue(ActivityContext context, String variableName, Object value)`
- `FlowchartMacroContext GetFlowchartMacroContext(ActivityContext context)`
- `T GetProvider(ActivityContext context, Func`1 createProviderAction)`

### `ActivityDataHelper`
**Методы:**
- `ParameterObjectValue GetParameterValue(ActivityContext context, InArgument`1 variable, InArgument`1 parameter, Boolean autoChanging, Boolean throwOnError)`
- `ParameterObjectValue[] GetParameterValues(ActivityContext context, InArgument`1 variable, InArgument`1 parameter, Boolean autoChanging, Boolean throwOnError)`
- `Object GetVariableValue(ActivityContext context, InArgument`1 variable, Boolean throwOnError)`
- `ObjectAccessor GetObjectAccessorValue(ActivityContext context, InArgument`1 variable, InArgument`1 reference, Boolean throwOnError) (+1)`
- `ObjectAccessor[] GetObjectAccessorValues(ActivityContext context, InArgument`1 variable, InArgument`1 reference, Boolean throwOnError) (+1)`
- `ReferenceObject GetReferenceObjectValue(ActivityContext context, InArgument`1 variable, InArgument`1 reference, Boolean throwOnError) (+1)`
- `ReferenceObject[] GetReferenceObjectValues(ActivityContext context, InArgument`1 variable, InArgument`1 reference, Boolean throwOnError) (+1)`
- `HierarchyLinkAccessor GetHierarchyLinkAccessorValue(ActivityContext context, InArgument`1 variable, Boolean throwOnError)`
- `ComplexHierarchyLink GetComplexHierarchyLinkValue(ActivityContext context, InArgument`1 variable, Boolean throwOnError)`
- `ComparisonOperator GetOperator(String value)`

### `ActivityManager`
**Методы:**
- `T Load(String code, Boolean ignoreDynamicRootActivity, Boolean tryConvertCode) (+1)`
- `String Serialize(Activity activity)`

### `ActivityMetadataExtensions`
**Методы:**
- `Void AddValidationWarning(ActivityMetadata metadata, String message) (+2)`
- `Void AddValidationArgumentWarning(ActivityMetadata metadata, String argument) (+2)`
- `Void AddValidationArgumentError(ActivityMetadata metadata, String argument) (+2)`
- `Void VerifyArgument(ActivityMetadata metadata, InArgument`1 argument, String name, Boolean isWarning) (+2)`
- `Void VerifyActivity(ActivityMetadata metadata, Activity activity, String name, Boolean isWarning) (+2)`
- `Void AddValidationMetadataArgumentError(ActivityMetadata metadata, String argument) (+2)`
- `Void AddValidationFunctionError(ActivityMetadata metadata) (+2)`
- `Void VerifyFunction(ActivityMetadata metadata, Activity activity) (+2)`
- `VariableInfo VerifyVariable(ActivityMetadata metadata, InArgument`1 argument, String variableCaption, Func`2 verifyTypeFunc, Boolean supportMultiple) (+2)`
- `VariableInfo VerifyAccessorVariable(ActivityMetadata metadata, InArgument`1 argument, DefaultSupportedType defaultType, String variableCaption, Boolean supportMultiple) (+5)`
- `Void SetReturnChildrenCollection(NativeActivityMetadata metadata, Collection`1 children)`

### `ActivitySettingsManager`
**Методы:**
- `Boolean AddNamespace(Activity activity, NamespaceInfo namespaceInfo)`
- `Void AddNamespaces(Activity activity, IEnumerable`1 namespaces)`

### `AddActionReferenceObject`
**Свойства:** Count: Int32Parameter, Comment: StringParameter

### `AdditionalReferenceObject`
**Свойства:** ReferenceObject: Guid, HierarchyLink: Guid

### `AddRangeToCollectionActivity`1`
**Свойства:** Values: InArgument`1, Items: InArgument`1, IsInsert: InArgument`1, Index: InArgument`1

### `AddressBookSettingReferenceObject`
**Свойства:** Class: AddressBookSettingType, Name: StringParameter, ReferenceParameter: GuidParameter, AddressParameter: StringParameter, NameParameter: StringParameter

### `AddressBookSettingsReference`
**Свойства:** Classes: AddressBookSettingsTypes

### `AddressBookSettingsTypes`
**Свойства:** AddressBookSettingReferenceObject: AddressBookSettingType

### `AddressBookSettingType`
**Свойства:** Classes: AddressBookSettingsTypes, IsAddressBookSettingReferenceObject: Boolean

### `AddToCollectionActivity`1`
**Свойства:** Values: InArgument`1, Item: InArgument`1, IsInsert: InArgument`1, Index: InArgument`1

### `AdminAccessChangedCallback`
**Методы:**
- `Void Invoke()`
- `IAsyncResult BeginInvoke(AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `AgregationParameterDataSettings`
**Свойства:** SourceParameter: SeriesParameter, OutputParameter: SeriesParameter, SummaryAggregationFunctionType: SummaryAggregationFunctionType, SummaryAggregationFormula: String

### `AliasedParameterInfoBuilder`
**Свойства:** IsVirtualParameterBuilder: Boolean
**Методы:**
- `Void FixParameterState()`
- `Void CopyFrom(ParameterInfo sourceParameter)`

### `AllChildObjectsPathItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `AllowedClassesSettings`
**Свойства:** Mode: AllowedClassesMode, Classes: List`1
**Методы:**
- `Void WriteXElement(XElement element)`
- `Void ReadXElement(XElement element)`

### `AllParentObjectsPathItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `AlphabeticRevisionLevelObject`
**Свойства:** EmptyValue: StringParameter, MinLength: Int32Parameter, RegexTemplate: String
**Методы:**
- `String GetNextValue(String previousValue)`
- `Int32 Compare(String x, String y)`
- `Boolean CanChangeParameter(Parameter p, Object newValue)`

### `AndAlsoOperator`
**Свойства:** LogicalType: LogicalActivityOperatorType
**Методы:**
- `Nullable`1 CompareFirst(Boolean firstOperand)`
- `Boolean CompareSecond(Boolean secondOperand)`

### `AnyReferenceLink`
**Свойства:** IsAnyReference: Boolean, IsModified: Boolean, IsLinkedReferenceInitialized: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, IsEmptyLinkedObjects: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32, Item: ReferenceObject
**Методы:**
- `Dictionary`2 GetLinkedObjectsId()` [has Async]
- `IEnumerable`1 GetLinkedObjects()` [has Async]
- `List`1 GetObjectsFromReference(Func`2 getReference, StaticReferenceLoadSettings loadSettings)` [has Async]
- `Boolean Load(Int32 count) (+1)` [has Async]
- `ReferenceObject AddLinkedObject(ReferenceObject linkedObject)` [has Async]
- `ReferenceObject AddLinkedObjectWithNoCopy(ReferenceObject linkedObject, Func`2 getReference)` [has Async]
- `Boolean RemoveLinkedObject(ReferenceObject linkedObject)` [has Async]
- `Boolean RemoveLinkedObjectWithNoCopy(ReferenceObject linkedObject, Func`2 getReference)` [has Async]
- `Void RemoveAll()` [has Async]
- `Void RemoveAllWithNoCopy(Func`2 getReference)` [has Async]
- `Reference GetOrAddLinkedReference(ReferenceInfo info)`
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `Int32 IndexOf(ReferenceObject item)`
- `Boolean Contains(ReferenceObject item)`
- `Void CopyTo(ReferenceObject[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`
- `List`1 FindMasterObjects(ParameterGroup anyReferenceLink, Reference masterReference, ReferenceObject slaveObject)`

### `AnyReferenceLinkManager`
**Свойства:** LinkGroups: ParameterGroupCollection

### `AnyReferenceLoadSettings`
**Методы:**
- `Boolean Add(ParameterInfo parameter)`

### `AnyValueListComboBoxEditData`
**Свойства:** ParameterPath: String
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `ApplicabilityColumnData`
**Свойства:** IsEmpty: Boolean, Type: ColumnDataType

### `ApplicabilityInterval`
**Свойства:** StartProductGuid: GuidParameter, EndProductGuid: GuidParameter

### `ApplicabilityPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `ApplicabilityRecordsCreator`
**Методы:**
- `Task`1 CreateDefaultBaseApplicabilityRecord(IntervalReferenceObject object, CancellationToken cancellationToken)`
- `Task`1 CreateApplicabilityRecord(IntervalReferenceObject applicabilityObject, NumberRange numberRange, CancellationToken cancellationToken)`

### `ApplicabilityRecordsReference`
**Свойства:** Classes: ApplicabilityRecordsTypes

### `ApplicabilityRecordsReferenceObject`
**Свойства:** Class: ApplicabilityRecordsType, LinkedObjectID: Int32Parameter, ReferenceID: Int32Parameter, ProjectID: Int32Parameter, ProductID: Int32Parameter, Modification: StringParameter, StartMilestoneOfRange: Int32Parameter, EndMilestoneOfRange: Int32Parameter, StartNumberOfRange: Int32Parameter, EndNumberOfRange: Int32Parameter, StartActionDate: DateTimeParameter, EndActionDate: DateTimeParameter, ApplicabilityAction: ApplicabilityActionType, StructureVariantID: Int32Parameter, ApplicabilityGroup: ApplicabilityGroupType, UseNumberRanges: BooleanParameter

### `ApplicabilityRecordsType`
**Свойства:** Classes: ApplicabilityRecordsTypes, IsApplicabilityRecordsType: Boolean

### `ApplicabilityRecordsTypes`
**Свойства:** ApplicabilityRecordsType: ApplicabilityRecordsType

### `Application`
**Свойства:** AssemblyPath: String, Type: ApplicationType, ReadOnly: Boolean, Guid: Guid, Name: String, Description: String

### `ApplicationRelationReference`
**Свойства:** Classes: ApplicationRelationTypes

### `ApplicationRelationReferenceObject`
**Свойства:** Class: ApplicationRelationType, Name: StringParameter, ApplicationParameter: StringParameter, DOCsParameterType: Int32Parameter, DOCsParameter: StringParameter, DOCsLink: StringParameter, DOCsParameterPath: StringParameter, ApplicationParameterType: StringParameter, TypeRelation: Int32Parameter

### `ApplicationRelationType`
**Свойства:** Classes: ApplicationRelationTypes, IsApplicationRelationType: Boolean

### `ApplicationRelationTypes`
**Свойства:** ApplicationRelationType: ApplicationRelationType

### `ApplicationsManager`
**Свойства:** Connection: ServerConnection, Applications: ICollection`1
**Методы:**
- `Application CreateNewApplication(ApplicationType type)`
- `Void DeleteApplication(Application application)`
- `Void SaveApplication(Application application)`
- `Void LoadApplications(Action`1 exceptionCallback, IEnumerable`1 applicationGuids) (+1)`
- `IEnumerable`1 GetStoredApplications()`
- `IEnumerable`1 GetLocalApplications()`
- `IEnumerable`1 GetSystemApplications()`
- `IEnumerable`1 GetSystemApplicationsModels()`
- `IEnumerable`1 GetSystemApplicationsUIs()`
- `IEnumerable`1 GetSystemApplicationsUIClient()`
- `IEnumerable`1 GetSystemApplicationsUniClient()`

### `ApplicationsRelationsProfileReference`
**Свойства:** Guid: Guid, CurrentProflie: ApplicationsRelationsProfileReferenceObject, Classes: ApplicationsRelationsProfileTypes

### `ApplicationsRelationsProfileReferenceObject`
**Свойства:** Class: ApplicationsRelationsProfileType, Name: StringParameter, AppCode: StringParameter, LocalFilePaths: StringParameter, LoadingFolderPaths: StringParameter, DisallowEditStructure: BooleanParameter, ReferenceForDataExchange: Guid, UseSimplifiedRepresentations: SimplifiedRepresentationState, ApplicationsRelations: ReferenceObjectCollection, TypeRelations: ReferenceObjectCollection, AssocParameters: ReferenceObjectCollection, EnvironmentSettingsFile: FileObject
**Методы:**
- `ReferenceObject AddApplicationRelation(Guid listObjectClass) (+1)`

### `ApplicationsRelationsProfileType`
**Свойства:** Classes: ApplicationsRelationsProfileTypes, IsApplicationsRelationsProfileType: Boolean

### `ApplicationsRelationsProfileTypes`
**Свойства:** ApplicationsRelationsProfileType: ApplicationsRelationsProfileType

### `ArgumentExtensions`
**Методы:**
- `T ToValue(InArgument`1 argument)`

### `AssemblyActionReferenceObject`
**Свойства:** IsAutomatic: Boolean, ChangingNode: NomenclatureReferenceObject
**Методы:**
- `Guid GetChangingNodeGuid()`
- `Void SetChangingNode(NomenclatureReferenceObject newObject)`
- `NomenclatureObject GetChangingObject()`

### `AssemblyLoader`
**Свойства:** Plugins: ReadOnlyCollection`1
**Методы:**
- `T GetClassObject()`

### `AssignmentChangeManager`1`
**Методы:**
- `Boolean CanChangeParameter(TAssignment assignment, Parameter parameter, Object newValue)`
- `Boolean CanChangeLink(TAssignment assignment, LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`

### `AssignmentDescriptionFormatTypeConverter`
**Методы:**
- `ConvertResponse Convert(AssignmentReferenceObject assignment, DescriptionFormatType to, Object context) (+1)`

### `AssignmentFolderReference`
**Свойства:** Classes: AssignmentFolderTypes
**Методы:**
- `ManualAssignmentFolderReferenceObject[] GetAllManualFolders()`
- `ManualAssignmentFolderReferenceObject CreateManualFolder(AssignmentFolderReferenceObject parent)`
- `SearchAssignmentFolderReferenceObject CreateSearchFolder(AssignmentFolderReferenceObject parent)`

### `AssignmentFolderReferenceObject`
**Свойства:** Class: AssignmentFolderType, Name: StringParameter, ViewName: StringParameter, IsPublic: BooleanParameter
**Методы:**
- `Boolean CanCreateManualFolder()`
- `Boolean CanCreateSearchFolder()`
- `Boolean CanDeleteFolder()`

### `AssignmentFolderType`
**Свойства:** Classes: AssignmentFolderTypes, IsAssignmentFolderReferenceObject: Boolean, IsSearchAssignmentFolderReferenceObject: Boolean, IsManualAssignmentFolderReferenceObject: Boolean

### `AssignmentFolderTypes`
**Свойства:** AssignmentFolderReferenceObject: AssignmentFolderType, SearchAssignmentFolderReferenceObject: AssignmentFolderType, ManualAssignmentFolderReferenceObject: AssignmentFolderType

### `AssignmentFormulaMacro`
**Свойства:** CodeOffset: Int32

### `AssignmentMacroProvider`
**Свойства:** Context: AssignmentMacroContext
**Методы:**
- `List`1 GetSubordinateIds()` [RU: ПолучитьИдентификаторыПодчинённых]

### `AssignmentReference`
**Свойства:** ProcessHelper: IAssignmentReferenceHelper, UsersAssistance: AssignmentUsersAssistance, Classes: AssignmentTypes
**Методы:**
- `List`1 GetAssociatedAssignments(Guid referenceObjectGuid, Boolean reload) (+1)`
- `Boolean OpenAssignmentsInMail(ServerConnection serverConnection)` [has Async]

### `AssignmentReferenceObject`
**Свойства:** StatusType: AssignmentStatus, DescriptionFormatType: DescriptionFormatType, AcceptType: AssignmentAcceptType, Percent: Double, AutoCalculation: Boolean, IsDraft: Boolean, IsCancelled: Boolean, InProgress: Boolean, Class: AssignmentType, Name: StringParameter, StartDate: DateTimeParameter, EndDate: DateTimeParameter, CheckDate: DateTimeParameter, Description: StringParameter, DescriptionTextFormat: Int32Parameter, Status: Int32Parameter, LaboriousnessPlan: SingleParameter, LaboriousnessFact: SingleParameter, AuxiliaryTime: SingleParameter, PercentComplete: PercentParameter, Importance: Int32Parameter, Number: StringParameter, Basic: BooleanParameter, Priority: ByteParameter, ErrorLog: StringParameter, ExtendedData: StringParameter, Comments: IEnumerable`1, StatusChangeComments: IEnumerable`1, Executor: User, StorageExecutor: User, Task: ReferenceObject, LinkedMaterials: AnyReferenceLink, StorageLinkedMaterials: ICollection`1, MailingList: ReferenceObjectCollection`1, Controller: User, OnBehalf: User, StorageOnBehalf: User, Files: ReferenceObjectCollection`1, Categories: ReferenceObjectCollection, DependentAssignments: ReferenceObjectCollection`1
**Методы:**
- `CommentReferenceObject AddComment(Guid listObjectClass) (+1)`
- `ReferenceObject AddLinkedMaterial(ReferenceObject newLinkedObject)`
- `ReferenceObject AddStorageLinkedMaterial(ReferenceObject newLinkedObject)`
- `Boolean RemoveLinkedMaterial(ReferenceObject linkedObject)`
- `Boolean RemoveStorageLinkedMaterial(ReferenceObject linkedObject)`
- `ReferenceObject Subscribe(User user) (+1)`
- `Boolean Unsubscribe(User user) (+1)`
- `ReferenceObject AddFile(ReferenceObject newLinkedObject)`
- `Boolean RemoveFile(ReferenceObject linkedObject)`
- `ReferenceObject AddCategory(ReferenceObject newLinkedObject)`
- `Boolean RemoveCategory(ReferenceObject linkedObject)`
- `ReferenceObject AddDependentAssignment(AssignmentReferenceObject newLinkedObject)`
- `Boolean RemoveDependentAssignment(ReferenceObject linkedObject)`
- `Boolean CheckCurrentUserIsAssignmentManager()`
- `Void ChangeAutoCalculation(Boolean autoCalculation)`
- `Boolean CanChangeAutoCalculation()`
- `Boolean CanChangePercent()`
- `Void ChangePercent(Double percent)`
- `Void RecalculateProgress()`
- `Boolean CanChangeParameter(Parameter p, Object newValue)`
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`
- `Boolean CanRemove()`
- `CommentReferenceObject CreateComment(String text, Boolean endChanges, String name, CommentType type) (+2)`
- `Boolean CanCreateComment()`
- `AssignmentReferenceObject GetParentAssignment()`
- `GroupAssignmentReferenceObject GetGroupAssignment()`
- `Void BuildBody(String text, String comments)`
- `Void Accept(AssignmentReferenceObject[] assignments) (+1)`
- `Boolean CanAccept()`
- `Boolean Complete(String comment, String description) (+1)`
- `Boolean CanComplete(Boolean statusReload) (+1)`
- `Void Reject(AssignmentReferenceObject[] assignments) (+1)`
- `Boolean CanReject()`
- `Void Close(AssignmentReferenceObject[] assignments) (+1)`
- `Boolean CanClose(Boolean statusReload) (+1)`
- `Void Suspend(AssignmentReferenceObject[] assignments) (+1)`
- `Boolean CanSuspend(Boolean statusReload) (+1)`
- `Void Resume(AssignmentReferenceObject[] assignments) (+1)`
- `Boolean CanResume(Boolean statusReload) (+1)`
- `Void Cancel(AssignmentReferenceObject[] assignments, CancellationActionOnDependentAssignments actionOnDependentAssignments, String comment) (+1)`
- `Boolean CanCancel(Boolean statusReload) (+1)`
- `Void Elaborate(AssignmentReferenceObject[] assignments, String comment)`
- `Boolean CanElaborate(Boolean statusReload) (+1)`
- `Boolean CanCreateLinkedAssignment()`
- `Void SetImportance(AssignmentReferenceObject[] assignments, AssignmentImportance importance)`
- `Boolean CanClone()`
- `AssignmentReferenceObject CreateClone(AssignmentType type, Boolean shouldSaved) (+1)`

### `AssignmentType`
**Свойства:** CanCreateObjects: Boolean, Classes: AssignmentTypes, IsAssignmentReferenceObject: Boolean, IsMemoReferenceObject: Boolean, IsAssignmentWithExecutorsList: Boolean, IsGroupAssignment: Boolean, IsProcessAssignment: Boolean, IsAgreementProcessAssignment: Boolean, IsWorkProcessAssignment: Boolean, IsExceptionProcessAssignment: Boolean, IsDurationExceptionProcessAssignment: Boolean, IsNoExecutorExceptionProcessAssignment: Boolean, IsNoSolutionExceptionProcessAssignment: Boolean, IsNativeExceptionProcessAssignment: Boolean, IsMacroProcessAssignment: Boolean, IsRunSubprocessProcessAssignment: Boolean, IsProjectAssignment: Boolean

### `AssignmentTypes`
**Свойства:** AssignmentReferenceObject: AssignmentType, MemoReferenceObject: AssignmentType, AssignmentWithExecutorsList: AssignmentType, GroupAssignment: AssignmentType, ProcessAssignment: AssignmentType, AgreementProcessAssignment: AssignmentType, WorkProcessAssignment: AssignmentType, ExceptionProcessAssignment: AssignmentType, DurationExceptionProcessAssignment: AssignmentType, NoExecutorExceptionProcessAssignment: AssignmentType, NoSolutionExceptionProcessAssignment: AssignmentType, NativeExceptionProcessAssignment: AssignmentType, MacroProcessAssignment: AssignmentType, RunSubprocessProcessAssignment: AssignmentType, ProjectAssignment: AssignmentType

### `AssignmentUsersAssistance`
**Свойства:** SubordinateIds: ReadOnlyCollection`1, UserIdsWhoseRightsInheritedByCredentials: ReadOnlyCollection`1
**Методы:**
- `Void Clear()`

### `AssignmentWithExecutorsListObject`
**Свойства:** PossibleExecutors: ReferenceObjectCollection
**Методы:**
- `ReferenceObject AddPossibleExecutor(ReferenceObject newLinkedObject)`
- `Boolean RemovePossibleExecutor(ReferenceObject linkedObject)`

### `AssignObjectPropertyActivityBase`
**Свойства:** Object: InArgument`1, Action: InArgument`1, Value: Activity`1

### `Attachment`
**Свойства:** Name: String, IsFile: Boolean, IsObject: Boolean, IsMessage: Boolean, IsTask: Boolean

### `AuthorInfo`
**Свойства:** Connection: ServerConnection, AuthorFullName: String, AuthorFirstName: String, AuthorLastName: String, AuthorPatronymic: String, AuthorShortName: String

### `AuthorPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `AuthToken`
**Свойства:** AccessToken: String, RefreshToken: String, RefreshTokenLifetime: Int64

### `AuthTokenExtensions`
**Методы:**
- `TimeSpan GetExpirationTime(AuthToken authToken)`

### `AvailableProductLicense`
**Свойства:** Module: ModuleLicense, TotalCount: Int32, AccessibleCount: Int32

### `BaseColumnData`
**Свойства:** Owner: StructureGroupSettings, Type: ColumnDataType, IsEmpty: Boolean
**Методы:**
- `BaseColumnData CreateEmpty(ColumnDataType type)`
- `Void SetInternalOwner(StructureGroupSettings owner)`

### `BaseConfiguration`
**Свойства:** Connection: ServerConnection, Guid: Guid, Name: String, Comment: String, Title: String, ConfiguratorGuid: Guid, Icon: IconImage, AccessUsersUseType: ItemListUseType, ReferencesUseType: ItemListUseType, CanEdit: Boolean, CanEditProperties: Boolean, CanDelete: Boolean, AsClientConfiguration: ClientConfiguration, AsWebConfiguration: WebConfiguration
**Методы:**
- `Image GetImage()`
- `Byte[] GetImageBytes()`
- `Void SetImage(Image image)`
- `List`1 GetAccessUsers()`
- `Void SetAccessUsers(IEnumerable`1 users)`
- `Boolean IsAccessibleFor(UserReferenceObject user)`
- `List`1 GetReferences()` [has Async]
- `Void SetReferences(IEnumerable`1 references)`
- `Boolean SupportsReference(ReferenceInfo reference) (+1)`
- `List`1 GetAvailableLicenses()`
- `Dictionary`2 GetLicenses()`
- `Void SetLicenses(Dictionary`2 data)`
- `Void Save()`
- `ClientConfiguration ToServerData()`
- `Boolean Delete()`

### `BasePathColumnData`
**Методы:**
- `Void SetPathFuncs(Func`3 deserialize, Func`2 convert, Func`2 serialize, Func`2 masterGroupGetterFunc, Func`2 outputGroupGetter, Func`3 filterAdder)`

### `BaseRepresentationObjectPathItem`
**Свойства:** DefaultName: String, Name: String, Type: PathItemType

### `BaseTaskObject`
**Свойства:** DateTimeInterval: TimeInterval, IsStartTimeSet: Boolean, IsEndTimeSet: Boolean, IsDurationSet: Boolean, StartTime: DateTime, EndTime: DateTime, Duration: Int32, Description: String, OrderParameter: OrderParameter, Order: String, TaskOrderNumber: Int32, Color: Int32, Style: ProjectStylesReferenceObject, IsFixingTask: Boolean, ResourceLinks: ReferenceObjectCollection`1, Labels: IEnumerable`1, StartTaskMessageGuid: GuidParameter, StartMailTask: MailTask, Progress: Double, Plan: BaseTaskObject, State: TaskState, AutoSendMessage: Boolean, MainWorkflowGuid: Guid, MainProcedureGuid: Guid, WorkflowObjects: ReferenceObjectCollection, WorkflowReference: Reference, ProceduresReference: Reference, ProcedureObjects: ReferenceObjectCollection, AnyReferenceObjectsLink: AnyReferenceLink, Owner: UserReferenceObject, Costs: Double, CurrentCosts: Double, WorkTimeManager: WorkTimeManager, Texts: TaskTexts, TopText: String, BottomText: String, LeftText: String, RightText: String, InsideText: String
**Методы:**
- `Boolean SetParent(ReferenceObject parentObject)`
- `Void AddToSaveSet(ReferenceObjectSaveSet saveSet)`
- `Void UpdateStartTime(DateTime startTime, ReferenceObjectSaveSet saveSet)`
- `Void UpdateEndTime(DateTime endTime, ReferenceObjectSaveSet saveSet)`
- `Void MoveStartTimeTo(DateTime date)`
- `Void MoveEndTimeTo(DateTime date)`
- `List`1 GetChildTasks()`
- `Void StartTask()`
- `Void SetStartMailTask(Guid mailTaskGuid)`
- `Void UpdateCosts(ReferenceObjectSaveSet saveSet)`
- `Void OnCalendarChanged()`
- `DateTime CalcSummTime(DateTime startTime, Int32 duration)`
- `Boolean ChangeEndTimeByDuration(Int32 duration)`
- `Void ChangeStartTimeByDuration(Int32 duration)`
- `Int32 CalcDuration(DateTime start, DateTime end)`
- `Void ChangeDurationByEndTime(DateTime endTime)`
- `Void ChangeDurationByStartTime(DateTime startTime)`

### `BaseVisualSetting`
**Свойства:** Color: Int32, IsVisible: Boolean, Size: Double, CanChangeIsVisible: Boolean, CanChangeColor: Boolean, CanChangeSize: Boolean

### `BillOfMaterials`
**Методы:**
- `Void UpdateLinkedBOMFile()`
- `Void GenerateNewReport(FileObject fileObject)`
- `IReadOnlyCollection`1 GetFileObjects()`

### `BomSectionsReference`
**Свойства:** Classes: BomSectionsTypes

### `BomSectionsReferenceObject`
**Свойства:** Name: String, Code: Int32

### `BomSectionsType`
**Свойства:** Classes: BomSectionsTypes

### `BomSectionsTypes`
**Свойства:** BomSection: BomSectionsType

### `BooleanParameter`
**Свойства:** IsEmpty: Boolean
**Методы:**
- `Boolean GetBoolean()`
- `TypeCode GetTypeCode()`

### `BorrowLinkedObject`
**Свойства:** Action: BorrowLinkedObjectAction
**Методы:**
- `Boolean SetAction(BorrowLinkedObjectAction action)`

### `BorrowLinkInfo`
**Свойства:** Key: BorrowLinkKey, Action: BorrowLinkedObjectAction

### `BorrowLinkKey`
**Свойства:** LinkId: Guid, IsSwapped: Boolean

### `BorrowLinkSetting`
**Свойства:** LinkGuid: Guid, Visible: Boolean, Status: BorrowObjectStatus

### `BorrowMacroContext`
**Свойства:** SourceObjects: List`1, DestinationObject: ReferenceObject, Result: List`1

### `BorrowObject`
**Свойства:** Reference: Reference, HasChildren: Boolean, ReferenceObject: ReferenceObject, ComplexLink: ComplexHierarchyLink, Ignored: Boolean, RevisionTypeGuid: Guid, CopyApplicability: Boolean, ExistEqualsParameters: Boolean, ExistEqualsOnlyLinkParameters: Boolean, IsChildrenLoaded: Boolean, Children: ReadOnlyCollection`1, BorrowParameters: ReadOnlyCollection`1, Parent: BorrowObject, ExistingUniqueObjectByEqualsParameters: ReferenceObject
**Методы:**
- `Boolean HasAnyLinkedObject(Guid linkId, Boolean isSwapped) (+1)`
- `IEnumerable`1 GetLinkedObjects(BorrowLinkKey linkKey) (+1)`
- `Void LoadChildren(HashSet`1 linksToLoad)`
- `Void FillBorrowParametersMap(IDictionary`2 map)`
- `IDictionary`2 GetBorrowParametersMap()`
- `BorrowObjectStatus GetObjectStatus(Boolean recalc)`
- `Dictionary`2 GetParameterValuesForCheckUnique(Boolean isNewParentObject, Boolean& existUniqueBorrowParameter)`
- `Void AddObjectParameter(ParameterInfo parameter, Object fromValue, Object toValue, Boolean onlySetValue)`
- `Object GetValue(ParameterInfo parameter, Object currentValue) (+2)`
- `Boolean FindChanged(ParameterInfo parameter, Object fromValue, BorrowParameterObject& resParameter)`

### `BorrowObjectManager`
**Свойства:** Struct: BorrowObjectStruct, LinkSettings: IReadOnlyCollection`1
**Методы:**
- `BorrowObjectManager CreateInstance(Guid parameterGroup)`
- `Void RegisterCreator(Guid parameterGroup, Func`1 factory)`
- `Void Initialize(ICollection`1 objects) (+3)`
- `Void SetLinkSettings(ICollection`1 linkSettings)`
- `Task`1 Execute(IProgress progress, Func`4 borrowStructureInitializer, CancellationToken cancellationToken)`

### `BorrowObjectStruct`
**Свойства:** DestinationObject: ReferenceObject, Formula: String, ClearHiddenLinks: Boolean, LinkActions: HashSet`1, SourceObjects: IReadOnlyCollection`1, ResultObject: ReferenceObject, ResultObjects: List`1, SupportCopyFiles: Boolean, PrototypeCopyContext: CopyReferenceObjectsContext, BorrowReference: Reference, Reference: Reference, HideNotUseObjectsInUI: Boolean, BorrowObjects: ReadOnlyCollection`1, AdditionalName: String
**Методы:**
- `Void AddUniqueParameter(ParameterInfo parameter, Object toValue)`
- `String GenerateUniqueValue(String parameterValue, ParameterInfo parameter, List`1 bufferValues)`
- `Void AddGlobalParameter(ParameterInfo parameter, Object fromValue, Object toValue)`
- `BorrowObject AddObject(BorrowObject borrowObject)`
- `BorrowObject FindObject(ReferenceObject referenceObject, ComplexHierarchyLink complexKey)`
- `String GetObjectStatusName(BorrowObject borrowObject)`
- `BorrowObject Create(ReferenceObject obj, ComplexHierarchyLink link, BorrowObject parent)`
- `BorrowLinkedObject CreateLinked(ReferenceObject obj, BorrowObject parent) (+1)`
- `Void ChangeLinkActions(HashSet`1 newActions)`

### `BorrowParameterObject`
**Свойства:** ParameterId: Int32, Parameter: ParameterInfo, FromValue: Object, ToValue: Object, OriginalValue: Object
**Методы:**
- `Object GetNewValue(Object currentValue)`

### `BorrowStatusChangedHandler`
**Методы:**
- `Void Invoke(Object sender, BorrowObjectStatus prevStatus, BorrowObjectStatus newStatus)`
- `IAsyncResult BeginInvoke(Object sender, BorrowObjectStatus prevStatus, BorrowObjectStatus newStatus, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `BoundsInterval`
**Свойства:** Start: PointParameterValueEx, End: PointParameterValueEx, Type: ParameterDataType

### `BrokenSetting`
**Свойства:** Description: CalendarSettingDescription, ErrorMessage: String

### `BusinessProcessesReferenceAccessor`
**Методы:**
- `Boolean Run(String name, RefObj refObj, Dictionary`2 variables, Boolean showDialog, String variablesTemplate, String begin, RefObjList appendantObjects) (+2)` [RU: Запустить]
- `Boolean Edit(String name, Dictionary`2 variables)` [RU: Изменить]
- `Boolean RunLinearProcess(String prototype, RefObj refObj, Boolean showDialog) (+5)` [RU: ЗапуститьЛинейныйПроцесс]
- `Void Complete(String process, String state, String solution, RefObjList objects, String comment)` [RU: Завершить]

### `ButtonFieldInputDialog`
**Свойства:** TypeName: String, Code: InArgument`1, Width: InArgument`1

### `ByteArrayParameter`
**Методы:**
- `Byte[] GetByteArray()`
- `TypeCode GetTypeCode()`

### `ByteParameter`
**Методы:**
- `Byte GetByte()`
- `TypeCode GetTypeCode()`

### `CachingFileServerObject`
**Свойства:** Class: CachingFileServerType, Name: StringParameter, ServerAddress: StringParameter, Users: ReferenceObjectCollection`1

### `CachingFileServerReference`
**Свойства:** Classes: CachingFileServerTypes

### `CachingFileServerType`
**Свойства:** Classes: CachingFileServerTypes, IsCachingFileServer: Boolean

### `CachingFileServerTypes`
**Свойства:** CachingFileServer: CachingFileServerType

### `CADBaseValue`
**Свойства:** ParameterInfo: CADParameterInfo

### `CADClient`
**Свойства:** Info: ServiceInfo
**Методы:**
- `CadDocumentRequestResult Open(String path, Boolean readOnly, Byte[] byteContext, ClientCallContext context)` [has Async]
- `CadDocumentRequestResult OpenVirtual(Guid referenceObjectGuid, Boolean readOnly, Byte[] byteContext, ClientCallContext context)` [has Async]
- `RequestResult Close(CadDocumentData document, Boolean save, ClientCallContext context)` [has Async]
- `StringRequestResult Export(CadDocumentData document, ExportContext exportContext, ClientCallContext context)` [has Async]
- `RequestResult Regenerate(CadDocumentData document, ClientCallContext context)` [has Async]
- `RequestResult RegenerateWithOption(CadDocumentData document, RegenerateOption regenerateOption, ClientCallContext context)` [has Async]
- `QualityAnalysisCollectionRequestResult Analyze3DModelQuality(CadDocumentData document, String reportFilePath, String analysisScript, ClientCallContext context)` [has Async]
- `VariableCollectionRequestResult GetVariables(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `VariableCollectionRequestResult SaveVariables(CadDocumentData document, String ownerId, List`1 variables, ClientCallContext context)` [has Async]
- `FragmentCollectionRequestResult GetFragments2D(CadDocumentData document, ClientCallContext context)` [has Async]
- `FragmentCollectionRequestResult GetFragments3D(CadDocumentData document, ClientCallContext context)` [has Async]
- `ConnectorCollectionRequestResult GetConnectors2D(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `ConnectorCollectionRequestResult GetConnectors3D(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `LCSCollectionRequestResult GetLCSs(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `Fragment3DRequestResult InsertFragment3D(CadDocumentData targetDocument, String targetLCSName, String fragmentPath, String fragmentLCSName, Boolean byConnector, Boolean embedded, ClientCallContext context)` [has Async]
- `RequestResult SaveInNomenclature(CadDocumentData document, Boolean recursive, Boolean autoCheckIn, ICollection`1 productStructures, ClientCallContext context)` [has Async]
- `ProductStructureCollectionRequestResult GetProductStructures(CadDocumentData documentData, ClientCallContext context)` [has Async]
- `CadDocumentRequestResult OpenPart(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `CadDocumentRequestResult OpenLink(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `NullableDoubleRequestResult GetRealProperty(CadDocumentData document, String ownerId, String propertyName, ClientCallContext context)` [has Async]
- `StringRequestResult GetTextProperty(CadDocumentData document, String ownerId, String propertyName, ClientCallContext context)` [has Async]
- `PropertyCollectionRequestResult GetProperties(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `DoubleRequestResult Compare(CadDocumentData document, String ownerId, String ownerLcs, String filePath, String fileLcs, ClientCallContext context)` [has Async]
- `StringRequestResult OpenLibrary(String fullPath, ClientCallContext context)` [has Async]
- `StringRequestResult CloseLibrary(String fullPath, ClientCallContext context)` [has Async]
- `RequestResult SetIntegrationRule(String integrationRule, ClientCallContext context)` [has Async]
- `BoolRequestResult IsCorrect(CadDocumentData document, String ownerId, ClientCallContext context)` [has Async]
- `PageInfoArrayRequestResult GetPagesInfo(CadDocumentData document, Int32[] types, ClientCallContext context)` [has Async]
- `RestResponseRequestResult CallPluginRestService(String pluginName, RestRequestData restRequest, ClientCallContext context)` [has Async]

### `CADDim`
**Методы:**
- `Void Accept(ICadObjectVisitor visitor)`

### `CadDocument`
**Свойства:** Path: String, ReadOnly: Boolean, Context: Object, Id: Int32, IsActive: Boolean, Provider: CadDocumentProvider
**Методы:**
- `Void Open(CadDocumentProvider provider)`
- `Void Close(Boolean save)`
- `VariableCollection GetVariables()`
- `FragmentCollection GetFragments2D()`
- `FragmentCollection GetFragments3D()`
- `LCSCollection GetLCSs()`
- `ConnectorCollection GetConnectors2D()`
- `ConnectorCollection GetConnectors3D()`
- `Fragment3D InsertFragment3D(LCS documentLCS, LCS fragmentLCS, String fragmentPath, Boolean embedded) (+1)`
- `Void SaveInNomenclature(ICollection`1 productStructures, Boolean autoCheckIn) (+1)`
- `ICollection`1 GetProductStructures()`
- `CadDocument OpenPart(Fragment fragment)`
- `CadDocument OpenLink(Fragment fragment)`
- `Void Regenerate(RegenerateOption regenerateOption) (+1)`
- `QualityAnalysisResult[] Analyze3DModelQuality(String reportFilePath, String analysisScript)`
- `String Export(ExportContext exportContext)`
- `PageInfo[] GetPagesInfo(Int32[] types)`

### `CadDocumentData`
**Свойства:** Path: String, ReadOnly: Boolean, ByteContext: Byte[], Id: Int32, VirtualAssembly: Guid, Context: Object

### `CadDocumentExtensions`
**Методы:**
- `TFlexPageInfo[] GetTFlexPagesInfo(CadDocument document, TFlexPageType[] pageTypes)`

### `CadDocumentProvider`
**Свойства:** IsActive: Boolean, Context: Object, Connection: ServerConnection, FilePreview: FilePreviewType
**Методы:**
- `CadDocumentProvider Connect(ServerConnection connection, String extension, String integrationRule, Object context) (+1)`
- `CadDocument OpenDocument(String path, Boolean readOnly, Object context)`
- `CadDocument OpenVirtualDocument(ReferenceObject referenceObject, Boolean readOnly, Object context)`
- `String RegisterLibrary(String path)`
- `RestResponse CallPluginRestService(String pluginName, RestRequest restRequest)`

### `CADElementTypeValue`
**Свойства:** DefaultEnumValue: CADElementTypeValue, DefaultValueAsObject: Object, DefaultValueAsString: String

### `CADElementValue`
**Свойства:** EnumValue: CADElementTypeValue, ValueAsObject: Object, ValueAsString: String, AttachedVariable: CADVar

### `CADFragment`
**Методы:**
- `Void Accept(ICadObjectVisitor visitor)`

### `CADLinkDescriptorInfo`
**Свойства:** LinkBackName: String, LinkName: String, LinkSystemName: String, UID: Guid

### `CADLinkedObjectInfo`
**Свойства:** LinkDescriptor: CADLinkDescriptorInfo, LinkedObjectSearchString: String, LinkedObjectGroupType: CADObjectTypes, LinkedObjectTypeSystemName: String

### `CadMeasure`
**Свойства:** Unit: String, ShowFullText: Boolean

### `CADMethodInfo`
**Свойства:** DisplayName: String, ID: Guid, IsAuxiliary: Boolean, IsStatic: Boolean, SystemName: String

### `CADObject`
**Свойства:** ID: UInt32, Name: String, DisplayName: String, CADType: CADObjectTypes
**Методы:**
- `String GetSearchIdentifier()`
- `Void Accept(ICadObjectVisitor visitor)`
- `Void SetAdditionalProperties(Object sourceObject)`

### `CADObjectInfo`
**Свойства:** ObjectId: UInt64, DocumentFileName: String, DisplayName: String, ObjectName: String, SearchString: String, SubType: CADObjectTypes, HasTable: Boolean, Visible: Boolean, Properties: CADObjectPropertyInfo[]

### `CADObjectPropertyInfo`
**Свойства:** Name: String, Description: String, DataType: CADObjectPropertiesTypes, MeasureUnit: String, Value: Object

### `CADParameterInfo`
**Свойства:** DisplayName: String, ID: Guid, IsAuxiliary: Boolean, IsStatic: Boolean, ReferenceTypeID: Guid, SystemName: String

### `CADServer`
**Свойства:** Info: ServiceInfo
**Методы:**
- `ValueTask`1 Open(String path, Boolean readOnly, Byte[] byteContext, ServerCallContext context)`
- `ValueTask`1 OpenVirtual(Guid referenceObjectGuid, Boolean readOnly, Byte[] byteContext, ServerCallContext context)`
- `ValueTask`1 Close(CadDocumentData document, Boolean save, ServerCallContext context)`
- `ValueTask`1 Export(CadDocumentData document, ExportContext exportContext, ServerCallContext context)`
- `ValueTask`1 Regenerate(CadDocumentData document, ServerCallContext context)`
- `ValueTask`1 RegenerateWithOption(CadDocumentData document, RegenerateOption regenerateOption, ServerCallContext context)`
- `ValueTask`1 Analyze3DModelQuality(CadDocumentData document, String reportFilePath, String analysisScript, ServerCallContext context)`
- `ValueTask`1 GetVariables(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 SaveVariables(CadDocumentData document, String ownerId, List`1 variables, ServerCallContext context)`
- `ValueTask`1 GetFragments2D(CadDocumentData document, ServerCallContext context)`
- `ValueTask`1 GetFragments3D(CadDocumentData document, ServerCallContext context)`
- `ValueTask`1 GetConnectors2D(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 GetConnectors3D(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 GetLCSs(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 InsertFragment3D(CadDocumentData targetDocument, String targetLCSName, String fragmentPath, String fragmentLCSName, Boolean byConnector, Boolean embedded, ServerCallContext context)`
- `ValueTask`1 SaveInNomenclature(CadDocumentData document, Boolean recursive, Boolean autoCheckIn, ICollection`1 productStructures, ServerCallContext context)`
- `ValueTask`1 GetProductStructures(CadDocumentData documentData, ServerCallContext context)`
- `ValueTask`1 OpenPart(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 OpenLink(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 GetRealProperty(CadDocumentData document, String ownerId, String propertyName, ServerCallContext context)`
- `ValueTask`1 GetTextProperty(CadDocumentData document, String ownerId, String propertyName, ServerCallContext context)`
- `ValueTask`1 GetProperties(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 Compare(CadDocumentData document, String ownerId, String ownerLcs, String filePath, String fileLcs, ServerCallContext context)`
- `ValueTask`1 OpenLibrary(String fullPath, ServerCallContext context)`
- `ValueTask`1 CloseLibrary(String fullPath, ServerCallContext context)`
- `ValueTask`1 SetIntegrationRule(String integrationRule, ServerCallContext context)`
- `ValueTask`1 IsCorrect(CadDocumentData document, String ownerId, ServerCallContext context)`
- `ValueTask`1 GetPagesInfo(CadDocumentData document, Int32[] types, ServerCallContext context)`
- `ValueTask`1 CallPluginRestService(String pluginName, RestRequestData restRequest, ServerCallContext context)`

### `CADServiceProxy`
**Методы:**
- `CadDocumentData Open(String path, Boolean readOnly, Object context)`
- `CadDocumentData OpenVirtual(Guid referenceObjectGuid, Boolean readOnly, Object context)`
- `Void Close(CadDocumentData document, Boolean save)`
- `String Export(CadDocumentData document, ExportContext context)`
- `PageInfo[] GetPagesInfo(CadDocumentData document, Int32[] types)`
- `Void Regenerate(CadDocumentData document, RegenerateOption regenerateOption) (+1)`
- `QualityAnalysisResult[] Analyze3DModelQuality(CadDocumentData document, String reportFilePath, String analysisScript)`
- `RestResponse CallPluginRestService(String pluginName, RestRequest restRequest)`
- `VariableCollection GetVariables(CadDocumentData document, String ownerId)`
- `VariableCollection SaveVariables(CadDocumentData document, String ownerId, VariableCollection variables)`
- `FragmentCollection GetFragments2D(CadDocumentData document)`
- `FragmentCollection GetFragments3D(CadDocumentData document)`
- `ConnectorCollection GetConnectors2D(CadDocumentData document, String ownerId)`
- `ConnectorCollection GetConnectors3D(CadDocumentData document, String ownerId)`
- `LCSCollection GetLCSs(CadDocumentData document, String ownerId)`
- `Fragment3D InsertFragment3D(CadDocumentData targetDocument, String targetLCSName, String fragmentPath, String fragmentLCSName, Boolean byConnector, Boolean embedded)`
- `Void SaveInNomenclature(CadDocumentData document, Boolean recursive, Boolean autoCheckIn, ICollection`1 productStructures) (+1)`
- `ICollection`1 GetProductStructures(CadDocumentData document)`
- `CadDocumentData OpenPart(CadDocumentData document, String ownerId)`
- `CadDocumentData OpenLink(CadDocumentData document, String ownerId)`
- `Nullable`1 GetRealProperty(CadDocumentData document, String ownerId, String propertyName)`
- `String GetTextProperty(CadDocumentData document, String ownerId, String propertyName)`
- `PropertyCollection GetProperties(CadDocumentData document, String ownerId)`
- `Double Compare(CadDocumentData document, String ownerId, String ownerLcs, String filePath, String fileLcs)`
- `String OpenLibrary(String fullPath)`
- `String CloseLibrary(String fullPath)`
- `Void SetIntegrationRule(String integrationRule)`
- `Boolean IsCorrect(CadDocumentData document, String ownerId)`

### `CADStructureElementInfo`
**Свойства:** StructureElementType: CADStructureElementTypeInfo, UID: Guid, ValueCollection: CADElementValueCollection, LinkedObjectInfoCollection: CADLinkedObjectInfoCollection

### `CADStructureElementTypeInfo`
**Свойства:** IsEnum: Boolean, Name: String, Description: String, SystemName: String, SystemParentName: String, ParentElementType: CADStructureElementTypeInfo, UID: Guid, Icon: String, IsAbstract: Boolean, TypeValueCollection: CADElementTypeValueCollection, MethodInfoCollection: CADMethodInfoCollection
**Методы:**
- `List`1 GetHierarchyTypes()`

### `CADVar`
**Свойства:** Name: String, TextValue: String, RealValue: Double, IsText: Boolean, Comment: String

### `CadWorkSessionsReference`
**Свойства:** Classes: CadWorkSessionsTypes
**Методы:**
- `String CreateWorkSessionName(ReferenceObject referenceObject)`

### `CadWorkSessionsType`
**Свойства:** Classes: CadWorkSessionsTypes, IsWorkSessionElementReferenceObject: Boolean, IsWorkSessionReferenceObject: Boolean

### `CadWorkSessionsTypes`
**Свойства:** WorkSessionElementReferenceObject: CadWorkSessionsType, WorkSessionReferenceObject: CadWorkSessionsType

### `CalculationInfo`
**Свойства:** CalculationType: Int32, Path: String, MacrosGuid: String, MacrosMethod: String, Formula: String, LinkGuid: String, LinkFilter: String, LinkParameter: String, ParameterSet: String, Splitter: String, AdditionalCalculatorId: Guid, AdditionalCalculatorSettings: String
**Методы:**
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `CalendarAppointmentBase`
**Свойства:** Header: String, Comment: String, Start: DateTime, End: DateTime, AllDay: Nullable`1, Key: Int32, LabelId: Int32, Status: Int32, Setting: CalendarCategorySettingBase, CanChangeTimeInterval: Boolean
**Методы:**
- `MacroContext GetMacroContext()`
- `Void SetMacroContext(MacroContext context)`
- `Object GetCoreObject()`
- `Void Release()`

### `CalendarAppointmentWithParameters`
**Свойства:** Setting: CalendarCategorySettingsWithParameters
**Методы:**
- `Boolean GetAllDayParameterValueWithSetting()`
- `Boolean GetAllDayParameterValue()`
- `DateTime GetStartTimeParameterValue()`
- `DateTime GetEndTimeParameterValue()`
- `String GetCommentParameterValue()`
- `String GetHeaderParameterValue()`
- `Void SetAllDayParameterValue(Boolean value)`
- `Void SetStartTimeParameterValue(DateTime newIntervalStartTime)`
- `Void SetEndTimeParameterValue(DateTime newIntervalEndTime)`

### `CalendarCategory`
**Свойства:** Manager: CalendarCategoryManager, Id: Guid, IsSystem: Boolean, IsVisible: Boolean, IsPublic: Boolean, Text: String, HasBrokenSettings: Boolean, SettingsCount: Int32, Name: String, IsChanged: Boolean, IsDeleted: Boolean, IsAdded: Boolean
**Методы:**
- `ReadOnlyCollection`1 GetSettings(Boolean getDeleted)`
- `ReadOnlyCollection`1 GetBrokenSettings()`
- `Void UpdateSetting(CalendarCategorySettingBase calendarCategorySetting)`
- `Boolean DeleteSetting(CalendarCategorySettingBase set)`
- `Boolean Add(CalendarCategorySettingBase set)`
- `Void ClearSettings()`

### `CalendarCategoryFactory`
**Методы:**
- `CalendarCategory Create(CalendarCategoryDescription calendarCategoryDescription, CalendarCategoryManager manager, ICalculateParameterValue parameterValueCalculator)`

### `CalendarCategoryManager`
**Свойства:** IsPublicChanged: Boolean, Connection: ServerConnection, SettingsFactory: CalendarSettingsFactory
**Методы:**
- `Boolean CheckBrokenCategories()`
- `ReadOnlyCollection`1 GetCategories()`
- `ReadOnlyCollection`1 GetBrokenCategories()`
- `ReadOnlyCollection`1 GetReferenceSettings()`
- `ReadOnlyCollection`1 GetVisibleReferenceSettings()`
- `Void InitializeCategories(String userContext)`
- `Void SaveCategories(String userContext)`
- `Boolean Add(CalendarCategory cat)`
- `Boolean Delete(CalendarCategory calendarCategory)`
- `Void DeleteSetting(CalendarCategorySettingBase setting)`
- `Void UpdateCategorySetting(Guid categoryGuid, CalendarCategorySettingBase setting)`
- `Void UpdateCategories(List`1 categories)`
- `IEnumerable`1 FillDataSource(Nullable`1 start, Nullable`1 end, CancellationToken cancellationToken)`
- `IEnumerable`1 FillDataSourceForSetting(CalendarCategorySettingBase setting, Nullable`1 start, Nullable`1 end, CancellationToken cancellationToken)`
- `Void SetObjectKey(ICalendarAppointment appointment)`
- `Void ClearCategories()`
- `CalendarCategorySettingBase GenerateSettingByType(SettingType settingType, CalendarCategory calendarCategory)`
- `Void BeginChanges()`
- `Void CancelChanges()`

### `CalendarCategorySettingBase`
**Свойства:** Id: Guid, Connection: ServerConnection, IsSystem: Boolean, Category: CalendarCategory, Editable: Boolean, AppointmentColor: Int32, AppointmentLabel: Int32, AppointmentStatus: Int32, AllDay: Nullable`1, Duration: Nullable`1, IsDeleted: Boolean, IsAdded: Boolean
**Методы:**
- `String GetName()`
- `IEnumerable`1 GetAppointments(Nullable`1 start, Nullable`1 end, CancellationToken cancellationToken)`
- `Void ResetCache()`
- `CalendarSettingDescription CreateDescription()`
- `Void Refresh()`

### `CalendarCategorySettingMailParameter`1`
**Свойства:** MailField: MailField
**Методы:**
- `T GetValue(ICalendarAppointment calendarAppointment)`
- `Void SetValue(ICalendarAppointment calendarAppointment, Object value)`

### `CalendarCategorySettingParameterExt`
**Методы:**
- `ReferencePath AsReferencePath(ICalendarCategorySettingParameter`1 parameter)`
- `MailField AsMailField(ICalendarCategorySettingParameter`1 parameter)`

### `CalendarCategorySettingReferenceParameter`1`
**Свойства:** ReferencePath: ReferencePath
**Методы:**
- `T GetValue(ICalendarAppointment calendarAppointment)`
- `Void SetValue(ICalendarAppointment calendarAppointment, Object value)`

### `CalendarCategorySettingsWithParameters`
**Свойства:** HeaderParameter: ICalendarCategorySettingParameter`1, CommentParameter: ICalendarCategorySettingParameter`1, StartTimeParameter: ICalendarCategorySettingParameter`1, EndTimeParameter: ICalendarCategorySettingParameter`1, AllDayParameter: ICalendarCategorySettingParameter`1, HeaderCalculatedParameter: CalculationInfo, DescriptionCalculatedParameter: CalculationInfo, StartTimeCalculatedParameter: CalculationInfo, EndTimeCalculatedParameter: CalculationInfo, AllDayCalculatedParameter: CalculationInfo
**Методы:**
- `Void FillParameters(ICalendarAppointment calendarAppointment, CancellationToken cancellationToken)`
- `Boolean GetAllDayParameterValue(ICalendarAppointment calendarAppointment)`
- `Boolean GetAllDayParameterValueWithSetting(ICalendarAppointment calendarAppointmentWithParameters)`
- `DateTime GetStartTimeParameterValue(ICalendarAppointment calendarAppointment)`
- `DateTime GetEndTimeParameterValue(ICalendarAppointment calendarAppointment)`
- `String GetCommentParameterValue(ICalendarAppointment calendarAppointment)`
- `String GetHeaderParameterValue(ICalendarAppointment calendarAppointment)`
- `Void SetAllDayParameterValue(ICalendarAppointment calendarAppointment, Boolean value)`
- `Void SetStartTimeParameterValue(ICalendarAppointment calendarAppointment, DateTime value)`
- `Void SetEndTimeParameterValue(ICalendarAppointment calendarAppointment, DateTime value)`
- `CalendarSettingDescription CreateDescription()`

### `CalendarMailFolderSetting`
**Свойства:** FolderGuid: Guid, AccountGuid: Guid, IsTaskFolder: Boolean, Filter: Filter
**Методы:**
- `String GetName()`
- `IconImage GetIcon()`
- `Void Refresh()`
- `Account GetAccount()`
- `Void ResetCache()`
- `CalendarSettingDescription CreateDescription()`

### `CalendarReference`
**Свойства:** Classes: CalendarTypes

### `CalendarReferenceObject`
**Свойства:** Class: CalendarType, WorkingTimesLink: OneToManyLink, WorkingTimes: ICollection`1, WorkTimeManager: WorkTimeManager, Name: StringParameter
**Методы:**
- `Void UpdateWorkTimeElements()`
- `Boolean HasAnyWorkTimeInterval()`
- `Void LoadWorkingTimes()`

### `CalendarReferenceSetting`
**Свойства:** Reference: Reference, ReferenceFilter: Filter, RootReferenceObject: ReferenceObject, CanCreateObjects: Boolean
**Методы:**
- `String GetName()`
- `CalendarSettingDescription CreateDescription()`
- `Void AddToLoadSettings(Reference reference)`
- `IEnumerable`1 GetAppointments(Reference reference, Nullable`1 start, Nullable`1 end, CancellationToken cancellationToken)`
- `IEnumerable`1 FillDataSourceByLoadedObjects(IEnumerable`1 referenceObjects, CancellationToken cancellationToken)`
- `Void ResetCache()`
- `Void Refresh()`

### `CalendarReminderSetting`
**Методы:**
- `String GetName()`
- `String GetCommentParameterValue(ICalendarAppointment calendarAppointment)`
- `String GetHeaderParameterValue(ICalendarAppointment calendarAppointment)`
- `DateTime GetStartTimeParameterValue(ICalendarAppointment calendarAppointment)`
- `Void SetStartTimeParameterValue(ICalendarAppointment calendarAppointment, DateTime value)`
- `Void ResetCache()`
- `CalendarSettingDescription CreateDescription()`
- `Void Refresh()`

### `CalendarSettingsFactory`
**Методы:**
- `CalendarMailFolderSetting GenerateMailFolderSetting(CalendarCategory category)`
- `CalendarReferenceSetting GenerateReferenceSetting(CalendarCategory category)`
- `CalendarCategorySettingBase Create(CalendarSettingDescription description, ServerConnection connection, ICalculateParameterValue parameterValueCalculator)`

### `CalendarType`
**Свойства:** Classes: CalendarTypes, WorkTimePriorityComparer: Func`2

### `CallbackSolution`
**Свойства:** Text: String, Tag: Object, IsAccepted: Boolean

### `CallbackSolutions`
**Методы:**
- `Boolean Invoke(ICollection`1 solutions)`
- `IAsyncResult BeginInvoke(ICollection`1 solutions, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `CallbackSolutionsAsync`
**Методы:**
- `Task`1 Invoke(ICollection`1 solutions)`
- `IAsyncResult BeginInvoke(ICollection`1 solutions, AsyncCallback callback, Object object)`
- `Task`1 EndInvoke(IAsyncResult result)`

### `CaptionFieldInputDialog`
**Свойства:** TypeName: String, Caption: InArgument`1

### `Catalog`
**Свойства:** Manager: CatalogManager, RootFolders: ReadOnlyCollection`1, Id: Int32, Guid: Guid, Name: String, IsPrivate: Boolean, IsAdded: Boolean, IsModified: Boolean, IsSystem: Boolean, AccessUsersUseType: ItemListUseType, Item: CatalogFolder, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Void Reload()` [has Async]
- `List`1 FindCatalogFolders(String name)`
- `CatalogFolder FindCatalogFolder(Int32 id) (+1)`
- `Boolean Save()`
- `Boolean Delete()`
- `ReferenceObjectCollection CreateLoader(IEnumerable`1 folders, Filter filter, MacroContext formulaContext)`
- `List`1 GetAccessUsers()`
- `Void SetAccessUsers(IEnumerable`1 users)`
- `Boolean ChangingFolderObjectsAllowed()`
- `Int32 IndexOf(CatalogFolder item)`
- `Boolean Contains(CatalogFolder item)`
- `Void CopyTo(CatalogFolder[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`
- `Int32 CompareTo(Catalog other)`

### `CatalogFolder`
**Свойства:** Catalog: Catalog, Id: Int32, Guid: Guid, Name: String, Icon: IconImage, HasIcon: Boolean, IsIconLoaded: Boolean, ShowObjects: Boolean, Parent: CatalogFolder, Subfolders: ReadOnlyCollection`1, IsAdded: Boolean, IsModified: Boolean, IsSystem: Boolean, Objects: ReferenceObjectCollection, AsUserFolder: UserFolder, AsSearchFolder: SearchFolder, AsFolderGroup: FolderGroup
**Методы:**
- `List`1 GetAllSubfolders()`
- `Boolean Save()` [has Async]
- `Boolean Delete()` [has Async]
- `List`1 FindSubFolders(String name)`
- `CatalogFolder FindSubFolder(Guid guid)`
- `Int32 CompareTo(CatalogFolder other)`

### `CatalogManager`
**Свойства:** ReferenceInfo: ReferenceInfo, Reference: Reference, SearchQueries: SearchQueryReference, Item: Catalog, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `List`1 Find(String name) (+2)`
- `List`1 FindCatalogFolder(String name) (+1)`
- `Void Reload()` [has Async]
- `Int32 IndexOf(Catalog item)`
- `Boolean Contains(Catalog item)`
- `Void CopyTo(Catalog[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `CategoriesFilterData`
**Свойства:** ShowAllCategories: Boolean, ShowEmptyCategories: Boolean, ProductCategories: List`1

### `CategoriesReference`
**Свойства:** Classes: CategoriesTypes
**Методы:**
- `CategoriesReferenceObject Find(String name)` [has Async]

### `CategoriesReferenceObject`
**Свойства:** Class: CategoriesType, Name: StringParameter

### `CategoriesType`
**Свойства:** Classes: CategoriesTypes, IsLinkCategory: Boolean

### `CategoriesTypes`
**Свойства:** LinkCategory: CategoriesType

### `CategoryCriteria`
**Методы:**
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`

### `CategoryMailField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `String ConvertToString(Object value)`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `CategoryReference`
**Свойства:** Classes: CategoryTypes

### `CategoryReferenceObject`
**Свойства:** Class: CategoryType, Name: StringParameter, Icon: IconParameter

### `CategoryType`
**Свойства:** Classes: CategoryTypes, IsCategory: Boolean

### `CategoryTypes`
**Свойства:** Category: CategoryType

### `Certificate`
**Свойства:** Class: CertificateType, Name: StringParameter, IsExpired: Boolean, ExpirationDate: DateTimeParameter, Algorithm: StringParameter, Hash: PasswordParameter, Note: StringParameter, BeginningOfExpiration: DateTimeParameter, UseTrustedUsersList: BooleanParameter, EncryptedText: StringParameter, UserCertificates: ReferenceObjectCollection
**Методы:**
- `Boolean OpenCloseSymmetricKey(String phKeyPassword)`
- `Tuple`2 CreateKeysPair(String sourcePasswordHash)`
- `Boolean IsCertificateAvailable()`
- `Filter CreateFilter(ServerConnection connection, Boolean showExpired)`
- `ReferenceObject AddUserCertificates(ReferenceObject newLinkedObject)`
- `Boolean RemoveUserCertificates(ReferenceObject linkedObject)`

### `CertificateReference`
**Свойства:** Classes: CertificateTypes

### `CertificateType`
**Свойства:** IsCertificate: Boolean, Classes: CertificateTypes
**Методы:**
- `List`1 GetCertificates()`

### `CertificateTypes`
**Свойства:** Certificate: CertificateType

### `ChancelleryReferenceAccessor`
**Методы:**
- `ResolutionTaskObj CreateResolutionTask()` [RU: СоздатьЗадание]

### `ChangeLinkActivityBase`
**Свойства:** Object: InArgument`1, LinkedObject: InArgument`1, Reference: InArgument`1, Link: InArgument`1

### `Changelist`
**Свойства:** Connection: ServerConnection, Number: Int32, User: User, UserName: String, HostName: String, Date: DateTime, Comment: String, Label: String
**Методы:**
- `ChangelistObject FindObjectInChangelist(ReferenceObject referenceObject)`
- `IEnumerator`1 GetEnumerator()`

### `ChangelistObject`
**Свойства:** Changelist: Changelist, Id: Int32, Guid: Guid, Reference: ReferenceInfo, ReferenceObject: ReferenceObject, CurrentReferenceObject: ReferenceObject, Name: String, Version: Int32, Class: ClassObject, Icon: IconImage, ChangeTypeIcon: IconImage, IsAdded: Boolean, IsDeleted: Boolean, IsUpdated: Boolean, IsRestored: Boolean, IsLabeled: Boolean, SourceVersion: Int32, IsPrototype: Boolean, IsVersionDeleted: Boolean, ChangeTypeDescription: String

### `ChangePictureFieldInputDialog`
**Свойства:** TypeName: String, Index: InArgument`1, Object: InArgument`1, ImagePath: InArgument`1

### `CharacteristicClassReference`
**Свойства:** Classes: CharacteristicClassTypes

### `CharacteristicClassReferenceObject`
**Свойства:** Class: CharacteristicClassType, Name: StringParameter, IsPercent: BooleanParameter, IsVariable: BooleanParameter, Symbol: StringParameter, DataType: Int32Parameter, CharacteristicGroupClass: CharacteristicGroupClassReferenceObject, LinkClassCharacteristicMeasure: Unit

### `CharacteristicClassType`
**Свойства:** Classes: CharacteristicClassTypes, IsCharacterClass: Boolean

### `CharacteristicClassTypes`
**Свойства:** CharacterClass: CharacteristicClassType

### `CharacteristicGroupClassReference`
**Свойства:** Classes: CharacteristicGroupClassTypes

### `CharacteristicGroupClassReferenceObject`
**Свойства:** Class: CharacteristicGroupClassType, Name: StringParameter, ForVariables: BooleanParameter, CharacteristicClasses: ReferenceObjectCollection`1

### `CharacteristicGroupClassType`
**Свойства:** Classes: CharacteristicClassTypes, IsCharacteristicGroupClass: Boolean

### `CharacteristicGroupClassTypes`
**Свойства:** CharacteristicGroupClass: CharacteristicGroupClassType

### `CharacteristicGroupReference`
**Свойства:** Classes: CharacteristicGroupTypes
**Методы:**
- `Boolean DeleteEmptyCharacteristicGroup(CharacteristicGroupReferenceObject groupObject, ReferenceObjectSaveSet saveSet)` [has Async]
- `CharacteristicGroupReferenceObject FindExistedCharacteristicGroup(CharacteristicClassReferenceObject characteristicClass, IEnumerable`1 characteristics)`

### `CharacteristicGroupReferenceObject`
**Свойства:** Class: CharacteristicGroupType, Name: StringParameter, CharacteristicGroupClassObject: GuidParameter, ForVariables: BooleanParameter, LinkGroupCharacteristics: ReferenceObjectCollection, Characteristics: ReferenceObjectCollection`1
**Методы:**
- `ReferenceObject AddLinkGroupCharacteristic(ReferenceObject newLinkedObject)`
- `CharacteristicReferenceObject AddCharacteristic(CharacteristicReferenceObject newLinkedCharacteristic)`
- `Boolean RemoveLinkGroupCharacteristic(ReferenceObject linkedObject)`
- `Boolean RemoveCharacteristic(CharacteristicReferenceObject linkedCharacteristic)`

### `CharacteristicGroupType`
**Свойства:** Classes: CharacteristicGroupTypes, IsCharacteristicGroup: Boolean

### `CharacteristicGroupTypes`
**Свойства:** CharacteristicGroup: CharacteristicGroupType

### `CharacteristicReference`
**Свойства:** Classes: CharacteristicTypes
**Методы:**
- `CharacteristicReferenceObject CreateCharacteristic(CharacteristicClassReferenceObject characteristicClassObject, CharacteristicGroupReferenceObject characteristicGroupObject)` [has Async]
- `IReadOnlyList`1 CreateCharacteristics(IEnumerable`1 characteristicObjects)` [has Async]
- `ReferenceObjectCopySet CopyCharacteristic(CharacteristicReferenceObject prototype)`
- `Boolean RemoveLinkedCharacteristic(OneToManyLink characteristicsLink, CharacteristicReferenceObject characteristicObject, ReferenceObjectSaveSet saveSet) (+1)` [has Async]
- `Boolean ContainsLinkedCharacteristicsGroups(ClassObject classObject)` [has Async]
- `ParameterGroup[] GetLinkedCharacteristicsGroups(ClassObject classObject)` [has Async]
- `Boolean ClearLinkedCharacteristics(OneToManyLink characteristicsLink, ReferenceObjectSaveSet saveSet) (+1)` [has Async]
- `IReadOnlyList`1 CreateCharacteristicsByClassifiers(ReferenceObject referenceObject, Guid linkGuid, List`1 characteristicTypes)`

### `CharacteristicReferenceObject`
**Свойства:** Class: CharacteristicType, ValueString: StringParameter, ValueYesNo: BooleanParameter, Summary: StringParameter, IsVariable: BooleanParameter, LowerTolerance: DoubleParameter, IsPercent: BooleanParameter, Name: StringParameter, Symbol: StringParameter, IsTolerancePercent: BooleanParameter, UpperTolerance: DoubleParameter, CharacterTypeID: Int32Parameter, ValueDate: DateTimeParameter, ValueReal: DoubleParameter, MinValue: DoubleParameter, DataType: Int32Parameter, ValueInteger: Int32Parameter, MaxValue: DoubleParameter, Mode: StringParameter, Comment: StringParameter, LinkCharacterMeasure: ReferenceObject, CharacteristicGroup: CharacteristicGroupReferenceObject
**Методы:**
- `Boolean CharacteristicUsagesExists(OneToManyLink toCharacteristicsLink) (+1)` [has Async]

### `CharacteristicsTypePathItem`
**Свойства:** Icon: IconImage, CharacteristicsType: CharacteristicClassReferenceObject, CharacteristicsDataType: CharacteristicsDataType, Name: String, Type: PathItemType

### `CharacteristicsTypesPathItem`
**Свойства:** Icon: IconImage, Name: String, SupportSearchType: SupportSearchTypes, Type: PathItemType

### `CharacteristicType`
**Свойства:** Classes: CharacteristicTypes, IsCharacterReference: Boolean

### `CharacteristicTypes`
**Свойства:** CharacteristicReference: CharacteristicType

### `ChartSettings`
**Свойства:** RowEvenColor: Int32, RowOddColor: Int32, RowReadOnlyColor: Nullable`1, SelectedRowHighlightColor: Int32, ColumnHolidayColor: Int32, ColumnCurrentColor: Int32, LineColor: Int32, LineThickness: Double, RowHeightStep: Double, ElementRelativeRowHeight: Double, HeaderColor: Int32, HeaderCurrentColor: Int32, HeaderFontSettings: FontSetting, SelectedElementBorderColor: Int32, FocusedElementBorderColor: Int32

### `CheckStatusTypeConverter`
**Методы:**
- `Boolean GetStandardValuesSupported(ITypeDescriptorContext context)`
- `StandardValuesCollection GetStandardValues(ITypeDescriptorContext context)`
- `Boolean CanConvertTo(ITypeDescriptorContext context, Type destinationType)`
- `Object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, Object value, Type destinationType)`

### `ChildHierarchyLinksPathItem`
**Свойства:** Type: PathItemType, Name: String
**Методы:**
- `Boolean IsOneToMany()`

### `ChildObjectsPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `ChildrenObjectsStructure`
**Свойства:** ShowAddCommandLock: Nullable`1, ShowRemoveCommandLock: Nullable`1, IsLinkOrParameterGroup: Boolean, Type: StructureGroupTypes
**Методы:**
- `String AppendToPath(String path, HierarchyDirections hierarchyDirection, String pathItem) (+1)`

### `ChunkObjectsArgs`
**Свойства:** Empty: ChunkObjectsArgs, Part: Int32, Objects: List`1, HierarchyLinks: List`1

### `ClassCatalogFolder`
**Свойства:** Class: ClassObject, HasIcon: Boolean

### `ClassGroupSettings`
**Свойства:** IsInherit: Boolean, Connection: ServerConnection
**Методы:**
- `String Serialize()`
- `Void Deserialize(String data)`

### `ClassObject`
**Свойства:** Classes: ClassTree, Id: Int32, Guid: Guid, Base: ClassObject, ChildClasses: ClassObjectCollection, CanContainChildren: Boolean, Icon: IconImage, IconLoaded: Boolean, Name: String, Comment: String, SupportsSaveAndCreate: Boolean, ShowChangeCommandInObjectProperties: Nullable`1, IsAbstract: Boolean, IsSealed: Boolean, UseBaseClassIcon: Boolean, CanCreateInRoot: Boolean, InheritRevisionNamingRule: Boolean, RevisionNamingRule: RevisionNamingRuleObject, PropertiesDisplayType: PropertiesDisplayType, CreateFromPrototype: Boolean, Hidden: Boolean, CanCreateObjects: Boolean, CanEdit: Boolean, CanDelete: Boolean, IsStandaloneProductByDefault: Boolean, ChildObjectClasses: ClassObjectCollection, InheritMasterObjectClasses: Boolean, MasterObjectClasses: ClassObjectCollection, ParameterGroups: ParameterGroupCollection, SwappedToSelfParameterGroups: ParameterGroupCollection, Attributes: ClassObjectAttributes, SigningParameters: String, IsUniqueIndexInherit: Boolean, UniqueIndex: UniqueIndex, Dialog: Dialog, WebDialog: Dialog, HierarchyLinkDialog: Dialog, HierarchyLinkWebDialog: Dialog, IsSupportMultiAttachmentInherit: Boolean, SupportMultiAttachment: Boolean, IsSchemeInherit: Boolean, IsDefaultStageInherit: Boolean, Scheme: Scheme, DefaultStage: SchemeStage, HasLinkedNomenclatureType: Boolean, LinkedNomenclatureType: NomenclatureType, InheritCanChange: Boolean, CanChange: Boolean, XmlId: String, ObjectFormat: ObjectFormat
**Методы:**
- `Boolean CanCreateChildObject(ClassObject classObject)`
- `Boolean GetShowChangeCommandWithInheritance()`
- `ParameterGroupCollection GetUnattachedParameterGroups()`
- `T GetGroupSettings(Guid settingsId, ParameterGroup group)` [has Async]
- `Boolean SetGroupSettings(Guid settingsId, ParameterGroup group, T settings)` [has Async]
- `Boolean ClearGroupSettings(Guid settingsId, ParameterGroup group)` [has Async]
- `ClassObjectCollection GetParentObjectClasses()`
- `Boolean IsInherit(ParameterGroup group) (+3)`
- `ClassObject GetBaseClassOfGroup(ParameterGroup group)`
- `Boolean IsBaseClassFor(ClassObject classObject)`
- `Boolean CanChangeTo(ClassObject other)`
- `ClassObjectCollection GetAllChildClasses()`
- `Void SetEventHandlersInheritance(ParameterGroupEvent event, Nullable`1 inheritEventHandlers)` [has Async]
- `Nullable`1 GetEventHandlersInheritance(ParameterGroupEvent event)`
- `List`1 GetEventHandlers(ParameterGroupEvent event)`
- `Int32 CompareTo(ClassObject other) (+1)`
- `Boolean TryParseXmlId(String xmlId, Int32& id, Boolean& deleted)`
- `List`1 GetSigningParametersGuids()`
- `SigningParametersInfo GetSigningParametersInfo()` [has Async]
- `Void SetSigningParameters(List`1 signingParameters)` [has Async]

### `ClassObjectAccessor`
**Свойства:** Name: String [RU: Имя], Guid: Guid [RU: УникальныйИдентификатор], Parameters: List`1 [RU: Параметры]
**Методы:**
- `Boolean IsInherit(String className) (+1)` [RU: ПорожденОт]
- `Boolean ContainsLink(String link)` [RU: ПорожденОт]
- `Int32 CompareTo(Object obj)` [RU: ПорожденОт]
- `Boolean СодержитСвязь(String имяСвязи)` [RU alternative]

### `ClassObjectAttribute`
**Свойства:** Attributes: ClassObjectAttributes, Name: String, IsSystem: Boolean, CanSerialize: Boolean, CanChangeCaption: Boolean, Caption: String, Value: Object, IsReadOnly: Boolean, CanRemove: Boolean
**Методы:**
- `Void SetModified()`

### `ClassObjectAttribute`1`
**Свойства:** CanChangeCaption: Boolean, IsSystem: Boolean, Caption: String, Value: Object, CanRemove: Boolean

### `ClassObjectAttributes`
**Свойства:** Class: ClassObject, BaseClass: ClassObject, Item: ClassObjectAttribute, IsReadOnly: Boolean, IsModified: Boolean, Count: Int32
**Методы:**
- `Void AddAttribute(String name, ClassObjectAttribute attr)`
- `Boolean RemoveAttribute(String name)`
- `Boolean IsValid(String name)`
- `Void Validate(String name)`
- `T GetValue(String name)`
- `Boolean SetValue(String name, Object value)`
- `Boolean Contains(String name)`
- `Boolean TryGetAttribute(String name, ClassObjectAttribute& attr)`
- `IEnumerator`1 GetEnumerator()`

### `ClassObjectBuilder`
**Свойства:** Classes: ClassTree, Class: ClassObject, Base: ClassObject, ParameterGroups: ParameterGroupCollection, SwappedToSelfParameterGroups: SwappedToSelfCollection, ChildObjectClasses: ClassObjectCollection, ParentObjectClasses: ClassObjectCollection, MasterObjectClasses: ClassObjectCollection, Attributes: ClassObjectAttributes, IsAdded: Boolean, IsModified: Boolean, Icon: IconImage, CanChangeIcon: Boolean, Name: String, Comment: String, IsAbstract: Boolean, IsSealed: Boolean, UseBaseClassIcon: Boolean, CanCreateInRoot: Boolean, SupportsSaveAndCreate: Boolean, ShowChangeCommandInObjectProperties: Nullable`1, PropertiesDisplayType: PropertiesDisplayType, CreateFromPrototype: Boolean, Hidden: Boolean, IsStandaloneProductByDefault: Boolean, IsSchemeInherit: Boolean, IsDefaultStageInherit: Boolean, UniqueIndex: UniqueIndex, Scheme: Scheme, DefaultStage: SchemeStage, InheritCanChange: Boolean, CanChange: Boolean, InheritMasterObjectClasses: Boolean, ObjectFormat: ObjectFormat, SupportMultiAttachment: Boolean, IsSupportMultiAttachmentInherit: Boolean, InheritRevisionNamingRule: Boolean, RevisionNamingRule: RevisionNamingRuleObject
**Методы:**
- `Void Save()` [has Async]
- `Void Delete(ClassObject classObject)` [has Async]

### `ClassObjectExtensions`
**Методы:**
- `ReferenceInfo GetReferenceInfo(ClassObject classObject)`
- `Icon CloneIcon(ClassObject classObject)`

### `ClassObjectHelper`
**Методы:**
- `ClassObject FindClass(ServerConnection connection, String referenceName, String className) (+1)`

### `ClassObjectLinksGroup`
**Свойства:** ClassObject: ClassObject, LinksParameterGroups: ParameterGroupCollection, ReferencePath: ReferencePath, IsFolder: Boolean, HasChildren: Boolean

### `ClassObjectParametersGroup`
**Свойства:** ClassObject: ClassObject, IsFolder: Boolean, HasChildren: Boolean

### `ClassObjectStructure`
**Свойства:** ShowEmptyFolderLock: Nullable`1, ShowFolderLock: Nullable`1, ShowCreateCommandLock: Nullable`1, ShowAddCommandLock: Nullable`1, ShowDeleteCommandLock: Nullable`1, ShowRemoveCommandLock: Nullable`1, CanHidedLock: Nullable`1, Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `ClassObjectTool`
**Свойства:** ClassObject: ClassObject

### `ClassTree`
**Свойства:** AllClasses: ClassObjectCollection, Owner: ParameterGroup, BaseClasses: ClassObjectCollection, ContainsFolderClasses: Boolean
**Методы:**
- `ClassObject Find(Int32 classId) (+2)`
- `ClassObjectCollection GetRootClasses()`
- `ClassObjectCollection GetRootBaseClasses()`
- `ClassObjectCollection GetNotAbstractClasses()`
- `ClassObjectCollection GetFolderClasses()`
- `ClassObjectCollection GetParameterGroupClasses(ParameterGroup parameterGroup, Boolean includeInherit)`
- `IEnumerable`1 GetIndexClasses(UniqueIndex index)`

### `ClearCollectionActivity`1`
**Свойства:** Values: InArgument`1

### `ClientConfiguration`
**Свойства:** IsDefault: Boolean, RegistryName: String, RegistryKey: String, CurrentRegistryKey: String, CommandLineArguments: String, MainWindowIcon: IconImage, SkinName: String, MainWindowTitle: String, LoginWindowTitle: String, Default: ClientConfiguration, AsClientConfiguration: ClientConfiguration
**Методы:**
- `Image GetLoginWindowImage()`
- `Byte[] GetLoginWindowImageBytes()`
- `Void SetLoginWindowImage(Image image)`
- `ClientConfiguration ToServerData()`

### `ClientView`
**Свойства:** Connection: ServerConnection, Id: Int32, Current: ClientView, IsAdministrator: Boolean, IsSystem: Boolean, Name: String, HostName: String, HostId: Int32, UserId: Int32, UserName: String, WorkingFolder: String, WorkingFolderPendingValue: String, WorkingFolderPendingStatus: WorkingFolderPendingStatus
**Методы:**
- `List`1 GetAllClientViews(ServerConnection connection) (+1)` [has Async]
- `List`1 GetHosts(ServerConnection connection) (+1)`
- `User GetUser()` [has Async]

### `CodeInfo`
**Свойства:** Type: CodeType, Language: ProgrammingLanguage, Version: Int32
**Методы:**
- `Boolean TryParse(String value, CodeInfo& info)`

### `CodeMacro`
**Свойства:** IsMethod: Boolean, IsCompiled: Boolean, CompilationResult: CompilationResult
**Методы:**
- `MacroValidationResults Validate()`
- `IEnumerable`1 GetEntryPoints()`
- `Type GetMacroProviderType()`
- `IEnumerable`1 GetReferences()`
- `CompilationResult Compile()`
- `Void DeleteAssembliesFromMacroFolder(ServerConnection connection, Boolean throwOnError)`
- `Int32 GetUserCodeOffset()`

### `CodeManager`
**Методы:**
- `Boolean IsFlowchartCode(String code)`
- `Boolean IsXml(String value)`

### `CodeVersionConverter`
**Методы:**
- `Boolean IsNeedConvert(String code)`
- `String TryConvert(String code)`
- `String Convert(String code)`

### `CodifierReference`
**Свойства:** Classes: CodifierTypes

### `CodifierReferenceObject`
**Свойства:** Class: CodifierType, Name: StringParameter, NumberParameter: StringParameter, InnerReference: GuidParameter, Context: StringParameter, ForceIncrementCounter: BooleanParameter, CounterReferenceObjects: List`1, ReferenceObjectTypes: ReferenceObjectCollection, NumberElements: ReferenceObjectCollection
**Методы:**
- `String GetNextNumber(ReferenceObject referenceObject)`
- `String GetTestNumber(IList`1 textParametersValues)`
- `Void AddLinkedCounter(ReferenceObject counterRegistryReferenceObject)`
- `Boolean ResetCounter()`
- `Void RenumberAllObjects(ServerConnection connection, CancellationToken cancellationToken, IProgress`1 progress)`
- `Boolean HasMatchWithCurrentCodeTemplate(ReferenceObject referenceObject, String code)`
- `ReferenceObject CreateNumberElements(Guid listObjectClass) (+1)`

### `CodifierType`
**Свойства:** Classes: CodifierTypes, IsCodifier: Boolean

### `CodifierTypes`
**Свойства:** Codifier: CodifierType

### `CombineFilesProvider`
**Свойства:** OutputPath: String, PageTypes: Int32[], FilesToCombine: String[], ShortDenotations: String[], IsEmbedded: Boolean
**Методы:**
- `Byte[] Serialize()`
- `CombineFilesProvider Deserialize(Byte[] data)`
- `Void Execute(ServerConnection connection)`
- `String GetLinkPath(String file)`

### `CommandDisplayModeExtensions`
**Методы:**
- `String GetName(CommandDisplayMode mode)`

### `CommentCodeActivity`1`
**Свойства:** Comment: String

### `CommentFieldInputDialog`
**Свойства:** TypeName: String, Comment: InArgument`1

### `CommentLinkReference`
**Свойства:** Classes: CommentTypes

### `CommentNativeActivity`1`
**Свойства:** Comment: String

### `CommentReferenceObject`
**Свойства:** Class: CommentType, Name: StringParameter, Text: StringParameter, DetailedDescription: StringParameter, DescriptionFormatType: DescriptionFormatType, DescriptionTextFormat: Int32Parameter, OnBehalf: User, LinkedMaterials: AnyReferenceLink
**Методы:**
- `ReferenceObject AddLinkedMaterial(ReferenceObject newLinkedObject)`
- `Boolean RemoveLinkedMaterial(ReferenceObject linkedObject)`

### `CommentType`
**Свойства:** Classes: CommentTypes, IsComment: Boolean, IsStatusChangeComment: Boolean

### `CommentTypes`
**Свойства:** Comment: CommentType, StatusChangeComment: CommentType

### `CommonApplication`
**Свойства:** Connection: ServerConnection, EventServiceApplication: Boolean, FileObjectId: Guid, Configurations: List`1, ConfigurationUseType: ConfigurationUseType, Guid: Guid, Name: String, Description: String, AssemblyPath: String, ReadOnly: Boolean, Type: ApplicationType

### `CommonToolsManager`
**Свойства:** Connection: ServerConnection, Favorites: ToolGroup, Language: Language, Macro: ToolGroup, Math: ToolGroup, Surrounds: ToolGroup, References: ToolGroup, Groups: Dictionary`2, Interface: String, SupportsViews: Boolean
**Методы:**
- `Void UpdateTools()`
- `List`1 LoadGroups(Assembly assembly, String fileName)`
- `ToolGroup LoadGroup(Assembly assembly, String fileName)`
- `Void Save()` [has Async]
- `Void CreateReferencesToolGroup()`

### `ComparisonOperator`
**Свойства:** Type: ComparisonOperatorType, SupportsSecondOperand: Boolean, RequireValueList: Boolean
**Методы:**
- `ComparisonOperator GetOperator(ComparisonOperatorType type)`
- `List`1 GetAllOperators()`
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `ComparisonRuleBase`
**Свойства:** Icon: IconImage, Key: String, Name: String, ReferencePath: String, Parent: ComparisonRuleBase, ChildrenRules: List`1
**Методы:**
- `Void Add(ComparisonRuleBase comparisonRule)`
- `Void Remove(ComparisonRuleBase comparisonRule)`
- `ComparisonRuleBase CreateShallowCopy()`
- `IObjectsComparisonNode Run(IObjectNode left, IObjectNode right)`

### `ComparisonRuleFactory`
**Методы:**
- `ComparisonRuleBase Create(ParameterInfo parameterInfo) (+1)`

### `ComparisonRulesRoot`
**Методы:**
- `IObjectsComparisonNode Run(IObjectNode left, IObjectNode right)`

### `CompilationResult`
**Свойства:** HasErrors: Boolean, HasWarnings: Boolean, IsClean: Boolean, Count: Int32, IsReadOnly: Boolean, Item: CompilationResultElement
**Методы:**
- `Void Add(CompilationResultElement item)`
- `Void Clear()`
- `Boolean Contains(CompilationResultElement item)`
- `Void CopyTo(CompilationResultElement[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`
- `Boolean Remove(CompilationResultElement item)`
- `Int32 IndexOf(CompilationResultElement item)`
- `Void Insert(Int32 index, CompilationResultElement item)`
- `Void RemoveAt(Int32 index)`

### `CompilationResultElement`
**Свойства:** Severity: CompilationResultElementSeverity, Line: Int32, Column: Int32, Number: String, CodeSource: String, IsMainSourceCode: Boolean, Text: String, IsWarning: Boolean, IsError: Boolean

### `ComplexHierarchyLink`
**Свойства:** ParameterValues: ParameterCollection, SystemFields: ComplexHierarchyLinkSystemFields, IsModified: Boolean, Reference: Reference, Id: Int32, Guid: Guid, ParentObject: ReferenceObject, ChildObject: ReferenceObject, ParentObjectId: Int32, ChildObjectId: Int32, RevisionsGroupId: Int32, IsAdded: Boolean, IsNew: Boolean, IsDeleted: Boolean, Prototype: ComplexHierarchyLink, SaveSet: ComplexHierarchyLinkSaveSet, CanEdit: Boolean, HasEditableStructure: Boolean, CanDelete: Boolean, SaveWith: ReferenceObject, Changing: Boolean, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, CanCheckOut: Boolean, CanCheckIn: Boolean, CanUndoCheckOut: Boolean, LockState: ReferenceObjectLockState, IsInRecycleBin: Boolean, IsPrimary: Boolean
**Методы:**
- `Boolean SetPrimary()`
- `Boolean SetRevisionsGroupId(Int32 revisionsGroupId)`
- `Void BeginChanges()` [has Async]
- `Boolean EndChanges(ReferenceObjectInstance sourceStructureInstance, ReferenceObjectInstance parentObjectInstance, ReferenceObjectInstance baseInstance) (+1)` [has Async]
- `Void CancelChanges()` [has Async]
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, Boolean throwOnError)`
- `Void UpdateRelevantParameters(ComplexHierarchyLink sourceHierarchyLink, CopyReferenceObjectsContext copyContext) (+1)`
- `Void UpdateFromLink(ComplexHierarchyLink sourceHierarchyLink, Boolean copyParameters, CopyReferenceObjectsContext copyContext, Boolean copyApplicability) (+1)`
- `ParameterGroup FindRelation(Guid groupGuid)`
- `Boolean ContainsRelation(Int32 groupId)`
- `ComplexHierarchyLink CreateCopy(ReferenceObject newParent, ReferenceObject newChild)`
- `Boolean BelongsToConfigurationSettings()`
- `String GetGroupingKey()`

### `ComplexHierarchyLinkExtensions`
**Методы:**
- `Void ModifyLink(TObject hierarchyLink, Action`1 action, Boolean cancelOnError)`
- `ComplexHierarchyLink CopyAllTo(ComplexHierarchyLink hierarchyLink, Reference target)`

### `ComplexHierarchyLinkExtensions`
**Методы:**
- `Boolean IsSubstituteInActiveDesignContext(ComplexHierarchyLink hierarchyLink)`
- `Boolean IsSubstituteInDesignContext(ComplexHierarchyLink hierarchyLink, DesignContextObject designContext)`
- `DesignContextChangeStatus GetDesignContextStatus(ComplexHierarchyLink hierarchyLink)`

### `ComplexHierarchyLinkInstanceData`
**Свойства:** HierarchyLink: ComplexHierarchyLink, SourceStructureObjectInstance: ReferenceObjectInstance, ParentObjectInstance: ReferenceObjectInstance, BaseInstance: ReferenceObjectInstance
**Методы:**
- `Boolean EndChanges()` [has Async]

### `ComplexHierarchyLinkInstancesSaveSet`
**Свойства:** Count: Int32
**Методы:**
- `Void AddRange(IEnumerable`1 hierarchyLinks) (+1)`
- `Void Clear()`
- `Boolean Remove(ComplexHierarchyLink item)`
- `Void CancelChanges()` [has Async]
- `Boolean EndChanges()` [has Async]
- `Void Add(ComplexHierarchyLink hierarchyLink) (+1)` [has Async]
- `Boolean Contains(ComplexHierarchyLink hierarchyLink)`
- `Void CopyTo(ComplexHierarchyLink[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `ComplexHierarchyLinkParameters`
**Свойства:** Link: ComplexHierarchyLink

### `ComplexHierarchyLinkSaveSet`
**Свойства:** Changing: Boolean, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Void AddRange(IEnumerable`1 hierarchyLinks)`
- `Void Clear()`
- `Boolean Remove(ComplexHierarchyLink item)`
- `Void CancelChanges()` [has Async]
- `Boolean EndChanges()` [has Async]
- `Void Add(ComplexHierarchyLink hierarchyLink)` [has Async]
- `Boolean Contains(ComplexHierarchyLink hierarchyLink)`
- `Void CopyTo(ComplexHierarchyLink[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `ComplexHierarchyLinkStructure`
**Свойства:** IsLinkOrParameterGroup: Boolean, Type: StructureGroupTypes
**Методы:**
- `String AppendToPath(String path, HierarchyDirections hierarchyDirection, String pathItem) (+1)`

### `ComplexHierarchyLinkSystemFields`
**Свойства:** IsModified: Boolean, Id: Int32, Guid: Guid, IsPrimary: Boolean, AuthorName: String, AuthorId: Int32, Author: User, CreationDate: DateTime, EditorName: String, EditorId: Int32, Editor: User, EditDate: DateTime, StartDate: Nullable`1, EndDate: Nullable`1, DesignContextId: Int32, OriginalId: Int32, DeletedInDesignContext: Boolean, ConflictWithOriginal: ConflictWithOriginal, AutoSelectRevision: Boolean, StructureTypeId: Int32, StructureType: StructureTypesReferenceObject

### `ComplexHierarchyLinkValue`
**Свойства:** IsHierarchyLink: Boolean, Link: ComplexHierarchyLink

### `ConfigurationCriteria`
**Свойства:** Class: ConfigurationCriteriaType, Name: StringParameter, DefaultValue: StringParameter, IsHidden: BooleanParameter, IsReadOnly: BooleanParameter, IsRequired: BooleanParameter, AllowManualInput: BooleanParameter
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`
- `Boolean DefaultValueIsNotNull()`
- `Object GetDefaultValue()` [has Async]
- `Void SetDefaultValue(Object value)` [has Async]

### `ConfigurationCriteriasReference`
**Свойства:** Classes: ConfigurationCriteriasTypes

### `ConfigurationCriteriasTypes`
**Свойства:** ConfigurationCriteria: ConfigurationCriteriaType, CustomCriteria: ConfigurationCriteriaType, SelectRevisionsFilterCriteria: ConfigurationCriteriaType, SystemCriteria: ConfigurationCriteriaType, ProductMilestoneCriteria: ConfigurationCriteriaType, DateCriteria: ConfigurationCriteriaType, ProductCriteria: ConfigurationCriteriaType, DesignContextCriteria: ConfigurationCriteriaType, ProductConfigurationCriteria: ConfigurationCriteriaType, OptionsCriteria: ConfigurationCriteriaType, SerialNumberCriteria: ConfigurationCriteriaType, StructureTypeCriteria: ConfigurationCriteriaType, CategoryTypeCriteria: ConfigurationCriteriaType, StructureVariantCriteria: ConfigurationCriteriaType

### `ConfigurationCriteriaType`
**Свойства:** Classes: ConfigurationCriteriasTypes, IsConfigurationCriteria: Boolean, IsCustomCriteria: Boolean, IsSelectRevisionsFilterCriteria: Boolean, IsSystemCriteria: Boolean, IsProductMilestoneCriteria: Boolean, IsDateCriteria: Boolean, IsProductCriteria: Boolean, IsDesignContextCriteria: Boolean, IsProductDesignNumberCriteria: Boolean, IsOptionsCriteria: Boolean, IsSerialNumberCriteria: Boolean, IsStructureTypeCriteria: Boolean, IsCategoryTypeCriteria: Boolean, IsStructureVariantCriteria: Boolean

### `ConfigurationFilterTerm`
**Свойства:** Name: StringParameter, ReferenceGroup: GuidParameter, LinkGroup: GuidParameter, Term: StringParameter

### `ConfigurationGroupPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `ConfigurationParameterExtensions`
**Методы:**
- `String GetName(ConfigurationParameter configurationItemType)`

### `ConfigurationParameterPathItem`
**Свойства:** Name: String, Type: PathItemType, Parameter: ConfigurationParameter

### `ConfigurationSettings`
**Свойства:** Connection: ServerConnection, TypicalConfiguration: TypicalConfigurationSettingsObject, ApplyProductFilter: Boolean, Product: ProductsClassifierReferenceObject, ApplyProductDesignNumber: Boolean, ApplyProductMilestoneNumber: Boolean, ProductDesignNumber: Nullable`1, ProductMilestoneNumber: Nullable`1, SerialNumber: ProductsInstancesReferenceObject, ApplyOptionValues: Boolean, OptionValues: List`1, ApplyDesignContext: Boolean, DesignContext: DesignContextObject, ActiveDesignContext: DesignContextObject, ShowDeletedInDesignContextLinks: Boolean, ApplyDate: Boolean, Date: Object, ApplyStructureType: Boolean, ActiveStructure: StructureTypesReferenceObject, ApplyStructureTypes: Boolean, ActiveStructures: StructureTypesData, VisibleStructures: IEnumerable`1, EditableStructures: IEnumerable`1, CustomCriteriaValues: List`1, SelectRevisionsFilterCriteriaValue: CustomCriteriaValue, FilterDate: Nullable`1, ApplyStructureVariants: Boolean, StructureVariants: StructureVariantFilterData, ApplyCategoriesFilter: Boolean, Categories: CategoriesFilterData, ApplyTerms: Boolean, SelectRevisionsTermsObject: ReferenceFiltersGroupObject, SelectRevisionsTerms: FilterDataCollection
**Методы:**
- `Boolean ValidateDesignContextEdit(Boolean throwOnError)`
- `Boolean ValidateDateEdit(Boolean throwOnError)`
- `Void AppendToFilter(Filter filter, ParameterGroup linkGroup)` [has Async]
- `Void AppendToInstanceFilter(Filter filter, ParameterGroup linkGroup, CancellationToken token)` [has Async]
- `List`1 GetExcludedByApplicabilityObjectIds(ParameterGroup referenceGroup, ApplicabilityGroupType applicabilityGroupType)` [has Async]

### `ConfigurationSettingsAccessor`
**Свойства:** ApplyProduct: Boolean [RU: ПрименитьИзделие], Product: RefObj, ApplyDesignContext: Boolean [RU: ПрименитьИзделие], DesignContext: RefObj, ApplyDate: Boolean [RU: ПрименитьИзделие], Date: Nullable`1 [RU: Дата], ActiveStructure: RefObj, VisibleStructures: RefObjList, EditableStructures: RefObjList, ApplyCategories: Boolean [RU: ПрименитьИзделие], ShowAllCategories: Boolean [RU: ПрименитьИзделие], ShowEmptyCategories: Boolean [RU: ПрименитьИзделие], Categories: RefObjList, ApplySelectRevisionsTerms: Boolean [RU: ПрименитьИзделие], SelectRevisionsTermsObject: RefObj, SelectRevisionsTerms: String [RU: УсловияВыбораРевизий], Изделие: Объект [RU only], КонтекстПроектирования: Объект [RU only], АктивныйТипСтруктуры: Объект [RU only], ОтображаемыеСтруктуры: Объекты [RU only], РедактируемыеСтруктуры: Объекты [RU only], Категории: Объекты [RU only], ОбъектУсловийВыбораРевизий: Объект [RU only]
**Методы:**
- `Void AddStructure(RefObj structure, Boolean editable)` [RU: ДобавитьСтруктуру]
- `Void RemoveStructure(RefObj structure)` [RU: УдалитьСтруктуру]
- `Void AddCategory(RefObj category)` [RU: УдалитьСтруктуру]
- `Void RemoveCategory(RefObj category)` [RU: УдалитьСтруктуру]
- `Void ДобавитьКатегорию(Объект category)` [RU alternative]
- `Void УдалитьКатегорию(Объект category)` [RU alternative]

### `ConfigurationSettingsContainer`
**Свойства:** ConfigurationSettings: ConfigurationSettings, Connection: ServerConnection, SupportsViews: Boolean, Interface: String, Application: String

### `ConfigurationSettingsData`
**Свойства:** TypicalConfiguration: Guid, Product: Guid, DesignContext: Guid, ApplyStructureType: Boolean, ActiveStructureTypeGuid: Guid, ActiveStructureTypes: List`1, DisplayStructureTypes: List`1, ShowBaseStructure: Boolean, StatusesDate: String, ShowEmptyCategories: Boolean, ShowAllCategories: Boolean, ApplyProductFilter: Boolean, ApplyCategoriesFilter: Boolean, ApplyTerms: Boolean, ApplyDate: Boolean, ApplyDesignContext: Boolean, ApplyOptionValues: Boolean, ShowDeletedInDesignContextLinks: Boolean, ApplyProductDesignNumber: Boolean, ApplyProductMilestoneNumber: Boolean, ApplyStructureVariants: Boolean, ProductCategories: List`1, SelectRevisionsTermsObject: Guid, SelectRevisionsTerms: FilterDataCollection, ProductMilestoneNumber: Int32, ProductDesignNumber: Int32, SerialNumberGuid: Guid, OptionValues: List`1, ConfiguratorGuid: Guid, StructureVariants: StructureVariantFilterData, CustomCriteriaValueData: CustomCriteriaValueData

### `ConfigurationSettingsDataExtension`
**Методы:**
- `ConfigurationSettings GetConfigurationSettings(ConfigurationSettingsData data, ServerConnection connection)` [has Async]
- `ConfigurationSettingsData GetConfigurationSettingsData(ConfigurationSettings configurationSettings, Configurator configurator)`

### `ConfigurationSettingsExtensions`
**Методы:**
- `Void SetToday(ConfigurationSettings settings)`

### `ConfigurationSettingsSerialization`
**Методы:**
- `String ToXml(ConfigurationSettings configurationSettings, Configurator configurator)`
- `ConfigurationSettings FromXml(ServerConnection connection, String data)` [has Async]
- `String ToJson(ConfigurationSettings configurationSettings, Configurator configurator)`
- `ConfigurationSettings FromJson(ServerConnection connection, String data)` [has Async]
- `Byte[] ToBson(ConfigurationSettings configurationSettings, Configurator configurator)`
- `ConfigurationSettings FromBson(ServerConnection connection, Byte[] data)` [has Async]

### `ConfigurationTerm`
**Свойства:** Class: ConfigurationTermType

### `ConfigurationTermsReference`
**Свойства:** Classes: ConfigurationTermsTypes

### `ConfigurationTermsTypes`
**Свойства:** ConfigurationTerms: ConfigurationTermType, FilterTerm: ConfigurationTermType

### `ConfigurationTermType`
**Свойства:** Classes: ConfigurationTermsTypes, IsConfigurationTerms: Boolean, IsFilterTerm: Boolean

### `ConfigurationVariable`
**Свойства:** Variable: Variable, VariableName: String, VariableType: Type, IsArray: Boolean, AllowNullValue: Boolean, IsNull: Boolean, ReferenceGuid: Guid, DefaultObjectValue: Object, PossibleObjectValues: IEnumerable`1, Class: ConfigurationVariableType, Alias: StringParameter, DefaultValue: StringParameter, Data: StringParameter, PossibleVariableValues: StringParameter

### `ConfigurationVariablesReference`
**Свойства:** Classes: ConfigurationVariablesTypes

### `ConfigurationVariablesTypes`
**Свойства:** ConfigurationVariable: ConfigurationVariableType

### `ConfigurationVariableType`
**Свойства:** Classes: ConfigurationVariablesTypes, IsConfigurationVariable: Boolean

### `Configurator`
**Свойства:** Class: ConfiguratorType, Name: StringParameter, Description: StringParameter, ConfigurationCriterias: ReferenceObjectCollection`1
**Методы:**
- `Void LoadCriterias()` [has Async]
- `ConfigurationSettings GetDefaultConfigurationSettings()` [has Async]
- `ConfigurationCriteria CreateConfigurationCriteria(Guid listObjectClass) (+1)`

### `ConfiguratorsReference`
**Свойства:** DefaultConfigurator: Configurator, Classes: ConfiguratorsTypes

### `ConfiguratorsTypes`
**Свойства:** Configurator: ConfiguratorType

### `ConfiguratorType`
**Свойства:** Classes: ConfiguratorsTypes, IsConfigurator: Boolean

### `ConformityInfo`
**Свойства:** MachingReferenceParameterGuid: String, DestinationParameterGuid: String

### `ConnectionInfo`
**Свойства:** ConnectionCount: Int32
**Методы:**
- `List`1 GetLockedLicenses()`
- `Boolean IsLocked(ModuleLicense license)`

### `ConnectionParameters`
**Свойства:** UserName: String, Password: MD5HashString, WindowsAuthentication: Boolean, AccessToken: String, OidcToken: String, OidcProvider: Guid, Server: String, Proxy: IWebProxy, ConfigurationGuid: Nullable`1, UseSessionLog: Boolean, Communication: CommunicationMode, Compression: CompressionAlgorithm, DataSerializer: DataSerializerAlgorithm, ServerVersion: Int32, Version: String
**Методы:**
- `String GetServerAddress()`
- `String GetServerInstance()`
- `String GetServerNameWithInstance()`
- `String Serialize()`
- `ConnectionParameters Deserialize(String data)`

### `Connector`
**Свойства:** IsActive: Boolean
**Методы:**
- `VariableCollection GetVariables()`

### `Connector2D`
**Свойства:** StartNode: Point2D, EndNode: Point2D
**Методы:**
- `Void Initialize(Point2D startNode, Point2D endNode)`
- `Double GetAngle()`

### `Connector2DData`
**Свойства:** StartNode: Point2DData, EndNode: Point2DData

### `Connector3D`
**Свойства:** LCS: LCS

### `Connector3DData`
**Свойства:** Lcs: LcsData

### `ConstraintExtensions`
**Методы:**
- `Void AddConstraint(Collection`1 constraints, DelegateInArgument`1 activityDelegate, T activity, Boolean isWarning, String messageText, Expression`1 expression, Boolean argumentMessage) (+2)`
- `Void AddParameter(Collection`1 constraints, T activity)`
- `Void AddAction(Collection`1 constraints, T activity)`
- `Void AddReference(Collection`1 constraints, T activity)`
- `Void AddReferenceObject(Collection`1 constraints, T activity)`
- `Void AddPrototype(Collection`1 constraints, T activity)`
- `Void AddClassObject(Collection`1 constraints, T activity)`
- `Void AddLink(Collection`1 constraints, T activity)`
- `Void AddObjectsList(Collection`1 constraints, T activity)`
- `Void AddFilter(Collection`1 constraints, T activity)`
- `Void AddSignatureType(Collection`1 constraints, T activity)`
- `Void AddOperator(Collection`1 constraints, T activity)`
- `Boolean AssertExpression(InArgument`1 argument)`

### `ConstraintReference`
**Свойства:** Classes: ConstraintTypes

### `ConstraintReferenceObject`
**Свойства:** Class: ConstraintType, Name: String, ConstraintFormula: String, LogicalId: Guid, ConditionFormula: String, Comment: String, TableSet: OptionsTableSetReferenceObject

### `ConstraintType`
**Свойства:** Classes: ConstraintTypes, IsConstraint: Boolean

### `ConstraintTypes`
**Свойства:** Constraint: ConstraintType

### `ContactReferenceObject`
**Свойства:** Class: ContactType, LastName: StringParameter, Name: StringParameter, MiddleName: StringParameter, Job: StringParameter, Title: StringParameter, FullName: StringParameter, Department: StringParameter, Sex: StringParameter, Birthday: DateTimeParameter, Family: StringParameter, SpouseName: StringParameter, Description: StringParameter, WorkPhone1: StringParameter, WorkPhone2: StringParameter, MobilePhone: StringParameter, HomePhone: StringParameter, Fax: StringParameter, Email: StringParameter, Web: StringParameter, Phone: StringParameter, Addressee: StringParameter, AddresseePhone: StringParameter, Address: StringParameter, MailIndex: StringParameter, FullAddress: StringParameter, OwnerID: Int32Parameter, ContactCity: ReferenceObject, ContactCustomerAgreements: ReferenceObjectCollection, ContactExecutorAgreements: ReferenceObjectCollection, ActionContact: ReferenceObjectCollection, CompanyContacts: ReferenceObject
**Методы:**
- `ReferenceObject BeginChanges(ClassObject newClass)` [has Async]
- `ReferenceObject AddContactCustomerAgreements(ReferenceObject newLinkedObject)`
- `Boolean RemoveContactCustomerAgreements(ReferenceObject linkedObject)`
- `ReferenceObject AddContactExecutorAgreements(ReferenceObject newLinkedObject)`
- `Boolean RemoveContactExecutorAgreements(ReferenceObject linkedObject)`
- `ReferenceObject AddActionContact(ReferenceObject newLinkedObject)`
- `Boolean RemoveActionContact(ReferenceObject linkedObject)`

### `ContactsReference`
**Свойства:** Classes: ContactsTypes

### `ContactsTypes`
**Свойства:** Contact: ContactType, PrivateContact: ContactType

### `ContactType`
**Свойства:** Classes: ContactsTypes, IsContact: Boolean, IsPrivateContact: Boolean

### `ContainsMailCategoryOperator`
**Свойства:** RequireValueList: Boolean
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `Context`
**Свойства:** Default: Boolean, ContextUniqueString: String
**Методы:**
- `Boolean BaseEquals(Context context)`

### `ContextVariableInfo`
**Свойства:** ActivityType: Type
**Методы:**
- `Object GetValue(ActivityContext context) (+1)`
- `Object GetAccessorValue(ActivityContext context) (+1)`

### `ContextVariables`
**Свойства:** Variables: ContextVariableInfo[]

### `ContextVariables`
**Свойства:** Variables: ContextVariableInfo[]

### `ControllerMailField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `ConversionFormatReference`
**Свойства:** Classes: ConversionFormatTypes

### `ConversionFormatReferenceObject`
**Свойства:** Class: ConversionFormatType, Name: StringParameter, SupportedFileTypes: StringParameter, Disable: BooleanParameter, Format: StringParameter

### `ConversionFormatType`
**Свойства:** Classes: ConversionFormatTypes, IsConversionFormatReferenceObject: Boolean

### `ConversionFormatTypes`
**Свойства:** ConversionFormatReferenceObject: ConversionFormatType

### `ConversionTaskExtension`
**Методы:**
- `Void UpdateConvertedFiles(ICollection`1 conversionTasks)`

### `ConversionTaskQueueReference`
**Свойства:** Classes: ConversionTaskQueueTypes
**Методы:**
- `Queue`1 GetConversionTaskQueue(TaskGroupReferenceObject taskGroupReferenceObject, Int32 maxCount) (+2)`
- `ICollection`1 GetActiveTaskGroups()`
- `TaskGroupReferenceObject AddTaskGroup(String name, FolderObject saveObject, ReferenceObject instanceConversionService) (+1)`

### `ConversionTaskQueueReferenceObject`
**Свойства:** Class: ConversionTaskQueueType, Name: StringParameter, Status: Int32Parameter, ConversionStatus: ConversionStatusType
**Методы:**
- `Void AddConvertedFile(FileReferenceObject file)`

### `ConversionTaskQueueType`
**Свойства:** Classes: ConversionTaskQueueTypes, IsTaskGroup: Boolean, IsConversionTask: Boolean, IsSecondaryRepresentationTask: Boolean

### `ConversionTaskQueueTypes`
**Свойства:** TaskGroup: ConversionTaskQueueType, ConversionTask: ConversionTaskQueueType, SecondaryRepresentationTask: ConversionTaskQueueType

### `ConversionTaskReferenceObject`
**Свойства:** ObjectESP: GuidParameter, ErrorText: StringParameter, ConversionConfigurationSettings: StringParameter, ConversionFormat: StringParameter, OutputFileName: StringParameter, AttachFilesToObject: BooleanParameter, ConversionModule: FileConversionModuleReferenceObject, SourceFile: ReferenceObject, ConversionParameters: ReferenceObject, ConversionFormatObject: ConversionFormatReferenceObject, PathPrototypeFile: StringParameter, ConvertedFiles: ReferenceObjectCollection
**Методы:**
- `Void SetConversionFormat(String format)`

### `Converter`
**Методы:**
- `String GetString(CheckStatusType type)`

### `Converter`
**Методы:**
- `ConvertResponse Convert(ConvertRequest request, Object context) (+2)`
- `String GetEmpty()`

### `ConvertRequest`
**Свойства:** Body: String, BodyType: MailBodyType, ToMailBodyType: MailBodyType
**Методы:**
- `Converter GetConverter()`
- `ConvertResponse Execute(Object context) (+1)`

### `ConvertResponse`
**Свойства:** Failed: ConvertResponse, IsSuccessed: Boolean, Body: String, BodyType: MailBodyType, ConvertException: Exception

### `CoordinatesReference`
**Свойства:** Classes: CoordinatesTypes

### `CoordinatesReferenceObject`
**Свойства:** X_MAX: DoubleParameter, X_MIN: DoubleParameter, Placement: StringParameter, Z_MIN: DoubleParameter, Y_MAX: DoubleParameter, Y_MIN: DoubleParameter, Z_MAX: DoubleParameter, StructureType: Int32Parameter

### `CoordinatesType`
**Свойства:** Classes: CoordinatesTypes, IsCoordinatesReferenceObject: Boolean

### `CoordinatesTypes`
**Свойства:** CoordinatesReferenceObject: CoordinatesType

### `CopyReferenceObjectsContext`
**Свойства:** ParentObject: ReferenceObject, CopyChildren: Boolean, ReloadSourceChildren: Boolean, CopyLinkedPrototypes: Boolean, LinkPermanentCharacteristicsOnCopy: Boolean, NomenclatureHierarchyLink: NomenclatureHierarchyLink, Parameters: Dictionary`2
**Методы:**
- `Boolean SkipCopy(ParameterInfo info) (+1)`
- `Void RaiseProcess(String message, Object[] args)`

### `CopySetAccessor`
**Свойства:** Count: Int32, Changing: Boolean [RU: Редактируется], Owner: RefObj, Владелец: Объект [RU only]
**Методы:**
- `Void CopyTo(ObjectAccessor[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()` [RU: Сохранить]
- `RefObj GetCopy(ObjectAccessor prototype)` [RU: ПолучитьКопию]
- `Boolean Save()` [RU: Сохранить]
- `Void CancelChanges()` [RU: Сохранить]
- `Boolean Contains(ObjectAccessor refObj)` [RU: ПолучитьКопию]
- `Void ОтменитьИзменения()` [RU alternative]
- `Boolean Содержит(ObjectAccessor объект)` [RU alternative]

### `CounterElementReferenceObject`
**Свойства:** IsNullable: BooleanParameter, NullableConditions: Int32Parameter, MaxCounterValue: Int32Parameter, StartWith: Int32Parameter, Step: Int32Parameter, PositionCount: Int32Parameter, RestartDay: Int32Parameter, RestartMonth: Int32Parameter, CounterSelectionRule: StringParameter
**Методы:**
- `String GetTestValue(String parameter)`
- `String GetRegexTemplate(ReferenceObject referenceObject)`

### `CountOfItemsInCollectionActivity`1`
**Свойства:** Values: InArgument`1

### `CredentialPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `CredentialsReference`
**Свойства:** Classes: CredentialsTypes

### `CredentialsReferenceObject`
**Свойства:** Class: CredentialsType, Name: StringParameter, IsEnabled: BooleanParameter, CredentialTenants: ReferenceObjectCollection`1, CredentialTargets: ReferenceObjectCollection`1, CredentialBusinessProcess: ReferenceObjectCollection, CredentialOwnerUsers: ReferenceObjectCollection`1
**Методы:**
- `CredentialsTenantListObject CreateCredentialTenants(Guid listObjectClass) (+1)`
- `CredentialsTargetListObject CreateCredentialTargets(Guid listObjectClass) (+1)`
- `ReferenceObject AddCredentialBusinessProcess(ReferenceObject newLinkedObject)`
- `Boolean RemoveCredentialBusinessProcess(ReferenceObject linkedObject)`
- `ReferenceObject AddCredentialOwnerUsers(UserReferenceObject newLinkedObject)`
- `Boolean RemoveCredentialOwnerUsers(UserReferenceObject linkedObject)`

### `CredentialsTargetList`
**Свойства:** Classes: CredentialsTargetTypes

### `CredentialsTargetListObject`
**Свойства:** Class: CredentialsTargetType, Name: StringParameter, ItemGuid: GuidParameter, ItemStringId: StringParameter, AccessGroupGuid: GuidParameter, IsEnabled: BooleanParameter, AccessRightPK: Int32Parameter, CredentialOwner: GuidParameter, Objects: AnyReferenceLink
**Методы:**
- `ReferenceObject AddObject(ReferenceObject newLinkedObject)`
- `Boolean RemoveObject(ReferenceObject linkedObject)`

### `CredentialsTargetType`
**Свойства:** Classes: CredentialsTargetTypes, IsCredentialsTargetListObject: Boolean

### `CredentialsTargetTypes`
**Свойства:** CredentialsTargetListObject: CredentialsTargetType

### `CredentialsTenantList`
**Свойства:** Classes: CredentialsTenantListTypes

### `CredentialsTenantListObject`
**Свойства:** Class: CredentialsTenantListType, StartDate: DateTimeParameter, EndDate: DateTimeParameter, Name: StringParameter, TenantUser: UserReferenceObject

### `CredentialsTenantListType`
**Свойства:** Classes: CredentialsTenantListTypes, IsCredentialsTenantListObject: Boolean

### `CredentialsTenantListTypes`
**Свойства:** CredentialsTenantListObject: CredentialsTenantListType

### `CredentialsType`
**Свойства:** Classes: CredentialsTypes, IsCredentialType: Boolean

### `CredentialsTypes`
**Свойства:** CredentialType: CredentialsType

### `CriteriaValueSerializeManager`
**Методы:**
- `Object Deserialize(ConfigurationCriteria criteria, String valueString)`
- `String Serialize(ConfigurationCriteria criteria, Object value)`
- `Boolean IsSerializedValueValid(ConfigurationCriteria criteria, String valueString)`

### `CurrentDateElementReferenceObject`
**Свойства:** Format: StringParameter
**Методы:**
- `String GetTestValue(String parameter)`

### `CurrentStateChangeEventTypeAccessor`
**Свойства:** Add: CurrentStateChangeEventTypeObj, Move: CurrentStateChangeEventTypeObj, Delete: CurrentStateChangeEventTypeObj, Перенос: ТипИзмененияТекущегоСостояния [RU only], Удаление: ТипИзмененияТекущегоСостояния [RU only], Добавление: ТипИзмененияТекущегоСостояния [RU only]
**Методы:**
- `Object GetRealValue()`

### `CustomComparisonOperator`
**Свойства:** Type: ComparisonOperatorType

### `CustomCriteria`
**Свойства:** PossibleValues: ReferenceObjectCollection`1, Code: StringParameter
**Методы:**
- `Void CopyDefaultValue(CustomCriteria source)`
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`
- `PossibleValue AddPossibleValue(Guid listObjectClass) (+1)`

### `CustomCriteriaValue`
**Свойства:** Criteria: CustomCriteria, Apply: Boolean, Value: PossibleValue, VariableValues: Dictionary`2
**Методы:**
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `CustomCriteriaValueData`
**Свойства:** CustomCriteriaValues: List`1, SelectRevisionsFilterCriteriaValue: CustomCriteriaValue
**Методы:**
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `CustomUndoBlock`
**Свойства:** Name: String, AllowAddAction: Boolean
**Методы:**
- `Boolean CanClose()`

### `DailyObject`
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `DataExchangeAccess`
**Свойства:** AccessId: Int32, UserId: Int32, ObjectId: Int32

### `DataExchangeAccessFilter`
**Свойства:** UserId: Int32, FilterXml: String

### `DataExchangeAccessGroup`
**Свойства:** TypeId: Int32, SystemType: SystemObjectType, AllowedCommands: ReadOnlyCollection`1, ForbiddenCommands: ReadOnlyCollection`1, References: ReadOnlyCollection`1, Objects: ReadOnlyCollection`1, Stages: ReadOnlyCollection`1, Links: ReadOnlyCollection`1

### `DataExchangeAccessor`
**Методы:**
- `DataExchangeResultsAccessor Import(String ruleName, String reference, String filter, RefObj rootObject, Boolean onlyChildrenObjects, String filePath, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Int32 count, Int32 offset, IReadOnlyCollection`1 sortFields, Boolean deleting, Boolean usePackage, Boolean allowProcessingList, Boolean showWaitingDialog, String connectionString, String intermediateConnectionString, Boolean clearTransformTables)` [RU: Импортировать]
- `DataExchangeResultsAccessor ImportFromCatalog(String ruleName, String catalogFolder, String reference, String filePath, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Int32 count, Int32 offset, IReadOnlyCollection`1 sortFields, Boolean deleting, Boolean usePackage, Boolean allowProcessingList, Boolean showWaitingDialog, String connectionString)` [RU: ИмпортироватьИзКаталога]
- `DataExchangeResultsAccessor ImportObject(String ruleName, Object refObject, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Boolean deleting, Boolean allowProcessingList, Boolean reloadObjects, Boolean showWaitingDialog, String connectionString) (+2)` [RU: ИмпортироватьОбъект]
- `DataExchangeResultsAccessor ImportObjects(String ruleName, IEnumerable`1 refObjects, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Boolean deleting, Boolean allowProcessingList, Boolean reloadObjects, Boolean showWaitingDialog, String connectionString) (+2)` [RU: ИмпортироватьОбъект]
- `DataExchangeResultsAccessor Export(String ruleName, String reference, String filter, RefObj rootObject, Boolean onlyChildrenObjects, String filePath, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Int32 count, Int32 offset, IReadOnlyCollection`1 sortFields, Boolean deleting, String server, Boolean usePackage, Boolean allowProcessingList, Boolean showWaitingDialog, Dictionary`2 transferData, String connectionString, Boolean onlyStructure)` [RU: Экспортировать]
- `DataExchangeResultsAccessor ExportFromCatalog(String ruleName, String catalogFolder, String reference, String filePath, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, RefObjList attachToObjects, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Int32 count, Int32 offset, IReadOnlyCollection`1 sortFields, Boolean deleting, String server, Boolean usePackage, Boolean allowProcessingList, Boolean showWaitingDialog, Dictionary`2 transferData, String connectionString, Boolean onlyStructure)` [RU: ЭкспортироватьИзКаталога]
- `DataExchangeResultsAccessor ExportObject(String ruleName, Object refObject, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, String filePath, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Boolean deleting, String server, Boolean usePackage, Boolean allowProcessingList, Boolean reloadObjects, Boolean showWaitingDialog, Dictionary`2 transferData, String connectionString, Boolean onlyStructure) (+2)` [RU: ЭкспортироватьОбъект]
- `DataExchangeResultsAccessor ExportObjects(String ruleName, IEnumerable`1 refObjects, Boolean showDialog, Dictionary`2 extendedProperties, Boolean advancedLogging, String filePath, Nullable`1 readPacketSize, Nullable`1 writePacketSize, String referenceRule, Boolean deleting, String server, Boolean usePackage, Boolean allowProcessingList, Boolean reloadObjects, Boolean showWaitingDialog, Dictionary`2 transferData, String connectionString, Boolean onlyStructure) (+2)` [RU: ЭкспортироватьОбъект]
- `DataTransferResultsAccessor RunDataTransfer(RefObj dataTransferObject, Dictionary`2 extendedProperties, Boolean allowProcessingList) (+1)` [RU: ЗапуститьПередачуДанных]
- `MasterServerMacroProvider ConnectToServer(String server)` [RU: ПодключитьсяКСерверу]
- `DataExchangeResultsAccessor ИмпортироватьОбъекты(String наименованиеПравила, IEnumerable`1 объекты, Boolean показыватьДиалог, Dictionary`2 дополнительныеДанные, Boolean расширенноеЖурналирование, Объекты подключатьКОбъектам, Nullable`1 размерПакетаЧтения, Nullable`1 размерПакетаЗаписи, String правилоСправочника, Boolean удаление, Boolean ведениеСпискаОбработанныхОбъектов, Boolean перезагружатьОбъекты, Boolean показыватьДиалогОжидания, String строкаПодключения)` [RU alternative]
- `DataExchangeResultsAccessor ЭкспортироватьОбъекты(String наименованиеПравила, IEnumerable`1 объекты, Boolean показыватьДиалог, Dictionary`2 дополнительныеДанные, Boolean расширенноеЖурналирование, String путьКФайлу, Nullable`1 размерПакетаЧтения, Nullable`1 размерПакетаЗаписи, String правилоСправочника, Boolean удаление, String сервер, Boolean архивировать, Boolean ведениеСпискаОбработанныхОбъектов, Boolean перезагружатьОбъекты, Boolean показыватьДиалогОжидания, Dictionary`2 передаваемыеДанные, String строкаПодключения, Boolean толькоСтруктура)` [RU alternative]

### `DataExchangeAliasedParameterInfo`
**Свойства:** Alias: DataExchangeExtendedParameterReferenceLink, MasterAttributeId: Int32, MasterAttributeGuid: Guid, ClassId: Int32

### `DataExchangeApplication`
**Свойства:** Description: String, EventServiceApplication: Boolean, FileObjectId: Guid, Configurations: ReadOnlyCollection`1, ConfigurationUseType: ConfigurationUseType

### `DataExchangeCatalog`
**Свойства:** Folders: ReadOnlyCollection`1, Users: ReadOnlyCollection`1, UsersUseType: ItemListUseType

### `DataExchangeCatalogFolder`
**Свойства:** ParentId: Int32, Type: String, Icon: Byte[], CustomIcon: Boolean, Properties: String, Objects: ReadOnlyCollection`1, Filter: String, ParameterSearchFolder: String

### `DataExchangeClasses`
**Свойства:** Classes: ReadOnlyCollection`1, GroupSettings: ReadOnlyCollection`1, ExternalParameterGroups: ReadOnlyDictionary`2, ExternalParameters: ReadOnlyDictionary`2, ExternalClasses: ReadOnlyDictionary`2, ClassesKeys: ReadOnlyDictionary`2, SlaveGroupsClasses: ReadOnlyCollection`1
**Методы:**
- `Guid GetClass(Int32 classId) (+1)`

### `DataExchangeClassGroupSettings`
**Свойства:** Guid: Guid, ClassId: Int32, GroupId: Int32, Data: String

### `DataExchangeClassObject`
**Свойства:** Description: String, BaseClassId: Int32, Icon: Byte[], GroupId: Int32, SystemType: SystemObjectType, PropertiesDisplayType: PropertiesDisplayType, UniqueIndexId: Int32, SchemeId: Int32, DefaultStageId: Int32, LinkedClassId: Int32, CanChange: String, ParameterGroups: ReadOnlyCollection`1, ChildObjectClasses: ReadOnlyCollection`1, MasterObjectClasses: ReadOnlyCollection`1, SigningParametersData: String, ObjectFormat: String, ShowChangeCommandInObjectProperties: Nullable`1, SwappedToSelfParameterGroups: ReadOnlyCollection`1, CanCreateInRoot: Boolean, UseBaseClassIcon: Boolean, Sealed: Boolean, Abstract: Boolean, CreateFromPrototype: Boolean, SupportsSaveAndCreate: Boolean, Attributes: String, SupportMultiAttachment: Boolean, InheritMasterObjectClasses: Boolean, IsStandaloneProductByDefault: Boolean, Hidden: Boolean

### `DataExchangeDesktopObject`
**Свойства:** Parameters: ReadOnlyCollection`1, Links: ReadOnlyDictionary`2, AnyReferenceLinks: ReadOnlyDictionary`2, HasLinks: Boolean

### `DataExchangeDialog`
**Свойства:** Comment: String, GroupId: Int32, ClassId: Int32, Dockable: Boolean, EditObjectListInPropertyPanel: Boolean, Groups: ReadOnlyCollection`1, LinkDialogs: ReadOnlyCollection`1, IsWeb: Boolean

### `DataExchangeDialogData`
**Свойства:** Dialogs: ReadOnlyCollection`1, Pages: ReadOnlyCollection`1

### `DataExchangeDialogGroup`
**Свойства:** Comment: String, Icon: Byte[], DialogId: Int32, DialogPages: ReadOnlyCollection`1, GeneratedForGroupId: Int32

### `DataExchangeDialogPage`
**Свойства:** Comment: String, GroupId: Int32, ClassId: Int32, Type: DialogPageType, Icon: Byte[], Assembly: String, ClassName: String, UsedInPanel: Boolean, UsedInDialog: Boolean, Hidden: Boolean, UsedInClient: DialogPageClient, GeneratedForGroupId: Int32, DialogType: String, IsWeb: Boolean, Users: ReadOnlyCollection`1, AccessType: DialogPageAccessType, Configurations: ReadOnlyCollection`1, ConfigurationUseType: ConfigurationUseType, FilterData: String, Data: Byte[], XmlData: String

### `DataExchangeExtendedParameterInfo`
**Свойства:** ExtendedOptions: ExtendedParameterInfoOptions, Aliases: ReadOnlyCollection`1, ValuesStorageId: Int32

### `DataExchangeExtendedParameterReferenceLink`
**Свойства:** ParameterId: Int32, ParameterGuid: Guid, GroupId: Int32, GroupGuid: Guid, ClassId: Int32, ClassGuid: Guid, Alias: String, Comment: String

### `DataExchangeExternalLinkedObject`
**Свойства:** Id: Int32, Guid: Guid, Path: String

### `DataExchangeExternalLinkedObjects`
**Свойства:** Objects: ReadOnlyCollection`1

### `DataExchangeExternalObjects`
**Свойства:** ExternalLinkedGroups: ReadOnlyDictionary`2, ExternalLinkedParameters: ReadOnlyDictionary`2, ExternalLinkedClasses: ReadOnlyDictionary`2

### `DataExchangeFile`
**Свойства:** Product: String, ProductVersion: Version, SchemaVersion: Int32, Mode: ExportMode, StructureIdentify: Boolean, Schemes: ReadOnlyCollection`1, Stages: ReadOnlyCollection`1, StageAccesses: ReadOnlyCollection`1, References: ReadOnlyCollection`1, Classes: ReadOnlyCollection`1, Objects: ReadOnlyCollection`1, ExternalLinkedObjects: ReadOnlyCollection`1, ReferenceDialogs: ReadOnlyCollection`1, ReferenceSettings: ReadOnlyCollection`1, ReferenceCatalogs: ReadOnlyCollection`1, AccessGroups: ReadOnlyDictionary`2, UserAccessGroups: ReadOnlyCollection`1, UserGroups: ReadOnlyDictionary`2, ReferencesAccesses: ReadOnlyCollection`1, ReferenceGroupSettings: ReadOnlyCollection`1, Applications: ReadOnlyCollection`1
**Методы:**
- `Guid GetParameterGroup(Int32 parameterGroupId)`
- `Stream GetFileStream(DataExchangeObject dataExchangeObject)`

### `DataExchangeGateway`
**Методы:**
- `Void Export(ExportReferenceSettings referenceSettings, ExportObjectsSettings objectSettings, ExportOptions options, IReadOnlyList`1 additionalSettings) (+13)` [has Async]
- `Void Import(ServerConnection connection, ImportReferenceSettings settings, ImportOptions options) (+3)` [has Async]
- `DataExchangeFile Read(Stream stream, CancellationToken token)`
- `Stream ReadData(Stream stream, CancellationToken token)`

### `DataExchangeHierarchyLink`
**Свойства:** ParentId: Int32, ChildId: Int32, StructureTypes: ReadOnlyCollection`1

### `DataExchangeIndex`
**Свойства:** GroupId: Int32, UniqueKey: Boolean, Parameters: ReadOnlyCollection`1

### `DataExchangeIndexParameter`
**Свойства:** Id: Int32, CheckDefaultValue: Boolean

### `DataExchangeInstancesGroupInfo`
**Свойства:** MasterReferenceId: Int32, InstancesReferenceId: Int32, LinkToObjectId: Int32, LinkToHierarchyId: Int32, InstanceMainClassId: Int32

### `DataExchangeKeyObject`
**Свойства:** Id: Int32, Guid: Guid

### `DataExchangeNameObject`
**Свойства:** Name: String

### `DataExchangeNomenclatureClassObject`
**Свойства:** ReferenceId: Int32, ReferenceClassId: Int32, LinkedInheritClasses: Boolean, Rules: List`1

### `DataExchangeNomenclatureRule`
**Свойства:** ReferenceParameterId: Int32, NomenclatureParameterId: Int32

### `DataExchangeObject`
**Свойства:** GroupId: Int32, LinkedObjects: ReadOnlyDictionary`2, Signatures: ReadOnlyCollection`1, IsPrototype: Boolean, SystemType: SystemObjectType, ApplicabilityConditions: String, InstanceObjectHierarchyLinksPath: ReadOnlyCollection`1

### `DataExchangeObjectExtensions`
**Методы:**
- `IconImage GetIconImage(IDataExchangeObjectWithIcon dataExchangeObject)`

### `DataExchangeObjects`
**Свойства:** Objects: ReadOnlyCollection`1, HierarchyLinks: ReadOnlyCollection`1
**Методы:**
- `DataExchangeObject GetObject(Int32 objectId)`

### `DataExchangeParameter`
**Свойства:** Id: Int32, Type: Type
**Методы:**
- `Object GetValue()`

### `DataExchangeParameter`1`
**Свойства:** Type: Type, Value: T
**Методы:**
- `Object GetValue()`

### `DataExchangeParameterGroup`
**Свойства:** Parameters: ReadOnlyCollection`1, Indexes: ReadOnlyCollection`1, TableName: String, LogData: Boolean, SupportsRevisions: Boolean, SupportsExtendedParameters: Boolean, Caption: String, MasterGroupId: Int32, SlaveGroupId: Int32, GroupType: ParameterGroupType, Visibility: ParameterGroupVisibility, Icon: Byte[], Description: String, DefaultParameterId: Int32, HierarchyType: ReferenceHierarchyType, SupportsClasses: Boolean, SupportsDesktop: Boolean, SupportsRecycleBin: Boolean, SupportsSystemObjects: Boolean, CheckAccess: Int32, SupportsEncryption: Boolean, SupportsPrototype: Boolean, LinkType: LinkType, LinkVisibility: LinkVisibility, SupportsOrder: Boolean, SupportsMandatoryAccess: Boolean, SupportsOwner: Boolean, SystemType: SystemObjectType, SupportsSignature: Boolean, UseAllSignatureTypes: Boolean, SignatureTypes: ReadOnlyCollection`1, SigningParametersData: String, PrivateFolderPrototypeId: Int32, SupportsStages: Boolean, UniqueIndexId: Int32, SchemeId: Int32, DefaultStageId: Int32, EventHandlers: ReadOnlyCollection`1, UserEvents: ReadOnlyCollection`1, DoubleDirectionLink: Boolean, UserControl: String, AuthorAccessGroup: String, SelectionPath: String, CanChangeClass: Boolean, SupportsConfigurationSettings: Boolean, SupportsDesignContexts: Boolean, SupportsActivityDates: Boolean, SupportsApplicability: Boolean, SupportsSubstitutesInContext: Boolean, SearchQueryLinkFilter: String, SearchQueryLinkPathToFilter: String, SupportsObjectsInstances: Boolean, ObjectsInstances: DataExchangeInstancesGroupInfo, IsObjectsInstancesImpl: Boolean, Configurator: Guid, TableNameGenerated: Boolean, DefaultAccessLevel: Int32, ObjectFormat: String, RevisionNamingRule: String, LinkRequired: LinkRequired, IsAsymmetricLink: Boolean

### `DataExchangeParameterGroupEvent`
**Свойства:** GroupId: Int32, ButtonData: String

### `DataExchangeParameterInfo`
**Свойства:** GroupId: Int32, FieldName: String, ParameterType: ParameterType, Caption: String, Comment: String, IsRequired: Boolean, DefaultValue: String, IsVisible: Boolean, Nullable: Boolean, EditType: ParameterEditType, Length: Int32, Format: String, IsIndexed: Boolean, IsFullTextSearchEnabled: Boolean, ActivityStatus: ParameterActivityStatus, UnitId: Int32, UnitGuid: Guid, ListType: String, ListValues: ReadOnlyCollection`1, NomenclatureParameterID: Int32, SystemType: SystemObjectType, CalculationType: String, UserControl: String, RangeInfo: String, State: String, CertificateGuid: Guid, NormalizedFieldName: String

### `DataExchangeParameterListValue`
**Свойства:** Guid: Guid, Name: String, Value: String, Icon: Byte[]

### `DataExchangeReference`
**Свойства:** CatalogFolders: ReadOnlyCollection`1, ParameterGroups: ReadOnlyCollection`1, ParameterGroupKeys: ReadOnlyDictionary`2, ParameterKeys: ReadOnlyDictionary`2, SignatureTypeKeys: ReadOnlyDictionary`2, StageKeys: ReadOnlyDictionary`2
**Методы:**
- `Guid GetParameter(Int32 parameterId) (+1)`
- `Guid GetParameterGroup(Int32 parameterGroupId) (+1)`

### `DataExchangeReferenceAccesses`
**Свойства:** Accesses: ReadOnlyCollection`1, AccessFilters: ReadOnlyCollection`1

### `DataExchangeReferenceCatalogs`
**Свойства:** Catalogs: ReadOnlyCollection`1

### `DataExchangeReferenceDialogs`
**Свойства:** DialogData: ReadOnlyCollection`1

### `DataExchangeReferenceGroupSettings`
**Свойства:** GroupSettings: ReadOnlyCollection`1

### `DataExchangeReferenceHeader`
**Свойства:** File: DataExchangeFile, Guid: Guid, Caption: String, Description: String

### `DataExchangeReferenceSettings`
**Свойства:** Settings: ReadOnlyCollection`1

### `DataExchangeResultsAccessor`
**Свойства:** Cancelled: Boolean [RU: Отменён], HasErrors: Boolean [RU: Отменён], HasWarnings: Boolean [RU: Отменён], ErrorMessage: String [RU: ТекстОшибки], StartTime: DateTime [RU: ВремяНачала], EndTime: DateTime [RU: ВремяНачала], Duration: TimeSpan [RU: Длительность], FilePath: String [RU: ТекстОшибки], File: RefObj, Stream: Stream [RU: ПотокДанных], Data: Object [RU: Данные], DataType: Type [RU: ТипДанных], Objects: RefObjList, DataTransferObjects: RefObjList, Файл: Объект [RU only], Объекты: Объекты [RU only], ПередаваемыеДанныеСервера: Объекты [RU only]
**Методы:**
- `TResult GetData()` [RU: ПолучитьДанные]
- `Void ThrowIfCancelled()` [RU: ПолучитьДанные]
- `String GetFullErrorMessage()` [RU: ПолучитьДанные]
- `Void Clear()` [RU: ПолучитьДанные]
- `Void ОшибкаЕслиОтменено()` [RU alternative]
- `String ПолучитьПолныйТекстОшибки()` [RU alternative]
- `Void Очистить()` [RU alternative]

### `DataExchangeRunSettings`
**Свойства:** Context: MacroContext, MacroProviderType: Type, Name: String, ReferenceRuleName: String, IsImport: Boolean, ReadPacketSize: Nullable`1, WritePacketSize: Nullable`1, ShowDialog: Boolean, AdvancedLogging: Boolean, FilePath: String, UsePackage: Boolean, ReferenceName: String, FilterString: String, RootObject: ReferenceObject, OnlyChildrenObjects: Boolean, Count: Int32, Offset: Int32, SortFields: IReadOnlyCollection`1, Objects: IReadOnlyCollection`1, CatalogFolder: String, ExtendedProperties: Dictionary`2, AttachToObjects: IReadOnlyCollection`1, ShowSettingsDialog: Func`3, GetReference: Func`2, Deleting: Boolean, Server: String, AllowProcessingList: Boolean, ReloadObjects: Boolean, ShowWaitingDialog: Boolean, TransferData: Dictionary`2, ConnectionString: String, OnlyStructure: Boolean, IntermediateConnectionString: String, ClearTransformTables: Boolean

### `DataExchangeSchemeStages`
**Свойства:** Comment: String, StageIds: ReadOnlyCollection`1, Transitions: ReadOnlyCollection`1

### `DataExchangeSchemeTransition`
**Свойства:** FromStageId: Int32, ToStageId: Int32, Automatic: Boolean, Manual: Boolean

### `DataExchangeSettings`
**Свойства:** Guid: Guid, Name: String, IsView: Boolean, GroupId: Int32, ObjectId: Int32, Application: String, Interface: String, Context: String, Configurations: ReadOnlyCollection`1, ConfigurationUseType: ConfigurationUseType, DefaultConfigurations: ReadOnlyCollection`1, FolderGuid: Guid, Data: String, AccessType: SettingsViewAccessType, Users: ReadOnlyCollection`1

### `DataExchangeSignature`
**Свойства:** Key: Int32, TypeId: Int32, Date: DateTime, UserId: Int32, State: SignatureState, Resolution: String, Actual: Boolean, DigitalSignature: Byte[], SignedParameters: String, OnBehalfOf: Int32, CredentialId: Int32

### `DataExchangeSignatureType`
**Свойства:** Description: String

### `DataExchangeStage`
**Свойства:** Comment: String

### `DataExchangeStageAccessGroup`
**Свойства:** StageId: Int32, AccessGroupGuid: Guid, UserGuid: Guid

### `DataModelItemReferenceObject`
**Свойства:** Relation: StringParameter, ReferenceGuid: GuidParameter, LoadToCAD: BooleanParameter, Class: DataModelsType, IsReference: Boolean, IsRelation: Boolean, DisplayName: StringParameter
**Методы:**
- `ReferencePath GetReferencePath()`

### `DataModelObject`
**Свойства:** IsDefault: BooleanParameter

### `DataModelReferenceObject`
**Свойства:** Name: StringParameter, Class: DataModelsType

### `DataModelsReference`
**Свойства:** Classes: DataModelTypes
**Методы:**
- `ReferenceObjectCollection GetDefaultReferenceDataModelsCollection(Guid reference)` [has Async]

### `DataModelsType`
**Свойства:** Classes: DataModelTypes, IsRelation: Boolean, IsReference: Boolean, IsDataModel: Boolean

### `DataModelTypes`
**Свойства:** Relation: DataModelsType, Reference: DataModelsType, DataModel: DataModelsType

### `DataTransferResultsAccessor`
**Свойства:** HasErrors: Boolean [RU: ИмеютсяОшибки], Objects: RefObjList, Объекты: Объекты [RU only]
**Методы:**
- `String GetFullErrorMessage()` [RU: ПолучитьПолныйТекстОшибки]

### `DataTransferRunSettings`
**Свойства:** Context: MacroContext, DataTransferObject: ReferenceObject, ExtendedProperties: Dictionary`2, AllowProcessingList: Boolean

### `DateCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `DateFieldInputDialog`
**Свойства:** TypeName: String

### `DateTimeBaseFieldInputDialog`
**Свойства:** DefaultValue: InArgument`1

### `DateTimeFieldInputDialog`
**Свойства:** TypeName: String, Mask: InArgument`1

### `DateTimeOperator`
**Методы:**
- `Nullable`1 GetDateTimeMaskMode(ComparisonOperator comparisonOperator)`
- `Boolean IsSpecialDateTimeOperator(ComparisonOperator comparisonOperator)`

### `DateTimeParameter`
**Свойства:** IsEmpty: Boolean
**Методы:**
- `DateTime GetDateTime()`
- `TypeCode GetTypeCode()`

### `DateTimeParameterOffsetExtensions`
**Методы:**
- `String GetDisplayText(DateTimeParameterOffset value, String nullText)`
- `String GetDateUnitString(Double unitValue, String singular, String plural, String genitive)`

### `DateWorkingTime`
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `DayTrigger`
**Свойства:** DayInterval: Int32, Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `DecimalParameter`
**Методы:**
- `Decimal GetDecimal()`
- `TypeCode GetTypeCode()`

### `DefaultNewObjectFolderAttribute`
**Свойства:** IsInherit: Boolean, FolderIsMacro: Boolean, Macro: String, ShowFolderDialog: Boolean, DefaultFolderKey: Guid, CreateUserSubfolder: Boolean, ForbidSelectionFromOtherFolders: Boolean, IsSystem: Boolean, CanSerialize: Boolean, CanChangeCaption: Boolean, Caption: String, Value: Object, CanRemove: Boolean
**Методы:**
- `ReferenceObject FindDefaultParent(Reference reference)` [has Async]

### `DefaultVisibleParameterColumnData`
**Свойства:** DisplayMask: String, Type: ColumnDataType, IsEmpty: Boolean
**Методы:**
- `ReferencePath GetParameterPath(ParameterGroup parameterGroup)`

### `DependenciesOfRemarksReference`
**Свойства:** Classes: DependencyOfRemarkTypes
**Методы:**
- `List`1 FindDependencies(ReferenceObject referenceObject) (+1)`

### `DependencyOfRemarkReferenceObject`
**Свойства:** Class: DependencyOfRemarkType, ReferenceGuid: GuidParameter, ReferenceObjectGuid: GuidParameter, ReferenceObjectVersion: Int32Parameter, Binary_Data: ByteArrayParameter, XML_Data: StringParameter, LinkToRemark: RemarkReferenceObject

### `DependencyOfRemarkType`
**Свойства:** Classes: DependencyOfRemarkTypes, IsDependenciesOfRemarks: Boolean

### `DependencyOfRemarkTypes`
**Свойства:** DependenciesOfRemarks: DependencyOfRemarkType

### `DeselectObjectCommand`
**Свойства:** Objects: List`1, DelelectAll: Boolean
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `DesignContextCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `DesignContextObject`
**Свойства:** IsMain: Boolean, Class: DesignContextsType, Name: StringParameter, IsDefaultForUser: GuidParameter
**Методы:**
- `Boolean ValidateEditByCurrentUser(Boolean throwOnError)`
- `IReadOnlyCollection`1 Substitute(IEnumerable`1 referenceObjects, Boolean delete, ReferenceObject parent) (+3)` [has Async]
- `Void MoveChanges(ComplexHierarchyLink hierarchyLink) (+3)` [has Async]
- `Void CopyChanges(ComplexHierarchyLink hierarchyLink) (+3)` [has Async]
- `Void CopyMoveChanges(Dictionary`2 links) (+1)` [has Async]
- `Void DeleteChanges(ComplexHierarchyLink hierarchyLink) (+3)` [has Async]
- `Void ConfirmConflictChanges(IReadOnlyCollection`1 hierarchyLinks) (+1)` [has Async]
- `List`1 GetLinksFromMainContext(IReadOnlyCollection`1 links, Boolean copyToOriginalReference)` [has Async]
- `List`1 GetOriginals(IReadOnlyCollection`1 links, Boolean copyToOriginalReference) (+1)` [has Async]
- `List`1 GetObjectsFromMainContext(IEnumerable`1 referenceObjects, Boolean loadChildren)` [has Async]
- `Dictionary`2 GetObjectsWithChangedApplicability(IEnumerable`1 referenceObjects)` [has Async]
- `Dictionary`2 GetLinksWithChangedApplicability(IEnumerable`1 hierarchyLinks)` [has Async]
- `Void ApplyDesignContextChanges(IReadOnlyCollection`1 changes) (+1)` [has Async]
- `Boolean ValidateParentObject(ReferenceObject parent, ClassObject classObject, Boolean throwOnError)`

### `DesignContextsReference`
**Свойства:** MainContext: DesignContextObject, Classes: DesignContextsTypes, IsDefaultForUserParameterInfo: ParameterInfo
**Методы:**
- `DesignContextObject Find(String name)` [has Async]
- `DesignContextObject FindDefaultDesignContext(User user) (+1)` [has Async]
- `List`1 FindDefaultDesignContexts(User user) (+1)` [has Async]

### `DesignContextsType`
**Свойства:** Classes: DesignContextsTypes, IsDesignContext: Boolean

### `DesignContextsTypes`
**Свойства:** DesignContext: DesignContextsType

### `Desktop`
**Методы:**
- `IEnumerable`1 CheckOut(IEnumerable`1 objects, Boolean delete, Object context, Boolean canSetSignaturesNotActual, Int32 packetSize) (+5)` [has Async]
- `IEnumerable`1 CheckIn(IEnumerable`1 objects, String comment, Boolean executeCallBack, Object context, Int32 packetSize, Boolean keepCheckedOut) (+9)` [has Async]
- `IEnumerable`1 UndoCheckOut(IEnumerable`1 objects, Object context, Int32 packetSize) (+4)` [has Async]
- `Void AddLabel(IEnumerable`1 objects, String label, String comment)`
- `List`1 GetCheckedOutObjects(ServerConnection connection) (+2)` [has Async]
- `Boolean HasCheckedOutObjects(ClientView clientView, ReferenceInfo referenceInfo) (+2)` [has Async]
- `Int32 GetCheckedOutObjectsCount(IEnumerable`1 clientViews)`
- `List`1 GetAllCheckedOutObjects(ServerConnection connection) (+1)` [has Async]
- `List`1 GetCurrentUserHistory(ServerConnection connection, Boolean withLabel) (+2)`
- `List`1 GetUserHistory(User user, HistoryFilters filters, Boolean withLabel) (+1)`
- `List`1 GetAllUserHistory(ServerConnection connection, Boolean withLabel) (+2)`
- `List`1 GetChangelists(ReferenceObject referenceObject, Boolean withLabel)`
- `List`1 GetObjectChangelists(ReferenceObject referenceObject, Boolean withLabel)`
- `IEnumerable`1 Restore(IEnumerable`1 objects, Boolean restoreChildren, String comment, Boolean skipLinks, Int32 packetSize, Boolean executeCallback) (+2)` [has Async]
- `ReferenceObject CheckOutVersion(ReferenceObject referenceObject, Int32 version, Boolean canSetSignaturesNotActual) (+1)`
- `Boolean ClearRecycleBin(IEnumerable`1 desktopObjects, Int32 packetSize) (+1)` [has Async]

### `DesktopObject`
**Свойства:** Id: Int32, Guid: Guid, CanEdit: Boolean, CanDelete: Boolean, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, CanCheckOut: Boolean, CanCheckIn: Boolean, CanUndoCheckOut: Boolean, LockState: ReferenceObjectLockState, Links: ReferenceObjectLinks, Reference: Reference, IsAdded: Boolean, IsNew: Boolean, IsDeleted: Boolean, IsModified: Boolean, IsChanged: Boolean, Changing: Boolean, LockStateDescription: String, LockStateIcon: IconImage
**Методы:**
- `IEnumerable`1 CheckOut(Boolean delete, Object context) (+2)` [has Async]
- `IEnumerable`1 CheckIn(String comment, Object context, Boolean executeCallBack, Boolean keepCheckedOut) (+4)` [has Async]
- `IEnumerable`1 UndoCheckOut(Object context) (+1)` [has Async]
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`
- `ClassObjectCollection GetAllowedClassesToLink(ParameterGroup linkGroup)`
- `List`1 GetObjects(Guid linkGuid) (+3)` [has Async]
- `Boolean TryGetObjects(Guid linkGuid, List`1& objects) (+1)` [has Async]
- `ReferenceObject GetObject(Guid linkGroup) (+3)` [has Async]
- `Boolean TryGetObject(Guid linkGroup, ReferenceObject& linkedObject) (+1)` [has Async]
- `ComplexHierarchyLink GetLinkedComplexLink(Guid linkGroup) (+1)`
- `Boolean TryLinkedComplexLink(Guid linkGroup, ComplexHierarchyLink& link) (+1)`
- `ReferenceObject CreateListObject(Guid objectList, Guid listObjectClass) (+2)`
- `Void ClearObjectList(Guid objectList) (+1)`
- `Void SetLinkedObject(Guid linkGroup, ReferenceObject newLinkedObject) (+1)`
- `ReferenceObject AddLinkedObject(Guid linkGuid, ReferenceObject newLinkedObject) (+1)`
- `Void SetLinkedComplexLink(Guid linkGroup, ComplexHierarchyLink link) (+1)`
- `Void AddLinkedComplexLink(Guid linkGroup, ComplexHierarchyLink link) (+1)`
- `Boolean RemoveLinkedObject(Guid linkGuid, ReferenceObject linkedObject) (+1)`
- `Boolean RemoveLinkedComplexLink(Guid linkGuid, ComplexHierarchyLink link) (+1)`
- `Void ClearLinks(Guid linkGuid) (+2)`
- `ParameterGroup FindRelation(Guid groupGuid)`
- `Boolean ContainsRelation(Int32 groupId)`
- `Void BeginChanges()` [has Async]
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges()` [has Async]
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, Boolean throwOnError) (+1)`
- `Boolean BelongsToConfigurationSettings()`

### `DesktopObjectPacketSet`1`
**Свойства:** Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Object GetContextProperty(String propertyName)`
- `Void SetContextProperty(String propertyName, Object value)`
- `Void Add(TDesktopObject desktopObject)` [has Async]
- `Boolean Contains(TDesktopObject desktopObject)`
- `Void CopyTo(TDesktopObject[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `DesktopObjectResources`
**Методы:**
- `IconImage GetLockStateIcon(ReferenceObjectLockState lockState)`
- `String GetLockStateDescription(ReferenceObjectLockState lockState)`

### `DesktopObjectWithLink`
**Свойства:** DesktopObject: DesktopObject, Link: ComplexHierarchyLink, ReferenceObjectWithLink: ReferenceObjectWithLink

### `DesktopOperationInfo`
**Свойства:** Connection: ServerConnection, Type: DesktopOperationType, Count: Int32, Items: ReadOnlyCollection`1, Comment: String, KeepCheckedOut: Boolean
**Методы:**
- `Void AddNewLinkedObjects()` [has Async]
- `List`1 GetObjects()`
- `DesktopOperationItem Find(DesktopObject desktopObject)`
- `Boolean Contains(DesktopOperationItem item)`
- `Boolean Remove(DesktopOperationItem item)`
- `DesktopOperationItem Add(DesktopObject desktopObject)`
- `Void AddContext(DesktopOperationInfoContext context)`
- `DesktopOperationInfoContext FindContext(DesktopOperationInfoContextType type)`

### `DesktopOperationInfoContext`
**Свойства:** Type: DesktopOperationInfoContextType

### `DesktopOperationItem`
**Свойства:** Item: DesktopObject, ReferenceId: Int32, ObjectId: Int32, DependentItems: ReadOnlyCollection`1
**Методы:**
- `HashSet`1 GetAllDependentItems()`
- `Void MergeAllDependentItems(HashSet`1 items)`

### `DiagramSettings`
**Свойства:** DiagramType: DiagramType, Series: ObservableCollection`1, Panes: ObservableCollection`1, Titles: ObservableCollection`1, IsRotated: Boolean, LoadDataOnlyWithCurrentObject: Boolean, VariablesDataString: String, ElementsFormula: String, SeriesFormula: String, SeriesPointFormula: String, ThemeName: String, PaletteType: PaletteType, IsXNavigationEnabled: Boolean, IsYNavigationEnabled: Boolean, IsHorizontalScrollBarVisible: Boolean, IsVerticalScrollBarVisible: Boolean, IsAxisXSynchronize: Boolean, Legends: ObservableCollection`1, IsLegendVisible: Boolean, LegendHorizontalPosition: HorizontalPositionType, LegendVerticalPosition: VerticalPositionType, LegendOrientation: Orientation

### `Dialog`
**Свойства:** Id: Int32, Guid: Guid, ParameterGroup: ParameterGroup, Class: ClassObject, IsDockable: Boolean, HideToolbarInSeparateWindow: Boolean, EditObjectListInPropertyPanel: Boolean, Groups: ReadOnlyCollection`1, Changing: Boolean
**Методы:**
- `List`1 GetLinkDialogs()`
- `Void AddLinkDialog(ParameterGroup link)`
- `Boolean ContainsLinkDialog(Guid linkGuid)`
- `Boolean RemoveLinkDialog(Guid linkGuid)`
- `Void SwapGroups(DialogGroup group1, DialogGroup group2)`
- `DialogGroup CreateGroup()`
- `Void BeginChanges()`
- `Boolean ValidateLicense(Boolean throwOnError)`
- `Void CancelChanges()`
- `Void EndChanges()` [has Async]
- `Void Delete()` [has Async]

### `DialogConfigurationUseTypeExtensions`
**Методы:**
- `String GetConfigurationUseTypeName(ConfigurationUseType type)`

### `DialogGroup`
**Свойства:** Id: Int32, Guid: Guid, Dialog: Dialog, Name: String, Comment: String, Icon: IconImage, GeneratedForGroup: ParameterGroup, Pages: ReadOnlyCollection`1, Changing: Boolean
**Методы:**
- `Void SwapPages(DialogPage page1, DialogPage page2)`
- `Void AddPage(DialogPage page)` [has Async]
- `Boolean RemovePage(DialogPage page)` [has Async]
- `Void BeginChanges()`
- `Void CancelChanges()`
- `Void EndChanges()` [has Async]
- `Void Delete()` [has Async]
- `List`1 GetObjectPages(ReferenceObject referenceObject)`

### `DialogManager`
**Свойства:** ParameterGroup: ParameterGroup, Pages: ReadOnlyCollection`1, AllDialogs: List`1
**Методы:**
- `Void Refresh()` [has Async]
- `Dialog GetGroupDialog()`
- `Dialog GetClassDialog(ClassObject classObject)`
- `Dialog CreateGroupDialog()`
- `Dialog CreateClassDialog(ClassObject classObject)`
- `DialogPage CreateGroupPage()`
- `DialogPage CreateClassPage(ClassObject classObject)`
- `Dialog GetObjectDialog(ReferenceObject referenceObject)`
- `Dialog GetObjectWebDialog(ReferenceObject referenceObject)`
- `Dialog GetEmptyWebDialog()`
- `Dialog GetLinkDialog(ComplexHierarchyLink link) (+1)`
- `Boolean IsUsed(DialogPage page)`

### `DialogPage`
**Свойства:** HasNativeData: Boolean, Id: Int32, Guid: Guid, ParameterGroup: ParameterGroup, Class: ClassObject, Name: String, Comment: String, Type: DialogPageType, DialogType: DialogType, Icon: IconImage, Data: Byte[], Assembly: String, ClassName: String, UsedInPanel: Boolean, UsedInDialog: Boolean, Hidden: Boolean, UsedInClient: DialogPageClient, GeneratedForGroup: ParameterGroup, AccessType: DialogPageAccessType, ConfigurationUseType: ConfigurationUseType, Users: UserCollection, Configurations: ConfigurationCollection, IsModified: Boolean, Changing: Boolean
**Методы:**
- `Boolean CanUseInCurrentConfiguration()`
- `Boolean CanUseInConfiguration(BaseConfiguration configuration)`
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `Boolean ValidateLicense(Boolean throwOnError)`
- `Void BeginChanges()`
- `Void CancelChanges()`
- `Void EndChanges()` [has Async]
- `Void Delete()` [has Async]

### `DialogPageAccessTypeExtensions`
**Методы:**
- `String GetAccessTypeName(DialogPageAccessType type)`

### `DialogPageClientExtensions`
**Методы:**
- `String GetClientName(DialogPageClient client)`

### `DialogPageExchangeService`
**Методы:**
- `Boolean Export(ParameterGroup reference, ClassObject classObject, Dictionary`2 dialogPages, String fileName)` [has Async]
- `List`1 Import(String fileName, DialogGroup dialogGroup, ParameterGroup parameterGroup, ClassObject classObject)` [has Async]

### `DialogPageTypeExtensions`
**Методы:**
- `String GetPageName(DialogPageType type)`

### `DialogSizeFieldInputDialog`
**Свойства:** TypeName: String, Width: InArgument`1, Height: InArgument`1

### `DialogTypeExtensions`
**Методы:**
- `String GetName(DialogType type)`

### `DictionaryComparer`
**Методы:**
- `Int32 Compare(Guid x, Guid y)`

### `DigitalSignatureContent`
**Свойства:** ParametersGuids: Guid[], Parameters: String[], ReferenceObjectData: Byte[]
**Методы:**
- `Byte[] GetData()` [has Async]
- `String GetSigningParametersValuesString()`
- `List`1 Parse(String parametersString, Boolean& hasReferenceObjectData) (+1)`

### `DOCsAccount`
**Свойства:** Instance: DOCsAccount, TaskAccess: MailTasksAccess, Guid: Guid, Name: String, Outbox: MailFolder, TaskFolders: TaskFolderCollection, CanSaveMessagesOnServer: Boolean
**Методы:**
- `Int32 GetUnreadTaskCount()` [has Async]
- `List`1 GetTasks(Int32 count, Int32 startIndex, Filter filter) (+1)` [has Async]
- `List`1 GetUnreadTasks()` [has Async]
- `Void CancelTasks(Filter filter)` [has Async]
- `MailMessage FindMessage(Int32 globalId, Int32 folderId)`
- `MailTask FindTask(Int32 globalId)` [has Async]
- `List`1 GetObjectMessages(ReferenceObject object)` [has Async]
- `List`1 GetObjectTasks(ReferenceObject object)` [has Async]
- `List`1 GetObjectItems(ReferenceObject object)` [has Async]
- `Boolean IsSystemFolder(MailItemFolder folder)`
- `SmtpServerSettings GetSmtpServerSettings(User user)`
- `Void SendMessage(MailMessage message)`
- `Boolean SetMessagesRead(IEnumerable`1 messages)`
- `Boolean SetMessagesUnread(IEnumerable`1 messages)`
- `Boolean SetFolderRead(MailItemFolder mailItemFolder)`
- `Boolean SetFolderUnread(MailItemFolder mailItemFolder)`

### `DocumentReference`
**Свойства:** Classes: DocumentTypes

### `DocumentType`
**Свойства:** Classes: DocumentTypes, IsEngineeringDesignDocument: Boolean, IsProductDocument: Boolean, IsDetail: Boolean, IsAssembly: Boolean, IsDrawing: Boolean, IsAssemblyDrawing: Boolean

### `DocumentTypes`
**Свойства:** EngineeringDesignDocument: DocumentType, ProductDocument: DocumentType, Detail: DocumentType, Assembly: DocumentType, Product: DocumentType, Drawing: DocumentType, AssemblyDrawing: DocumentType

### `DomainObject`
**Свойства:** Id: Int32

### `DomainObjectCollection`1`
**Свойства:** Item: T, Count: Int32
**Методы:**
- `T Find(Int32 id)`
- `Int32 IndexOf(Int32 id) (+1)`
- `Boolean Contains(Int32 id) (+1)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `DomainObjectComparer`
**Методы:**
- `Int32 Compare(DomainObject x, DomainObject y)`

### `DoubleFieldInputDialog`
**Свойства:** TypeName: String, DefaultValue: InArgument`1, DecimalPlaces: InArgument`1

### `DoubleParameter`
**Методы:**
- `Double GetDouble()`
- `TypeCode GetTypeCode()`

### `DoubleVariableData`
**Свойства:** Value: Double

### `DynamicColumnData`
**Свойства:** Source: String, Filter: String, Header: String, Value: String, ValueToString: String, DisplayMask: String, ValueSplitter: String, CreateObjectsOnEdit: Boolean, SummaryType: Int32, Type: ColumnDataType, IsEmpty: Boolean, SourcePath: Object, ValuePath: Object, ValueToStringPath: Object, HeaderPath: Object

### `DynamicMacro`
**Свойства:** Guid: Guid, Name: String, SourceCodes: List`1, References: List`1, IsCompiled: Boolean, CompilationResult: CompilationResult, UseCurrentDomain: Boolean, UseConvertResult: Boolean, IsDefineServer: Boolean, ExecutionPlace: ExecutionPlace, DebugMode: Boolean, AdditionalFiles: List`1
**Методы:**
- `Void AddReference(String reference)`
- `Void Clear()`
- `CompilationResult Compile()`
- `Object Run(MacroContext context, String entryPoint, Object[] args) (+1)` [has Async]
- `Type GetMacroProviderType()`
- `IEnumerable`1 GetEntryPoints()`

### `DynamicType`
**Методы:**
- `TypeCode GetTypeCode()`
- `Boolean ToBoolean(IFormatProvider provider)`
- `Byte ToByte(IFormatProvider provider)`
- `Char ToChar(IFormatProvider provider)`
- `DateTime ToDateTime(IFormatProvider provider)`
- `Decimal ToDecimal(IFormatProvider provider)`
- `Double ToDouble(IFormatProvider provider)`
- `Int16 ToInt16(IFormatProvider provider)`
- `Int32 ToInt32(IFormatProvider provider)`
- `Int64 ToInt64(IFormatProvider provider)`
- `SByte ToSByte(IFormatProvider provider)`
- `Single ToSingle(IFormatProvider provider)`
- `Guid ToGuid(IFormatProvider provider)`
- `Byte[] ToByteArray(IFormatProvider provider)`
- `Object ToType(Type conversionType, IFormatProvider provider) (+1)`
- `UInt16 ToUInt16(IFormatProvider provider)`
- `UInt32 ToUInt32(IFormatProvider provider)`
- `UInt64 ToUInt64(IFormatProvider provider)`

### `EasyFilterObject`
**Свойства:** Class: EasyFilterType, Name: StringParameter, Path: StringParameter
**Методы:**
- `ReferencePath GetReferencePath()`

### `EasyFilterReference`
**Свойства:** Classes: EasyFilterTypes

### `EasyFilterSetObject`
**Свойства:** ReferenceGroup: ParameterGroup, Class: EasyFilterSetType, TargetReference: GuidParameter, ObjectList: StringParameter, EasyFilterObjects: ReferenceObjectCollection
**Методы:**
- `ReferenceObject CreateEasyFilter(Guid listObjectClass) (+1)`

### `EasyFilterSetReference`
**Свойства:** Classes: EasyFilterSetTypes
**Методы:**
- `List`1 Find(ParameterGroup referenceGroup)`
- `List`1 GetEasyFilterObjects(ParameterGroup referenceGroup)`

### `EasyFilterSetType`
**Свойства:** Classes: EasyFilterSetTypes, IsEasyFilterSetObject: Boolean

### `EasyFilterSetTypes`
**Свойства:** EasyFilterSetObject: EasyFilterSetType

### `EasyFilterType`
**Свойства:** Classes: EasyFilterTypes, IsEasyFilterObject: Boolean

### `EasyFilterTypes`
**Свойства:** EasyFilterObject: EasyFilterType

### `EditorPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `EditSession`
**Свойства:** Object: ReferenceObject
**Методы:**
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges()` [has Async]

### `ElementEnabledFieldInputDialog`
**Свойства:** TypeName: String, Value: InArgument`1

### `ElementVisibilityFieldInputDialog`
**Свойства:** TypeName: String, Value: InArgument`1

### `EMailAddress`
**Свойства:** Name: String, Email: String, Address: String, NetMailAddress: MailAddress

### `EmailServerSettings`
**Методы:**
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `EmbedVariableManager`
**Свойства:** Instance: EmbedVariableManager, Variables: ReadOnlyCollection`1
**Методы:**
- `Boolean AddVariable(ContextVariableInfo variable)`
- `Void AddVariables(IEnumerable`1 variables)`
- `Boolean RemoveVariable(ContextVariableInfo variable)`
- `Void RemoveVariables(IEnumerable`1 variables)`
- `ContextVariableInfo GetVariableByName(String variableName)`
- `ContextVariableInfo GetVariable(String variableValue)`
- `List`1 GetVariables(Type type, Boolean canInherit) (+1)`
- `Void Clear()`

### `EmptyViewerServiceOwner`
**Свойства:** AsyncModeSupported: Boolean, Control: Object
**Методы:**
- `Void DoShowPreview(Boolean async)`

### `EndProductPathItem`
**Свойства:** Name: String, Type: PathItemType

### `EngineeringDocumentObject`
**Свойства:** Name: String, Denotation: String, Code: String, Letter: String, Mass: Double
**Методы:**
- `Void AddFile(FileObject file)`
- `List`1 GetFiles()`
- `Void SaveFileContext(Byte[] context, FileObject file)`

### `EntranceObjectRelation`
**Свойства:** ComplexLink: ComplexHierarchyLink, Child: ReferenceObjectEntrance, Amount: Double

### `EntrancesChangingActionReferenceObject`
**Свойства:** Count: Int32Parameter, Remarks: StringParameter

### `EntrancesTree`
**Свойства:** Objects: IEnumerable`1, RootObjects: IEnumerable`1, StructuresEntrances: IEnumerable`1

### `EntryPoint`
**Свойства:** Name: String, Title: String, ReturnType: Type
**Методы:**
- `IEntryPointParameter[] GetParameters()`
- `TAttribute GetAttribute()`

### `EntryPointExtensions`
**Методы:**
- `String GetFullName(IEntryPoint entryPoint, ProgrammingLanguage language)`
- `Boolean IsExpression(String serEntryPoint)`
- `Int32 GetParametersCount(String serEntryPoint)`
- `Boolean IsEqual(IEntryPoint entryPoint, String serEntryPoint, ProgrammingLanguage language)`

### `EnumManager`
**Методы:**
- `Void CacheMetadata(CodeActivityMetadata& metadata, InArgument`1 argument, String errorText)`

### `EqualMailCategoryOperator`
**Свойства:** Type: ComparisonOperatorType, RequireValueList: Boolean
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `EventSourceExtension`
**Методы:**
- `String GetText(EventSource type)`

### `EventTypeExtension`
**Методы:**
- `String GetText(EventType type)`

### `EventWatcher`
**Свойства:** Connection: ServerConnection
**Методы:**
- `EventWatcherLock WatchCreatedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+7)` [has Async]
- `EventWatcherLock WatchChangedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+7)` [has Async]
- `EventWatcherLock WatchDeletedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+7)` [has Async]
- `EventWatcherLock WatchReferenceChanged(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+1)` [has Async]
- `EventWatcherLock WatchReferencesChanged(IEnumerable`1 references, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback)` [has Async]
- `EventWatcherLock WatchReferenceCatalogChanged(ISynchronizeInvoke synchronizeInvoke, ReferenceChangedCallback callback)` [has Async]
- `EventWatcherLock WatchReferenceCatalogChangedDebug(ISynchronizeInvoke synchronizeInvoke, ReferenceChangedCallbackDebug callback)` [has Async]
- `EventWatcherLock WatchAccessChangedChanged(ISynchronizeInvoke synchronizeInvoke, AdminAccessChangedCallback callback)` [has Async]
- `EventWatcherLock WatchForCreatedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+3)`
- `EventWatcherLock WatchForChangedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+3)`
- `EventWatcherLock WatchForDeletedObjects(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+3)`
- `EventWatcherLock WatchForReferenceChanged(ReferenceInfo referenceInfo, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback) (+1)`
- `EventWatcherLock WatchForReferencesChanged(IEnumerable`1 references, ISynchronizeInvoke synchronizeInvoke, ObjectCreatedCallback callback)`

### `EventWatcherLock`
**Свойства:** IsAlive: Boolean
**Методы:**
- `ValueTask StopWatching(CancellationToken token)`

### `ExceptionHandler`
**Методы:**
- `Void Invoke(Exception e)`
- `IAsyncResult BeginInvoke(Exception e, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ExchangePluginData`
**Свойства:** PluginModuleName: String, PluginClassName: String, Data: Byte[]

### `ExecutionPlaceExtensions`
**Методы:**
- `Boolean IsOnServerSide(ExecutionPlace executionPlace)`
- `Boolean IsOnClientSide(ExecutionPlace executionPlace)`
- `String GetDefineOption(ExecutionPlace executionPlace)`

### `ExecutorCandidate`
**Свойства:** Status: ExecutorCandidateStatus, Executor: User, Assignment: AssignmentReferenceObject

### `ExecutorCandidatesManager`
**Свойства:** GroupAssignment: GroupAssignmentReferenceObject, IsModified: Boolean
**Методы:**
- `ExecutorCandidate Add(User user)`
- `Void Remove(UserReferenceObject user)`
- `Void Detaching(UserReferenceObject user)`
- `List`1 GetChanges()`
- `Void CancelChanges()`
- `IEnumerator`1 GetEnumerator()`

### `ExistsInCollectionActivity`1`
**Свойства:** Values: InArgument`1, Item: InArgument`1

### `ExportCallback`
**Методы:**
- `Boolean Invoke(String[] messages, Int32 counter, Int32 totalCount)`
- `IAsyncResult BeginInvoke(String[] messages, Int32 counter, Int32 totalCount, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `ExportCatalogSettings`
**Свойства:** Catalog: Catalog, IncludeAllCatalogFolders: Boolean, CatalogFolders: IReadOnlyCollection`1
**Методы:**
- `Boolean AddCatalogFolder(Int32 id) (+2)`
- `Void AddCatalogFolders(Int32[] ids) (+5)`
- `Boolean ContainsCatalogFolder(Int32 id) (+2)`
- `Boolean RemoveCatalogFolder(Int32 id) (+2)`

### `ExportClassSettings`
**Свойства:** ClassObject: ClassObject, IncludeAllEventHandlers: Boolean, EventHandlers: IReadOnlyCollection`1, HasEventHandlers: Boolean, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1, RevisionNamingRule: ExportRevisionNamingRuleSettings, HasRevisionNamingRule: Boolean, Scheme: ExportSchemeSettings, HasScheme: Boolean
**Методы:**
- `Boolean AddEventHandler(Int32 id)`
- `Void AddEventHandlers(Int32[] ids) (+1)`
- `Boolean Add(ParameterGroupEventHandler eventHandler) (+2)`
- `Boolean ContainsEventHandler(Int32 id)`
- `Boolean Contains(ParameterGroupEventHandler eventHandler)`
- `Boolean RemoveEventHandler(Int32 id)`
- `Boolean Remove(ParameterGroupEventHandler eventHandler)`
- `Boolean AddProperty(ClassProperties property)`
- `Void AddProperties(ClassProperties[] properties) (+1)`
- `Boolean ContainsProperty(ClassProperties property)`
- `Boolean RemoveProperty(ClassProperties property)`
- `ExportRevisionNamingRuleSettings AddRevisionNamingRule()`
- `Void RemoveRevisionNamingRule()`
- `ExportSchemeSettings AddScheme()`
- `Void RemoveScheme()`

### `ExportContext`
**Свойства:** Path: String, Page: Int32, Pages: List`1, Parameters: Dictionary`2, IsRepresentation: Boolean, Item: Object
**Методы:**
- `Boolean ContainsParameter(String key)`
- `IEnumerable`1 GetParametersEnumerator()`

### `ExportDialogGroupSettings`
**Свойства:** DialogGroup: DialogGroup, IncludeAllDialogPages: Boolean, DialogPages: IReadOnlyCollection`1, HasDialogPages: Boolean
**Методы:**
- `Boolean AddDialogPage(Int32 id) (+1)`
- `Void AddDialogPages(Int32[] ids) (+3)`
- `Boolean Add(DialogPage dialogPage) (+2)`
- `Boolean ContainsDialogPage(Int32 id) (+1)`
- `Boolean Contains(DialogPage dialogPage)`
- `Boolean RemoveDialogPage(Int32 id) (+1)`
- `Boolean Remove(DialogPage dialogPage)`

### `ExportDialogsModeExtensions`
**Методы:**
- `String GetName(ExportDialogsMode mode)`

### `ExportDialogsModeExtensions`
**Методы:**
- `String GetName(ExportSettingsLoadDirection loadDirection)`

### `ExportErrorObjectsCallback`
**Методы:**
- `Boolean Invoke(List`1 descriptions)`
- `IAsyncResult BeginInvoke(List`1 descriptions, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `ExportLinkedObjectsModeExtensions`
**Методы:**
- `String GetName(ExportLinkedObjectsMode mode)`

### `ExportLinkSettings`
**Свойства:** LinkGroup: ParameterGroup, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1
**Методы:**
- `Boolean AddProperty(ParameterGroupProperties property)`
- `Void AddProperties(ParameterGroupProperties[] properties) (+1)`
- `Boolean ContainsProperty(ParameterGroupProperties property)`
- `Boolean RemoveProperty(ParameterGroupProperties property)`

### `ExportObjectsModeExtensions`
**Методы:**
- `String GetName(ExportObjectsMode mode)`

### `ExportObjectsPreviewLinkSettingsData`
**Свойства:** LinkGroup: Guid, IncludeLinkObjectsById: Boolean

### `ExportObjectsPreviewReferenceSettingsData`
**Свойства:** Objects: List`1

### `ExportObjectsPreviewSettingsData`
**Свойства:** MasterGroup: Guid, IncludeSignatures: Boolean, DontChangeObjects: Boolean, LoadDirection: ExportSettingsLoadDirection, IncludeAllParameters: Boolean, Parameters: List`1, IncludeAllLinks: Boolean, Links: List`1

### `ExportObjectsSettings`
**Свойства:** ObjectIds: IReadOnlyCollection`1, HierarchyLinkIds: IReadOnlyCollection`1
**Методы:**
- `Boolean ContainsObjectId(Int32 objectId)`
- `Void AddObject(Int32 objectId, Int32 instanceId) (+2)`
- `Void AddObjects(IEnumerable`1 objectIds, Dictionary`2 instanceIds) (+2)`
- `ExportObjectsSettings Create(ReferenceInfo referenceInfo) (+1)` [has Async]
- `Boolean ContainsHierarchyLinkId(Int32 hierarchyLinkId)`
- `Void AddHierarchyLink(ComplexHierarchyLink hierarchyLink) (+1)`
- `Void AddHierarchyLinks(IEnumerable`1 hierarchyLinks) (+1)`

### `ExportOptions`
**Свойства:** ExportMode: ExportMode, EncryptionMode: ExportEncryptionMode, ObjectsMode: ExportObjectsMode, DialogsMode: ExportDialogsMode, LinkedObjectsMode: ExportLinkedObjectsMode, IncludeStructure: Boolean, IncludeSigningParameters: Boolean, IncludePrototypes: Boolean, IncludeViews: Boolean, IncludeDialogs: Boolean, IncludeMacros: Boolean, IncludeAccesses: Boolean, IncludeRevisionNamingRules: Boolean, IncludeConfigurators: Boolean, IncludeProductsApplicability: Boolean, IncludeObjectStages: Boolean, IncludeCoordinates: Boolean, IncludeInstances: Boolean, ExportSpecificInstances: Boolean, FileName: String, DataFormat: TextFormats, Indent: Boolean, UsePackage: Boolean, BinaryFormat: Boolean, PlainFormat: Boolean, PlainCompression: CompressionAlgorithm, DataStream: Stream, FileIds: List`1, ApplicationIds: List`1, Callback: ExportCallback, ErrorObjectsCallback: ExportErrorObjectsCallback, SynchronizeInvoke: ISynchronizeInvoke

### `ExportParameterGroupSettings`
**Свойства:** ParameterGroup: ParameterGroup, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1
**Методы:**
- `Boolean AddProperty(ParameterGroupProperties property)`
- `Void AddProperties(ParameterGroupProperties[] properties) (+1)`
- `Boolean ContainsProperty(ParameterGroupProperties property)`
- `Boolean RemoveProperty(ParameterGroupProperties property)`

### `ExportParameterSettings`
**Свойства:** Parameter: ParameterInfo, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1
**Методы:**
- `Boolean AddProperty(ParameterProperties property)`
- `Void AddProperties(ParameterProperties[] properties) (+1)`
- `Boolean ContainsProperty(ParameterProperties property)`
- `Boolean RemoveProperty(ParameterProperties property)`

### `ExportPreviewSettingsData`
**Свойства:** References: List`1, Objects: List`1

### `ExportReferencePathExtensions`
**Методы:**
- `ExportSettings AddToExportSettings(ReferencePath path, ExportSettings settings)`

### `ExportReferencePreviewCatalogSettingsData`
**Свойства:** Catalog: Guid, CatalogFolders: List`1

### `ExportReferencePreviewClassSettingsData`
**Свойства:** ClassObject: Guid, IncludeAllProperties: Boolean, Properties: List`1, IncludeAllEventHandlers: Boolean, HandlerEvents: List`1

### `ExportReferencePreviewDialogGroupSettingsData`
**Свойства:** DialogGroup: Guid, IncludeAllDialogPages: Boolean, DialogPages: List`1

### `ExportReferencePreviewEventHandlerSettingsData`
**Свойства:** Event: Guid, Handler: Guid, EntryPoint: String, Data: String

### `ExportReferencePreviewLinkSettingsData`
**Свойства:** LinkGroup: Guid, IncludeAllProperties: Boolean, Properties: List`1

### `ExportReferencePreviewParameterGroupSettingsData`
**Свойства:** ParameterGroup: Guid, IncludeAllProperties: Boolean, Properties: List`1

### `ExportReferencePreviewParameterSettingsData`
**Свойства:** Parameter: Guid, IncludeAllProperties: Boolean, Properties: List`1

### `ExportReferencePreviewRevisionNamingRuleSettingsData`
**Свойства:** RevisionNamingRule: Guid, IncludeAllRevisionLevels: Boolean, RevisionLevels: List`1

### `ExportReferencePreviewSchemeSettingsData`
**Свойства:** Scheme: Guid, Stages: List`1, Transitions: List`1

### `ExportReferencePreviewSettingsData`
**Свойства:** MasterGroup: Guid, IncludeAllProperties: Boolean, Properties: List`1, IncludeAllClasses: Boolean, Classes: List`1, IncludeAllParameters: Boolean, Parameters: List`1, IncludeAllParameterGroups: Boolean, ParameterGroups: List`1, IncludeAllLinks: Boolean, Links: List`1, IncludeAllObjectLists: Boolean, ObjectLists: List`1, IncludeAllEvents: Boolean, Events: List`1, IncludeAllEventHandlers: Boolean, HandlerEvents: List`1, IncludeAllDialogGroups: Boolean, DialogGroups: List`1, IncludeAllAccesses: Boolean, Accesses: List`1, IncludeAllCatalogs: Boolean, Catalogs: List`1, IncludeAllPrototypes: Boolean, Prototypes: List`1, RevisionNamingRule: ExportReferencePreviewRevisionNamingRuleSettingsData, Scheme: ExportReferencePreviewSchemeSettingsData, IncludeAllSignatureTypes: Boolean, SignatureTypes: List`1, IncludeAllViews: Boolean, Views: List`1

### `ExportReferenceSettings`
**Свойства:** IncludeAllAccesses: Boolean, Accesses: IReadOnlyCollection`1, HasAccesses: Boolean, IncludeAllCatalogs: Boolean, Catalogs: IReadOnlyCollection`1, HasCatalogs: Boolean, IncludeAllClasses: Boolean, Classes: IReadOnlyCollection`1, HasClasses: Boolean, MasterGroup: ParameterGroup, IncludeAllDialogGroups: Boolean, DialogGroups: IReadOnlyCollection`1, HasDialogGroups: Boolean, IncludeAllEventHandlers: Boolean, EventHandlers: IReadOnlyCollection`1, HasEventHandlers: Boolean, IncludeAllEvents: Boolean, Events: IReadOnlyCollection`1, HasEvents: Boolean, IncludeAllLinks: Boolean, Links: IReadOnlyCollection`1, HasLinks: Boolean, IncludeAllObjectLists: Boolean, ObjectLists: IReadOnlyCollection`1, HasObjectLists: Boolean, IncludeAllParameterGroups: Boolean, ParameterGroups: IReadOnlyCollection`1, HasParameterGroups: Boolean, IncludeAllParameters: Boolean, Parameters: IReadOnlyCollection`1, HasParameters: Boolean, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1, IncludeAllPrototypes: Boolean, Prototypes: IReadOnlyCollection`1, HasPrototypes: Boolean, RevisionNamingRule: ExportRevisionNamingRuleSettings, HasRevisionNamingRule: Boolean, Scheme: ExportSchemeSettings, HasScheme: Boolean, IncludeAllSignatureTypes: Boolean, SignatureTypes: IReadOnlyCollection`1, HasSignatureTypes: Boolean, IncludeAllViews: Boolean, Views: IReadOnlyCollection`1, HasViews: Boolean
**Методы:**
- `Boolean ContainsParameter(Guid guid) (+1)`
- `Boolean Contains(ParameterInfo parameter) (+5)`
- `Boolean RemoveParameter(Int32 id) (+1)`
- `Boolean Remove(ParameterInfo parameter) (+5)`
- `Boolean AddProperty(ParameterGroupProperties property)`
- `Void AddProperties(ParameterGroupProperties[] properties) (+1)`
- `Boolean ContainsProperty(ParameterGroupProperties property)`
- `Boolean RemoveProperty(ParameterGroupProperties property)`
- `Boolean AddPrototype(Int32 id) (+2)`
- `Void AddPrototypes(Int32[] ids) (+5)`
- `Boolean ContainsPrototype(Int32 id) (+2)`
- `Boolean RemovePrototype(Int32 id) (+2)`
- `ExportRevisionNamingRuleSettings AddRevisionNamingRule()`
- `Void RemoveRevisionNamingRule()`
- `ExportSchemeSettings AddScheme()`
- `Void RemoveScheme()`
- `Boolean AddSignatureType(Int32 id) (+2)`
- `Void AddSignatureTypes(Int32[] ids) (+5)`
- `Boolean ContainsSignatureType(Int32 id) (+2)`
- `Boolean RemoveSignatureType(Int32 id) (+2)`
- `Boolean AddView(Guid viewGuid) (+1)`
- `Void AddViews(Guid[] viewGuids) (+3)`
- `Boolean ContainsView(Guid viewGuid) (+1)`
- `Boolean RemoveView(Guid viewGuid) (+1)`
- `IReadOnlyCollection`1 GetAllViews()` [has Async]
- `Void AddLinks(Guid[] guids) (+3)`
- `ExportLinkSettings Add(ParameterGroup linkGroup) (+17)`
- `Boolean TryGetLink(Int32 id, ExportLinkSettings& settings) (+1)`
- `Boolean TryGet(ParameterGroup linkGroup, ExportLinkSettings& settings) (+3)`
- `Boolean ContainsLink(Int32 id) (+1)`
- `Boolean RemoveLink(Int32 id) (+1)`
- `ExportReferenceSettings AddObjectList(Int32 id) (+2)`
- `Boolean ContainsObjectList(Int32 id) (+2)`
- `Boolean RemoveObjectList(Int32 id) (+2)`
- `ExportParameterGroupSettings AddParameterGroup(Int32 id) (+2)`
- `Void AddParameterGroups(Int32[] ids) (+5)`
- `Boolean TryGetParameterGroup(Int32 id, ExportParameterGroupSettings& settings) (+1)`
- `Boolean ContainsParameterGroup(Int32 id) (+2)`
- `Boolean RemoveParameterGroup(Int32 id) (+2)`
- `ExportParameterSettings AddParameter(Int32 id) (+1)`
- `Void AddParameters(Int32[] ids) (+3)`
- `Boolean TryGetParameter(Int32 id, ExportParameterSettings& settings) (+1)`
- `Boolean AddAccess(Int32 id) (+2)`
- `Void AddAccesses(Int32[] ids) (+5)`
- `Boolean ContainsAccess(Int32 id) (+2)`
- `Boolean RemoveAccess(Int32 id) (+2)`
- `ExportCatalogSettings AddCatalog(Int32 id) (+2)`
- `Void AddCatalogs(Int32[] ids) (+5)`
- `Boolean ContainsCatalog(Int32 id) (+2)`
- `Boolean RemoveCatalog(Int32 id) (+2)`
- `ExportClassSettings AddClass(Int32 id) (+1)`
- `Void AddClasses(Int32[] ids) (+3)`
- `Boolean TryGetClass(Int32 id, ExportClassSettings& settings) (+1)`
- `Boolean ContainsClass(Int32 id) (+1)`
- `Boolean RemoveClass(Int32 id) (+1)`
- `ExportReferenceSettings Create(ReferenceInfo referenceInfo) (+1)` [has Async]
- `ExportDialogGroupSettings AddDialogGroup(Int32 id) (+1)`
- `Void AddDialogGroups(Int32[] ids) (+3)`
- `Boolean ContainsDialogGroup(Int32 id) (+1)`
- `Boolean RemoveDialogGroup(Int32 id) (+1)`
- `Boolean AddEventHandler(Int32 id)`
- `Void AddEventHandlers(Int32[] ids) (+1)`
- `Boolean ContainsEventHandler(Int32 id)`
- `Boolean RemoveEventHandler(Int32 id)`
- `Boolean AddEvent(Int32 id) (+1)`
- `Void AddEvents(Int32[] ids) (+3)`
- `Boolean ContainsEvent(Int32 id) (+1)`
- `Boolean RemoveEvent(Int32 id) (+1)`
- `ExportLinkSettings AddLink(Int32 id) (+1)`

### `ExportRevisionNamingRuleSettings`
**Свойства:** RevisionNamingRule: RevisionNamingRuleObject, IncludeAllRevisionLevels: Boolean, RevisionLevels: IReadOnlyCollection`1, HasRevisionLevels: Boolean
**Методы:**
- `Boolean AddRevisionLevel(Int32 id) (+2)`
- `Void AddRevisionLevels(Int32[] ids) (+5)`
- `Boolean ContainsRevisionLevel(Int32 id) (+2)`
- `Boolean RemoveRevisionLevel(Int32 id) (+2)`

### `ExportSchemeSettings`
**Свойства:** Scheme: Scheme, IncludeAllStages: Boolean, Stages: IReadOnlyCollection`1, HasStages: Boolean, IncludeAllTransitions: Boolean, Transitions: IReadOnlyCollection`1, HasTransitions: Boolean
**Методы:**
- `Boolean AddStage(Int32 id) (+4)`
- `Void AddStages(Int32[] ids) (+3)`
- `Boolean ContainsStage(Int32 id) (+2)`
- `Boolean RemoveStage(Int32 id) (+2)`
- `Boolean AddTransition(ValueTuple`2 transitionGuid) (+1)`
- `Void AddTransitions(ValueTuple`2[] transitionGuids) (+3)`
- `Boolean ContainsTransition(SchemeStageTransition transition)`
- `Boolean RemoveTransition(SchemeStageTransition transition)`

### `ExportSettings`
**Свойства:** Connection: ServerConnection, MasterGroup: ParameterGroup, IncludeSignatures: Boolean, DontChangeObjects: Boolean, LoadDirection: ExportSettingsLoadDirection, IncludeAllParameters: Boolean, Parameters: ParameterInfoCollection, HasParameters: Boolean, IncludeAllLinks: Boolean, Links: IReadOnlyCollection`1, HasLinks: Boolean
**Методы:**
- `Void AddLoadDirection(ExportSettingsLoadDirection loadDirection)`
- `Void RemoveLoadDirection(ExportSettingsLoadDirection loadDirection)`
- `Boolean AddParameter(Int32 parameterId) (+1)`
- `Void AddParameters(Int32[] parameterIds) (+3)`
- `Boolean Add(ParameterInfo parameter) (+2)`
- `Boolean ContainsParameter(Int32 parameterId) (+1)`
- `Boolean Contains(ParameterInfo parameter)`
- `Boolean RemoveParameter(Int32 parameterId) (+1)`
- `Boolean Remove(ParameterInfo parameter)`
- `LinkExportSettings GetLink(Int32 linkId) (+2)`
- `Boolean ContainsLink(ParameterGroup link) (+2)`
- `LinkExportSettings AddLink(Int32 linkId) (+2)`
- `Void CopyLinks(ExportSettings sourceSettings)`
- `StructureTypeExportSettings GetStructureType()`
- `StructureTypeExportSettings AddStructureType()`
- `ProductsApplicabilityExportSettings GetProductsApplicability()`
- `ProductsApplicabilityExportSettings AddProductsApplicability()`
- `StartProductExportSettings GetStartProduct()`
- `StartProductExportSettings AddStartProduct()`
- `EndProductExportSettings GetEndProduct()`
- `EndProductExportSettings AddEndProduct()`
- `RemarksExportSettings GetRemarks()`
- `RemarksExportSettings AddRemarks()`
- `StructureTypesExportSettings GetStructureTypes()`
- `StructureTypesExportSettings AddStructureTypes()`

### `ExportSettingsData`
**Свойства:** Mode: ExportObjectsMode, Structure: Boolean, SigningParameters: Boolean, Prototypes: Boolean, Views: Boolean, Macros: Boolean, DialogsMode: ExportDialogsMode, Accesses: Boolean, RevisionNamingRules: Boolean, Configurators: Boolean, Stages: Boolean, Coordinates: Boolean, Instances: Boolean, LinkedMode: ExportLinkedObjectsMode, Preview: ExportPreviewSettingsData

### `ExportSettingsExtensions`
**Методы:**
- `String GetVisualization(ExportObjectsSettings settings)`

### `ExportSettingsManager`
**Методы:**
- `String Serialize(ExportOptions options, IReadOnlyList`1 referenceSettingsList, IReadOnlyList`1 objectsSettingsList)`
- `ValueTuple`3 Deserialize(ServerConnection connection, String settings)`

### `ExpressionHelper`
**Методы:**
- `ReferenceInfo FindReference(ActivityContext context, InArgument`1 reference)`
- `Boolean IsReferenceExpression(ServerConnection connection, String value, ReferenceInfo& referenceInfo) (+1)`
- `T GetEnumValue(ActivityContext context, InArgument`1 argument, T defaultValue)`
- `Boolean TryParseLink(ServerConnection connection, String referenceName, String linkText, ParameterGroup& linkGroup) (+1)`
- `Boolean IsObjectsListExpression(ServerConnection connection, String value, String referenceName)`
- `ClassObject FindClass(ActivityContext context, InArgument`1 classObject, ReferenceInfo referenceInfo) (+1)`
- `Boolean TryParseClassObject(ServerConnection connection, String referenceName, String classObjectText, ClassObject& classObject) (+1)`
- `Boolean IsClassObjectExpression(ServerConnection connection, String value, String referenceName, ReferenceInfo& referenceInfo, ClassObject& classObject) (+2)`
- `Boolean IsParameterExpression(String value, ClassObject classObject, ParameterInfo& parameterInfo) (+1)`
- `ParameterInfo FindParameter(ActivityContext context, InArgument`1 parameter, ClassObject classObject)`
- `Boolean TryParsePrototype(String value, ReferenceInfo referenceInfo, ReferenceObject& prototypeObject)`
- `ReferenceObject ParsePrototype(String value, ReferenceInfo referenceInfo)`
- `Boolean TryParseClassObjectWithPrototype(ServerConnection connection, String value, String referenceName, ClassObject& classObject, ReferenceObject& prototypeObject) (+1)`
- `Boolean TryParseReferenceObject(ServerConnection connection, String referenceName, String referenceObjectName, ReferenceObject& referenceObject) (+1)`
- `Boolean TryParseSpecialReferenceObject(Reference reference, String referenceObjectName, T& referenceObject)`
- `ReferenceObject FindReferenceObject(ActivityContext context, ReferenceInfo referenceInfo, InArgument`1 referenceObject, Boolean prototypeMode)`
- `Boolean IsReferenceObjectExpression(ServerConnection connection, String value, String reference, ReferenceObject& referenceObject, Boolean prototypeMode) (+1)`
- `Boolean IsSpecialReferenceObjectExpression(ServerConnection connection, String value, String reference, T& referenceObject, Boolean prototypeMode)`
- `SignatureType FindSignatureType(ActivityContext context, InArgument`1 signatureType)`
- `AccessGroup FindAccessGroup(ActivityContext context, InArgument`1 accessGroup)`
- `Filter ParseFilter(String text, ReferenceInfo referenceInfo, MacroContext macroContext, Boolean validate)`
- `Filter GetFilter(ActivityContext context, ReferenceInfo referenceInfo, InArgument`1 filter, Boolean validate) (+1)`
- `Boolean IsExpression(String value)`
- `Boolean IsExpressionOrNull(String value)`
- `Boolean IsGuidValue(String value)`
- `Boolean TryParseInArgumentValue(InArgument`1 argument, T& value)`
- `String GetExpressionValue(String expression)`
- `String MakeExpressionValue(String value)`

### `ExpressionManager`
**Методы:**
- `Boolean TryNeedUpdateArgumentType(Argument value, Type& argumentType)`
- `Argument CreateArgument(Type expressionType, String expressionText, ArgumentDirection direction) (+1)`
- `ActivityWithResult CreateExpression(Type expressionType, String expressionText, ArgumentDirection direction)`
- `String GetExpressionText(ActivityWithResult activity) (+1)`
- `Type GetValueType(Argument argument)`

### `ExtendedGroupPathItem`
**Свойства:** Name: String, Type: PathItemType, Group: ParameterGroup, SupportSearchType: SupportSearchTypes

### `ExtendedParameterInfoBuilder`
**Свойства:** IsExtendedParameterBuilder: Boolean, Aliases: ExtendedParameterReferenceLinksList, Connection: ServerConnection, ParameterClass: ClassObject, IsAliasesEditable: Boolean, IsAliasesEditableList: Boolean, CanAddAliases: Boolean, CanEditAliases: Boolean, CanDeleteAliases: Boolean, CanEditAliasesList: Boolean
**Методы:**
- `Void FixParameterState()`
- `Void CopyFrom(ParameterInfo sourceParameter)`
- `Void Save()` [has Async]
- `ExtendedParameterReferenceLink AddAlias(ParameterInfo parameter, ParameterGroup group, ClassObject classObject, String alias, String comment) (+2)`
- `ParameterInfo BuildAliasedParameterInfo(ParameterGroup group, ExtendedParameterReferenceLink aliasInfo) (+1)`
- `Void UpdateAlias(Int32 index, String alias) (+1)`
- `Void UpdateComment(Int32 index, String comment)`
- `Void DeleteAlias(Int32 index)`
- `Void SetAliases(IEnumerable`1 aliases)`
- `ParameterInfo FindAliasParameterInfo(String aliasToFind, ParameterGroup group)`
- `ExtendedParameterReferenceLink FindAlias(String aliasToFind, ParameterGroup group, ClassObject classObject) (+3)`
- `Boolean ContainsAlias(String aliasToFind, Int32 groupId, Int32 classId)`

### `ExtendedParameterPathItem`
**Свойства:** Name: String, Parameter: ParameterInfo, Type: PathItemType

### `ExtendedParameterReferenceLink`
**Свойства:** Key: GuidKey, Guid: Guid, Id: Int32, ParameterId: Int32, GroupId: Int32, ClassId: Int32, Alias: String, Comment: String, ParameterGroup: ParameterGroup, ClassObject: ClassObject, Connection: ServerConnection
**Методы:**
- `ExtendedParameterReferenceLink Create(ServerConnection connection, Int32 parameterId, Int32 groupId, Int32 classId, String alias, String comment) (+3)`
- `ClassObject GetLinkedClassObject(ClassObject classObject, Int32 groupId)`
- `Boolean IsLinkedClass(Int32 groupId, Int32 classId)`
- `String GetParameterGroupName()`

### `ExtendedParameterReferenceLinksList`
**Свойства:** IsEditable: Boolean, IsEditableList: Boolean, CanAdd: Boolean, CanEdit: Boolean, CanDelete: Boolean, CanEditList: Boolean, Item: ExtendedParameterReferenceLink, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Boolean ContainsAlias(String aliasToFind, Int32 groupId, Int32 classId)`
- `Boolean IsLinkedGroup(Int32 groupId)`
- `Boolean IsLinkedGroupOnly(Int32 groupId)`
- `Boolean IsLinkedClassAndGroup(Int32 groupId, Int32 classId)`
- `Boolean IsLinkedClassOrGroup(Int32 groupId, Int32 classId)`
- `ClassObject GetLinkedClassObject(ClassObject classObject, Int32 groupId)`
- `Int32 IndexOf(ExtendedParameterReferenceLink item)`
- `Void Insert(Int32 index, ExtendedParameterReferenceLink item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(ExtendedParameterReferenceLink item)`
- `Void Clear()`
- `Boolean Contains(ExtendedParameterReferenceLink item)`
- `Void CopyTo(ExtendedParameterReferenceLink[] array, Int32 arrayIndex)`
- `Boolean Remove(ExtendedParameterReferenceLink item)`
- `IEnumerator`1 GetEnumerator()`

### `ExtendedParametersManager`
**Методы:**
- `IReadOnlyCollection`1 GetExtendedParameters()` [has Async]
- `ParameterInfo AttachExtendedParameterToParameterGroup(ParameterInfo parameter, ParameterGroup group, ClassObject classObject) (+1)` [has Async]
- `ParameterInfo AttachExtendedParameterToClassObject(ParameterInfo parameter, ParameterGroup group, ClassObject classObject)` [has Async]
- `Boolean DetachExtendedParameterFromParameterGroup(ParameterInfo parameter, ParameterGroup group, ClassObject classObject)` [has Async]
- `ExtendedParameterReferenceLinksList GetExtendedParameterInfoAliases(ParameterInfo extendedParameter)` [has Async]

### `ExtendedParametersPathItem`
**Свойства:** Name: String, Type: PathItemType, Group: ParameterGroup, SupportSearchType: SupportSearchTypes

### `ExtendedParametersStorage`
**Свойства:** Source: ExtendedParametersStorage, Id: Int32, Guid: Guid, Name: String, Comment: String

### `ExtendedParametersStorageBuilder`
**Свойства:** ValuesStorage: ExtendedParametersStorage, IsAdded: Boolean, IsModified: Boolean, Name: String, Comment: String

### `Extensions`
**Методы:**
- `String ConvertToString64(Image image)`
- `Image ConvertFromString64(String value)`

### `ExtensionUtility`
**Методы:**
- `Boolean Verify(String ext)`
- `String[] ExtractExtensionsFromString(String exts, Boolean& allCorrect) (+1)`
- `String ConcatExtensionsToString(String[] exts, Boolean& allCorrect) (+1)`
- `Boolean Compare(String ext1, String ext2)`

### `FieldInputDialog`
**Свойства:** TypeName: String, InputDialog: InputDialog

### `FileAttachment`
**Свойства:** IsFile: Boolean, Name: String, Size: Int64, FilePath: String, SourceFilePath: String
**Методы:**
- `Boolean DownloadFile()`
- `Void DeleteFile()`

### `FileContainerObject`
**Свойства:** IsFileContainer: Boolean
**Методы:**
- `String GetHeadRevision(String destinationPath)` [has Async]
- `Boolean DeleteFromWorkingFolder()`
- `Boolean IsActualVersionDownloaded()` [has Async]

### `FileContentPathItem`
**Свойства:** Icon: IconImage, DefaultName: String, Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `FileContext`
**Свойства:** PathName: String, VirtualAssembly: Guid, Context: Object, ReadOnly: Boolean, LastModificationTime: DateTime, LinkedInstanceGuid: Guid

### `FileConversionModuleReference`
**Свойства:** Classes: FileConversionModuleTypes
**Методы:**
- `FileConversionModuleReferenceObject Add(String name, String path, String description)`
- `TFlexCadConversionModuleReferenceObject GetDefaultTFlexCadConversionModule()`

### `FileConversionModuleReferenceObject`
**Свойства:** Class: FileConversionModuleType, Name: StringParameter, Path: StringParameter, Description: StringParameter, ConversionTimeoutMinutes: Int32Parameter, MaxConversionAttempts: ByteParameter, WorkerCount: ByteParameter, LinkToConversionModule: ReferenceObject

### `FileConversionModuleType`
**Свойства:** Classes: FileConversionModuleTypes, IsFileConversionModuleReferenceObject: Boolean, IsTFlexCadConversionModuleReferenceObject: Boolean

### `FileConversionModuleTypes`
**Свойства:** FileConversionModuleReferenceObject: FileConversionModuleType, TFlexCadConversionModuleReferenceObject: FileConversionModuleType

### `FileDuplicateAuthorParameter`
**Свойства:** IsReadOnly: Boolean
**Методы:**
- `Int32 GetInt32()`
- `TypeCode GetTypeCode()`

### `FileDuplicateSourceParameter`
**Свойства:** IsReadOnly: Boolean

### `FileExtensionAttribute`
**Свойства:** CanChangeCaption: Boolean, IsSystem: Boolean, Caption: String, Value: Object, CanRemove: Boolean

### `FileHistoryLoader`
**Методы:**
- `List`1 Load(Nullable`1 beginDate, Nullable`1 endDate) (+1)` [has Async]
- `DownloadsLogEventDescription GetDownloadsLogEventDetails(Int64 eventId) (+1)` [has Async]
- `DownloadsLogFilterParameters GetDownloadsEventFilterParameters()` [has Async]

### `FileHistoryRecord`
**Свойства:** EventId: Int64, File: String, ClientView: String, Timestamp: DateTime, FileGuid: Guid, UserId: Int32, HostName: String, ClientAddress: String, LocalPath: String, FileName: String

### `FileLinkAdditionalSettings`
**Свойства:** Data: FileLinkAdditionalSettingsData, IsValid: Boolean, IsLoaded: Boolean, LinkGroup: ParameterGroup, LinkClass: ClassObject
**Методы:**
- `Void Reload()`
- `Boolean Save()`
- `Boolean Remove()`

### `FileLinkAdditionalSettingsData`
**Свойства:** DefaultPath: String, DefaultFileName: String, CreateUserSubfolder: Boolean, ShowSelectFolderDialog: Boolean, ForbidSelectionFromOtherFolders: Boolean, PathIsMacro: Boolean, FileNameIsMacro: Boolean
**Методы:**
- `String Serialize()`
- `Void Deserialize(String data)`

### `FileLinkAdditionalSettingsDataExtensions`
**Методы:**
- `FolderObject GetDefaultFolder(FileLinkAdditionalSettingsData data, LinkInfo link, Boolean createIfNotExist, ReferenceObject parentMasterObject)`
- `String GetDefaultFileName(FileLinkAdditionalSettingsData data, LinkInfo link, FileReferenceObject prototype)`

### `FileObject`
**Свойства:** IsFile: Boolean, Size: Int64, LastChangeDate: DateTime, HasLinkedFiles: Boolean, IsModified: Boolean, IsChanged: Boolean, RepresentationType: RepresentationType, MethodRepresentation: MethodRepresentationType, RepresentationCode: String, RepresentationName: String, LOD: Int32
**Методы:**
- `List`1 GetTypicalRepresentations()`
- `Void SetTypicalRepresentations(ICollection`1 secondaryRepresentations)`
- `List`1 GetSecondaryFileRepresentations()`
- `Void SetSecondaryFileRepresentations(IEnumerable`1 secondaryFiles)`
- `Void SetMasterFile(FileObject masterFile)`
- `FileObject GetMasterFile()`
- `Void SetRepresentationTemplate(TypicalRepresentationsReferenceObject typicalRepresentation)`
- `TypicalRepresentationsReferenceObject GetRepresentationTemplate()`
- `List`1 GetLinkedFiles()` [has Async]
- `Void SetLinkedFiles(IEnumerable`1 files)`
- `FileReferenceObject AddLinkedFile(FileReferenceObject file)`
- `Boolean RemoveLinkedFile(FileReferenceObject file)`
- `Boolean IsActualVersionDownloaded()` [has Async]
- `String GetHeadRevision(String destinationPath)` [has Async]
- `String GetFileVersion(Int32 version, Boolean loadLinkedFiles) (+1)` [has Async]
- `Boolean DeleteFileVersion(Int32 version)` [has Async]
- `Boolean DeleteFromWorkingFolder()`
- `Void Export(String destinationPath, Boolean clearReadOnly)`
- `Void SetOpenningDocumentId(String path, Int32 objectId, Int32 referenceId)`
- `Void SetOpenDocumentContext(String path, Guid referenceObject, Guid hierarchyLink, Int32 referenceId, String filter, String mainFileTypeInStructure, Boolean isLaunchedPdm) (+5)`
- `OpenDocumentContext GetOpenDocumentContext(String path) (+1)`
- `Boolean GetOpenningObjectId(String path, Int32& objectId, Int32& referenceId)`
- `Void ClearOpenningDocumentId()`
- `Void SaveFileContext(Byte[] context, DocumentReferenceObject document)`
- `Byte[] FindFileContext(DocumentReferenceObject document)`
- `FileObject CreateCopy(String newName, FolderObject parent, ReferenceObjectSaveSet saveSet) (+1)`
- `FileObject CreateFileDuplicate(FolderObject parentFolder)`
- `Void MoveFileToFolder(FolderObject newParentFolder)`
- `Void CopyTo(FileObject destinationFile)`
- `Byte[] GetSigningReferenceObjectData()`

### `FilePreviewClient`
**Свойства:** Info: ServiceInfo
**Методы:**
- `IntPtr ShowFile(Int32 id, ShowFileContext fileContext, ClientCallContext context)` [has Async]
- `Void SetControlSize(Int32 id, Int32 width, Int32 height, ClientCallContext context)` [has Async]
- `Byte[] ExchangePluginData(String pluginModuleName, String pluginClassName, Int32 controlId, Byte[] data, ClientCallContext context)` [has Async]
- `Byte[] GenerateReport(String moduleName, String className, Byte[] data, ClientCallContext context)` [has Async]
- `Int32 GetImagePageCount(Int32 id, String filePath, ClientCallContext context)` [has Async]
- `Byte[] GetPreviewImage(Int32 id, String filePath, Int32 pageIndex, ClientCallContext context)` [has Async]
- `Boolean IsInstalledPreviewProgram(Int32 id, String extension, Boolean isAnyCPUMode, ClientCallContext context)` [has Async]
- `String GetCadServiceAddress(Int32 communication, Int32 dataSerializer, ClientCallContext context)` [has Async]
- `String GetTechnologyCadExchangeServiceAddress(Int32 communication, Int32 dataSerializer, String assemblyPath, String assemblyName, ClientCallContext context)` [has Async]
- `Boolean IsSupportSaving(Int32 id, ClientCallContext context)` [has Async]
- `Boolean SaveAs(Int32 id, String filePath, ClientCallContext context)` [has Async]
- `Void CloseFilePreviews(String file, ClientCallContext context)` [has Async]
- `Boolean IsDocumentChanged(Int32 id, ClientCallContext context)` [has Async]
- `Void SaveChanges(Int32 id, ClientCallContext context)` [has Async]
- `String GetFilePreviewInformation(Int32 id, ClientCallContext context)` [has Async]
- `Void Print(Int32 id, ClientCallContext context)` [has Async]
- `Tuple`2 ExecuteDocumentRequest(Int32 id, FilePreviewRequest request, ClientCallContext context)` [has Async]

### `FilePreviewCommand`
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `FilePreviewer`
**Свойства:** Guid: Guid, Name: String, AssemblyPath: String, AssemblyName: String, ErrorMessage: String, Platform: CPUDigitCapacity, Extensions: List`1, RunInCurrentProcess: Boolean
**Методы:**
- `Boolean TryLoadFilePreviewersFromFile(String filePath, FilePreviewer& filePreviewer) (+1)`
- `FilePreviewType GetFilePreviewType()`
- `FilePreviewType GetFilePreviewTypeByAssembly()`

### `FilePreviewerAttribute`
**Свойства:** CanChangeCaption: Boolean, IsSystem: Boolean, Caption: String, Value: Object, CanRemove: Boolean

### `FilePreviewerDescriptionAttribute`
**Свойства:** Name: String, ErrorMessage: String, Extensions: String, Platform: CPUDigitCapacity, SupportExecutionInCurrentProcess: Boolean, IsDefault: Boolean, Key: String, IgnoreInListPreviewModule: Boolean

### `FilePreviewers`
**Свойства:** Previewers: FilePreviewersCollection, Connection: ServerConnection, Interface: String, SharingType: SettingsSharingType, ParameterGroupId: Int32, SupportsViews: Boolean
**Методы:**
- `FilePreviewer GetFilePreviewer(Guid guid) (+1)`
- `FilePreviewType GetFilePreviewType(Guid customFilePreviewerGuid, Guid defaultFilePreviewerGuid, String extension)`

### `FilePreviewerTypeAttribute`
**Свойства:** CanChangeCaption: Boolean, Caption: String, IsSystem: Boolean, Value: Object, CanRemove: Boolean

### `FilePreviewImageManager`
**Методы:**
- `Byte[] GetImageData(String fileName, Int32 pageIndex, ServerConnection connection) (+1)`
- `Int32 GetImagePageCount(String fileName, ServerConnection connection)`

### `FilePreviewImageObjectValue`
**Свойства:** File: FileObject, PageIndex: Int32

### `FilePreviewImagePathItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, PageIndex: Int32, SupportSearchType: SupportSearchTypes

### `FilePreviewLoaderManager`
**Методы:**
- `IFilePreviewManager CreatePreviewByType(String type)`
- `IFilePreviewManager CreatePreviewFromAssembly(String assemblyPath, String assemblyName)`
- `T CreateHandler(String assemblyPath, String assemblyName, Type baseType, String previewKey)`
- `Type GetTypeByServiceBase(String assemblyPath, String assemblyName, String baseServiceName)`
- `String GetImageTempPath()`
- `Byte[] LoadImageFromFile(String filePath)`

### `FilePreviewManager`
**Методы:**
- `Int32 GetImagePageCount(String filePath)`
- `Byte[] GetPreviewImage(String filePath, Int32 pageIndex)`
- `Boolean IsInstalledPreviewProgram(Boolean isAnyCPUMode)`

### `FilePreviewRequest`
**Свойства:** ObjectCommands: List`1, SelectCommands: List`1

### `FilePreviewServer`
**Свойства:** Info: ServiceInfo, BackwardExchangePluginData: FeedbackWriter`2
**Методы:**
- `ValueTask`1 ShowFile(Int32 id, ShowFileContext fileContext, ServerCallContext context)`
- `ValueTask SetControlSize(Int32 id, Int32 width, Int32 height, ServerCallContext context)`
- `ValueTask`1 ExchangePluginData(String pluginModuleName, String pluginClassName, Int32 controlId, Byte[] data, ServerCallContext context)`
- `ValueTask`1 GenerateReport(String moduleName, String className, Byte[] data, ServerCallContext context)`
- `ValueTask`1 GetImagePageCount(Int32 id, String filePath, ServerCallContext context)`
- `ValueTask`1 GetPreviewImage(Int32 id, String filePath, Int32 pageIndex, ServerCallContext context)`
- `ValueTask`1 IsInstalledPreviewProgram(Int32 id, String extension, Boolean isAnyCPUMode, ServerCallContext context)`
- `ValueTask`1 GetCadServiceAddress(Int32 communication, Int32 dataSerializer, ServerCallContext context)`
- `ValueTask`1 GetTechnologyCadExchangeServiceAddress(Int32 communication, Int32 dataSerializer, String assemblyPath, String assemblyName, ServerCallContext context)`
- `ValueTask`1 IsSupportSaving(Int32 id, ServerCallContext context)`
- `ValueTask`1 SaveAs(Int32 id, String filePath, ServerCallContext context)`
- `ValueTask CloseFilePreviews(String file, ServerCallContext context)`
- `ValueTask`1 IsDocumentChanged(Int32 id, ServerCallContext context)`
- `ValueTask SaveChanges(Int32 id, ServerCallContext context)`
- `ValueTask`1 GetFilePreviewInformation(Int32 id, ServerCallContext context)`
- `ValueTask Print(Int32 id, ServerCallContext context)`
- `Void SetupBackwardExchangePluginData(FeedbackWriter`2 notify)`
- `ValueTask`1 ExecuteDocumentRequest(Int32 id, FilePreviewRequest request, ServerCallContext context)`

### `FilePreviewType`
**Свойства:** Extension: String, PreviewType: String, PreviewKey: String, AssemblyPath: String, AssemblyName: String, StandAlone: String, ErrorMessage: String, IsAnyCPU: Boolean, IsValidStandAlone: Boolean, NeedChangeStandAlone: Boolean, IsStandalone: Boolean
**Методы:**
- `String GetUsedStandAlone()`
- `Void ChangeUsedStandAlone()`

### `FileReference`
**Свойства:** Classes: FileTypes, FileServers: FileServerReference
**Методы:**
- `FileReferenceObject FindByPath(String path)` [has Async]
- `ICollection`1 FindByPaths(ICollection`1 paths)` [has Async]
- `FileReferenceObject FindByRelativePath(String relativePath)` [has Async]
- `ICollection`1 FindByRelativePaths(ICollection`1 relativePaths)` [has Async]
- `FolderObject Import(String sourceFolder, FolderObject destinationFolder) (+1)` [has Async]
- `FileObject AddFile(String fileName, Stream stream, FolderObject folder, Boolean executeCallBack) (+2)` [has Async]
- `List`1 AddFiles(IReadOnlyCollection`1 filesData, FolderObject folder, Boolean executeCallBack) (+1)` [has Async]
- `FolderObject CreateFolder(String description, String name, ImportParameters parameters)` [has Async]
- `FolderObject CreatePath(String path, FolderObject parentFolder, ImportParameters parameters)` [has Async]
- `Void GetHeadRevision(IEnumerable`1 files)` [has Async]
- `Boolean DeleteFilesVersions(List`1 files)` [has Async]
- `FileType GetFileType(String fileName, Boolean createIfNotExists)` [has Async]

### `FileReferenceObject`
**Свойства:** Class: FileType, Children: ReferenceObjectCollection`1, IsFile: Boolean, IsFolder: Boolean, IsFileContainer: Boolean, Parent: FolderObject, Server: FileServerParameter, Path: StringParameter, Name: StringParameter, Comment: StringParameter, Code: Int32Parameter, LevelOfDetail: Int32Parameter, LocalPath: String
**Методы:**
- `Boolean IsActualVersionDownloaded()` [has Async]
- `Void ValidateName(String name, Boolean isFolder)`
- `Void GetHeadRevision(Boolean loadLinkedFiles) (+2)` [has Async]
- `Boolean DeleteFromWorkingFolder()`
- `Void Export(String destinationPath, Boolean clearReadOnly)`
- `Boolean CanCopy(ParameterGroup relation)`

### `FileServerObject`
**Свойства:** Name: StringParameter, ServerAddress: StringParameter, Storage: StringParameter, IsDefault: Boolean

### `FileServerParameter`
**Методы:**
- `Int32 GetInt32()`
- `Int64 GetInt64()`
- `TypeCode GetTypeCode()`

### `FileServerReference`
**Методы:**
- `FileServerObject GetDefaultFileServer()` [has Async]
- `List`1 GetStorages(String serverAddress)`
- `Void SetDefaultFileServer(FileServerObject fileServer)`

### `FileShownHandler`
**Методы:**
- `Void Invoke(IFilePreviewContext context)`
- `IAsyncResult BeginInvoke(IFilePreviewContext context, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `FileSizeParameter`
**Свойства:** IsNull: Boolean, IsReadOnly: Boolean
**Методы:**
- `Int64 GetInt64()`
- `TypeCode GetTypeCode()`

### `FileType`
**Свойства:** Name: String, Classes: FileTypes, IsFolder: Boolean, IsFile: Boolean, IsFileContainer: Boolean, IsGRBFile: Boolean, CanContainChildren: Boolean, Attributes: FileTypeAttributes, Extension: String, Icon: IconImage, DefaultFilePreviewerGuid: Guid, CustomFilePreviewerGuid: Guid, DefaultFilePreviewerType: FilePreviewerTypes, CustomFilePreviewerType: FilePreviewerTypes

### `FileTypeAttributes`
**Свойства:** Extension: FileExtensionAttribute, DefaultFilePreviewer: FilePreviewerAttribute, DefaultFilePreviewerType: FilePreviewerTypeAttribute, ProtectedPreview: ProtectedPreviewAttribute

### `FileTypes`
**Свойства:** Folder: FileType, FileBase: FileType, TFlexCADFileBase: FileType, FileContainer: FileType
**Методы:**
- `FileType GetFileTypeByExtension(String extension)`
- `FileType CreateFileType(String name, String comment, String extension, FileType baseType, Guid customFilePreviewer, Guid defaultFilePreviewer, FilePreviewerTypes customFilePreviewerType, FilePreviewerTypes defaultFilePreviewerType) (+2)` [has Async]
- `Void ModifyFileType(FileType type, String name, String comment, String extension, Guid customFilePreviewer, Guid defaultFilePreviewer, FilePreviewerTypes customFilePreviewerType, FilePreviewerTypes defaultFilePreviewerType) (+1)` [has Async]
- `Void DeleteFileType(FileType type)` [has Async]

### `Filter`
**Свойства:** Connection: ServerConnection, Terms: TermGroup, Variables: VariableCollection, MainReference: ReferenceInfo, MasterGroup: ParameterGroup, SourceReference: ReferenceInfo, SerializationMode: ObjectSerializationMode, ValuesTable: DynamicDataTable
**Методы:**
- `Void Validate(MacroContext formulaContext)`
- `Boolean IsValid(MacroContext formulaContext)`
- `Boolean Match(Object obj, MacroContext formulaContext)`
- `ParameterInfoCollection GetParameters()`
- `IEnumerable`1 GetReferencePaths()`
- `Filter Parse(String str, ParameterGroup masterGroup)`
- `Boolean TryParse(String str, ParameterGroup masterGroup, Filter& filter)`
- `LoadOptionsParameters GetLoadOptions(MacroContext formulaContext)`
- `ConfigurationSettings GetConfigurationSettings(MacroContext formulaContext)`
- `String Serialize()`
- `Filter Deserialize(String xml, ServerConnection connection)`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`
- `Filter Merge(Filter firstFilter, Filter secondFilter, LogicalOperator logicalOperator) (+2)`
- `Void MergeVariables(Filter otherFilter)`
- `IReadOnlyCollection`1 GetSearchRulesOfElseGroup(Int32 elseGroupOrder) (+1)`
- `IReadOnlyCollection`1 GetSearchRules(TermGroupItem termGroupItem)`
- `IReadOnlyCollection`1 GetAllSearchRules(TermGroupItem termGroupItem)`
- `Void AddSearchRule(TermGroupItem termGroupItem, SearchRule searchRule)`
- `Void AddSearchRules(TermGroupItem termGroupItem, IEnumerable`1 searchRules)`
- `Void RemoveSearchRule(SearchRule searchRule)`
- `Void ChangeSearchRuleOwner(TermGroupItem termGroupItem, SearchRule searchRule)`
- `Void ChangeSearchRulesOwner(TermGroupItem termGroupItem, IEnumerable`1 searchRules)`

### `FilterData`
**Свойства:** Connection: ServerConnection, LinkGroupGuid: Guid, Name: String, IsCustom: Boolean, CustomFilter: Filter, FilterObject: ReferenceFilterObject, Filter: Filter
**Методы:**
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `FilterEditControlData`
**Свойства:** ReferenceGuid: Guid, ObjectListPath: String, ParameterPath: String
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `FilterExtensions`
**Методы:**
- `Filter ChangeBasePath(Filter filter, ReferencePath basePath)`
- `Filter MergeRepetitiveHierarchy(Filter filter)`
- `Filter AddAnalyzerToFormulaTerms(Filter filter)`
- `Filter MergeWithSearchRules(Filter first, Filter second)`
- `ValueTask`1 RunAndSetSpecialValues(Filter filter, MacroContext context, CancellationToken token)`
- `Filter CloneWithFormulaOptimization(Filter filter)`
- `Filter MassMerge(ICollection`1 filters, LogicalOperator logicalOperator)`
- `Filter OptimizeFilterStructure(Filter filter)`
- `Filter RemoveOnlyErrorTerms(Filter filter)`
- `ValueTuple`2 PartialMatchFilter(Filter filter, ReferenceObjectTerm termForRemove, Boolean isMatch)`
- `Nullable`1 MatchWithCustomPathGetter(Filter filter, DesktopObject value, Func`3 getter)`
- `Boolean CanMatchWithCustomPathGetter(Filter filter)`
- `Dictionary`2 RemoveSharedParts(Dictionary`2 sourceMap)`
- `Boolean IsEqualsByContent(Filter first, Filter second)`
- `Boolean IsNullOrEmpty(Filter filter)`
- `String VisualizeFilterRaw(Filter filter)`
- `String VisualizeFilter(Filter filter)`
- `Void SetDataTableValues(Filter filter, IReadOnlyCollection`1 parameterInfos, IReadOnlyCollection`1 values)`
- `List`1 GetTerms(Filter filter)`

### `FilterFormulaDetector`
**Методы:**
- `Boolean ContainsFormula(Filter filter)`

### `FilterParser`
**Свойства:** Filter: Filter
**Методы:**
- `Filter Parse(String str, Boolean throwOnError)`

### `FilterTerm`
**Свойства:** ParameterName: String, Value: Filter, Operator: ComparisonOperator
**Методы:**
- `Void Clear()`

### `FindInCollectionActivity`1`
**Свойства:** Values: InArgument`1, IsOne: InArgument`1, Body: ActivityFunc`2

### `FlagFieldInputDialog`
**Свойства:** TypeName: String, DefaultValue: InArgument`1

### `FloatDefaultRepositoryItemXMLData`
**Свойства:** MaxValue: Nullable`1, MinValue: Nullable`1, UseMinValue: Boolean, UseMaxValue: Boolean

### `FlowchartMacro`
**Свойства:** IsCompiled: Boolean, IsLimitedCountEntryPointParameters: Boolean, IsMethod: Boolean
**Методы:**
- `MacroValidationResults Validate()`
- `IEnumerable`1 GetEntryPoints()`

### `FlowchartMacroContext`
**Свойства:** MacroProvider: MacroProvider, Parameters: List`1, Result: Object, Sender: Object, Args: Object, FormulaCreator: IFormulaMacroCreator, Mode: FlowchartMacroWorkflowExecuteMode

### `FlowchartMacroHandlerManager`
**Методы:**
- `Boolean CanInvoke(ActivityEventHandler handler)`
- `Object Invoke(ActivityEventHandler handler, Object args)`

### `FlowchartMacroManager`
**Свойства:** Name: String, Code: String, IsCompiled: Boolean, AllowThrowOnValidate: Boolean, FormulaCreator: IFormulaMacroCreator
**Методы:**
- `ValidationResults Validate(String code, Activity& activity) (+2)`
- `Void ValidateAndThrowOnError(String name, String code)`
- `Object Calculate(String code, MacroContext context, Object[] parameters) (+5)`
- `Void Clear()`

### `FolderGroup`
**Свойства:** AsFolderGroup: FolderGroup

### `FolderMovedHandler`
**Методы:**
- `Void Invoke(MailFolder folder)`
- `IAsyncResult BeginInvoke(MailFolder folder, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `FolderObject`
**Свойства:** IsFolder: Boolean
**Методы:**
- `Void Rename(String newName)`
- `Void MoveTo(FolderObject otherFolder)`
- `Boolean SetParent(ReferenceObject parentObject)`
- `FileObject CreateFile(String source, String description, String name, FileType type, ImportParameters parameters)` [has Async]
- `FolderObject CreateFolder(String description, String name, ImportParameters parameters)` [has Async]
- `FileContainerObject CreateFileContainer(String source, String description, String name, ImportParameters parameters)` [has Async]
- `FolderObject CreatePath(String path, ImportParameters parameters)`
- `Void Load(Boolean recursive, Boolean getHeadRevisions, List`1& notActualFiles) (+1)` [has Async]
- `String GetHeadRevision(String destinationPath)` [has Async]
- `Boolean DeleteFromWorkingFolder()`
- `Void Export(String destinationPath, Boolean clearReadOnly, Boolean recursive) (+1)`

### `Font`
**Свойства:** FamilyName: String, Size: Int32, Style: FontStyles, Bold: Boolean, Underline: Boolean, Strikeout: Boolean, Italic: Boolean
**Методы:**
- `Boolean TryParse(String value, Font& font)`

### `FontSetting`
**Свойства:** FontFamily: String, Bold: Boolean, Italic: Boolean, FontSize: Double, FontColor: Int32
**Методы:**
- `FontSetting CreateDefault()`

### `ForActivity`1`
**Свойства:** From: InArgument`1, To: InArgument`1, Step: InArgument`1, Body: ActivityAction`1

### `ForEachActivity`1`
**Свойства:** Values: InArgument`1, Body: ActivityAction`1

### `FormulaAnalyzer`
**Свойства:** ParameterGroup: ParameterGroup
**Методы:**
- `FormulaAnalyzer Create(ReferenceInfo referenceInfo) (+2)`

### `FormulaElementReferenceObject`
**Свойства:** FormulaText: StringParameter
**Методы:**
- `String GetTestValue(String parameter)`

### `FormulaExtensions`
**Методы:**
- `Void AddToLoadSettings(FormulaMacro formulaMacro, LoadSettings loadSettings)`

### `FormulaMacro`
**Свойства:** Formula: String, IsReturnValue: Boolean, IsText: Boolean, IsSimpleText: Boolean, IsFlowchart: Boolean, ReturnType: Type, CodeOffset: Int32
**Методы:**
- `Void Clear()`
- `MacroValidationResults Validate()`
- `Object Calculate(MacroContext context)` [has Async]
- `String GetMacroCode()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `FormulaMacroEx`
**Свойства:** CodeOffset: Int32, Parameters: IReadOnlyCollection`1, IsReturnValue: Boolean, ReturnType: Type
**Методы:**
- `T Calculate(MacroContext context, Object[] args)` [has Async]
- `Void Clear()`

### `FormulaMacroExtensions`
**Методы:**
- `String GetShortCode(String formula, String text, Int32 maxNameLength)`

### `FormulaProcessor`
**Методы:**
- `String Replace(String text, MacroContext context, FormatType formatType, IFormulaMacroCreator formulaMacroCreator)`
- `ValueTuple`2 ReplaceWithExceptionsFixation(String text, MacroContext context, FormatType formatType, IFormulaMacroCreator formulaMacroCreator)`

### `FormulaRepositoryItemXMLData`
**Свойства:** FormulaCreatorType: String, ExtensionType: String

### `Fragment`
**Свойства:** Document: CadDocument, IsActive: Boolean
**Методы:**
- `VariableCollection GetVariables()`
- `Nullable`1 GetRealProperty(String propertyName)`
- `String GetTextProperty(String propertyName)`
- `PropertyCollection GetProperties()`
- `CadDocument OpenPart()`
- `CadDocument OpenLink()`

### `Fragment2DCommand`
**Свойства:** Priority: Int32, Angle: Int32
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `Fragment3D`
**Методы:**
- `LCSCollection GetLCSs()`
- `Nullable`1 CompareTo(String compareToDocument, LCS sourceLCS, String compareToDocumentLCS)`
- `Boolean IsCorrect()`

### `Fragment3DCommand`
**Свойства:** Z: Int32, Transformation: Double[]
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `FragmentCommandBase`
**Свойства:** Id: Guid, Name: String, File: String, Layer: String, X: Int32, Y: Int32, Variable: Variable
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `FrameworkExtensions`
**Методы:**
- `String GetDisplayNamespace(Type type)`
- `String GetDisplayName(Type type, ProgrammingLanguage language) (+1)`
- `String GetDisplayFullName(Type type, ProgrammingLanguage language)`
- `String GetFormattedName(Type type)`

### `FromMailField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `GetMailFieldStringValueDelegate`
**Методы:**
- `Boolean Invoke(MailItem item, String& value)`
- `IAsyncResult BeginInvoke(MailItem item, String& value, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(String& value, IAsyncResult result)`

### `GetMailFieldValueDelegate`
**Методы:**
- `Boolean Invoke(MailItem item, Object& value)`
- `IAsyncResult BeginInvoke(MailItem item, Object& value, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(Object& value, IAsyncResult result)`

### `GlobalParameter`
**Свойства:** Class: GlobalParameterType, Name: StringParameter, Comment: StringParameter, Category: StringParameter, Value: Parameter, AdministrativeAccessRequired: BooleanParameter

### `GlobalParameterAccessor`
**Свойства:** Item: DynamicType

### `GlobalParameterReference`
**Свойства:** Instance: GlobalParameterReference, Classes: GlobalParameterTypes, Item: GlobalParameter, GlobalCalendar: CalendarReferenceObject, WorkingFolderPath: FormulaMacro, DisableInplaceEdit: Boolean
**Методы:**
- `GlobalParameter Find(String name)` [has Async]
- `Boolean GetIsStageCommentsRequired()` [has Async]
- `Boolean IsOmitHasChildrenCheckEnabled(Boolean catalog)` [has Async]
- `Boolean GetShowAnnotateCommand()` [has Async]

### `GlobalParameterType`
**Свойства:** Classes: GlobalParameterTypes, IsString: Boolean, IsInt: Boolean, IsReal: Boolean, IsBoolean: Boolean, IsDateTime: Boolean

### `GlobalParameterTypes`
**Свойства:** String: GlobalParameterType, Int: GlobalParameterType, Real: GlobalParameterType, Boolean: GlobalParameterType, DateTime: GlobalParameterType

### `GrbFileObject`
**Методы:**
- `ICollection`1 LoadTfrFiles()`
- `Boolean HasTfrFilesOnServer()`

### `GroupAssignmentReferenceObject`
**Свойства:** AutomaticCalculation: BooleanParameter, AutoCalculation: Boolean, IsModified: Boolean, IsChanged: Boolean
**Методы:**
- `ExecutorCandidatesManager GetExecutorsManager()`
- `Void RecalculateProgress()`
- `GroupAssignmentReferenceObject GetGroupAssignment()`
- `Void ChangeAutoCalculation(Boolean autoCalculation)`

### `GroupCache`
**Методы:**
- `Void Clear()`
- `Boolean IsUnidirectionalLink(ParameterGroup group, ParameterGroup prefix)`
- `Boolean ContainsInClass(ClassObject classObject, Guid linkId, Boolean isToAny)`

### `GroupFieldInputDialog`
**Свойства:** TypeName: String

### `GroupObject`
**Свойства:** Description: GroupDescription, AccessibleInCurrentConfiguration: Boolean

### `GroupPathItem`
**Свойства:** Group: ParameterGroup, Path: ReferencePath, Name: String, Type: PathItemType, Icon: IconImage, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `GuidDomainObject`
**Свойства:** Guid: Guid

### `GuidDomainObjectCollection`1`
**Свойства:** Connection: ServerConnection
**Методы:**
- `T Find(Guid guid)`
- `Int32 IndexOf(Guid guid)`
- `Boolean Contains(Guid guid)`

### `GuidDomainObjectComparer`
**Методы:**
- `Int32 Compare(GuidDomainObject x, GuidDomainObject y)`

### `GuidKeyElement`
**Свойства:** Id: Int32, Guid: Guid

### `GuidNameElement`
**Свойства:** Name: String, Guid: Guid

### `GuidParameter`
**Свойства:** IsEmpty: Boolean
**Методы:**
- `Guid GetGuid()`
- `TypeCode GetTypeCode()`
- `Boolean TryParse(String s, Guid& result)`

### `GuidTool`
**Свойства:** Guid: Guid, IsGroupedMethod: Boolean

### `HandlerActivity`2`
**Свойства:** Body: ActivityAction`2

### `HierarchyGroupPathItem`
**Свойства:** Name: String, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `HierarchyLink`
**Методы:**
- `HierarchyLink CreateInstance(ComplexHierarchyLink hierarchyLink, MacroContext context)`

### `HierarchyLinkAccessor`
**Свойства:** Item: DynamicType, Changing: Boolean [RU: Редактируется], IsDeleted: Boolean [RU: Редактируется], Parameter: ParameterAccessor [RU: Параметр], ParentObject: RefObj, ChildObject: RefObj, LinkedObject: LinkedObjectAccessor`1, LinkedObjects: LinkedObjectsAccessor`2, Reference: ReferenceAccessor [RU: Справочник], РодительскийОбъект: Объект [RU only], ДочернийОбъект: Объект [RU only], СвязанныйОбъект: LinkedObjectAccessor`1 [RU only], СвязанныеОбъекты: LinkedObjectsAccessor`2 [RU only]
**Методы:**
- `Void AddLink(String linkName, ObjectAccessor refObj)` [RU: Подключить]
- `Void RemoveLink(String linkName, ObjectAccessor refObj) (+1)` [RU: Подключить]
- `Void Save()` [RU: Сохранить]
- `Void BeginChanges()` [RU: Сохранить]
- `Void CancelChanges()` [RU: Сохранить]
- `Boolean Delete()` [RU: Сохранить]
- `HierarchyLink Copy(Boolean copyApplicability, String[] skipParameters)` [RU: Подключить]
- `HierarchyLink FullCopy(ObjectAccessor newParent, ObjectAccessor newChild, String[] copyLinks) (+1)` [RU: Отключить]
- `Void Изменить()` [RU alternative]
- `Void ОтменитьИзменения()` [RU alternative]
- `Boolean Удалить()` [RU alternative]
- `Подключение Копия(Boolean копироватьПрименяемость, String[] пропущенныеПараметры)` [RU alternative]
- `Подключение ПолнаяКопия(ObjectAccessor новыйРодительскийОбъект, ObjectAccessor новыйДочернийОбъект, String[] копируемыеСвязи)` [RU alternative]

### `HierarchyLinkAccessorExtensions`
**Методы:**
- `ObjectAccessor GetParentObject(HierarchyLinkAccessor hierarchyLink)`
- `ObjectAccessor GetChildObject(HierarchyLinkAccessor hierarchyLink)`

### `HierarchyLinkAccessorList`1`
**Свойства:** Item: T, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `HierarchyLinkList`
**Методы:**
- `HierarchyLinkList CreateInstance(IEnumerable`1 links, MacroContext context)`

### `HierarchyLinkMatchesReference`
**Свойства:** Classes: HierarchyLinkMatchesTypes

### `HierarchyLinkMatchesReferenceObject`
**Свойства:** Class: HierarchyLinkMatchesType, Name: StringParameter, Action: Int32Parameter
**Методы:**
- `NomenclatureHierarchyLink GetSourceHierarchyLink(DesignContextObject designContext, Boolean applyDesignContext, Boolean applyDate)`
- `NomenclatureHierarchyLink GetAddedHierarchyLink(DesignContextObject designContext, Boolean applyDesignContext, Boolean applyDate)`
- `NomenclatureHierarchyLink GetDeletedHierarchyLink(DesignContextObject designContext, Boolean applyDesignContext, Boolean applyDate)`

### `HierarchyLinkMatchesType`
**Свойства:** Classes: HierarchyLinkMatchesTypes, IsHierarchyLinkMatches: Boolean

### `HierarchyLinkMatchesTypes`
**Свойства:** MatchesType: HierarchyLinkMatchesType

### `HistoryFilters`
**Свойства:** Connection: ServerConnection, FromDateTime: Nullable`1, ToDateTime: Nullable`1, FromChangelistNumber: Int32, ToChangelistNumber: Int32, HostName: String

### `HtmlHelper`
**Методы:**
- `String InsertFirstString(String htmlString, String str) (+1)`
- `String InsertLastString(String htmlString, String str)`
- `String GetHtmlBodyText(String htmlString)`
- `String ReplaceNewLineSymbols(String str)`
- `String InsertIntoEmptyHtml(String str)`

### `HyperLink`
**Свойства:** Text: String, Resource: String, CanContainChildren: Boolean

### `IAdditionalSettings`
**Свойства:** Parameters: Dictionary`2

### `IAssignmentChangeManager`1`
**Методы:**
- `Boolean CanChangeParameter(TAssignment assignment, Parameter parameter, Object newValue)`
- `Boolean CanChangeLink(TAssignment assignment, LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`

### `IAssignmentReferenceHelper`
**Свойства:** DisableUserCreateObject: Boolean

### `IBusinessProcessesAccessor`
**Методы:**
- `Boolean Run(MacroContext context, String name, IEnumerable`1 objects, IEnumerable`1 appendantObjects, Dictionary`2 variables, Boolean showDialog, String variablesTemplate, String begin, Func`5 createRunBusinessProcessContext)`
- `Boolean RunLinear(MacroContext context, String prototypeName, IEnumerable`1 objects, Boolean showDialog, Func`3 showLinearBusinessProcessDialog)`
- `Boolean Edit(MacroContext context, String name, Dictionary`2 variables)`
- `Void Complete(MacroContext context, String process, String state, String solution, IEnumerable`1 objects, String comment)`

### `ICachedToDeleteReferenceObjects`
**Методы:**
- `Void CacheToDelete(ICollection`1 referenceObjects, DesktopObjectPacketSet`1 packetSet)`

### `ICADObject`
**Свойства:** ID: UInt32, Name: String, DisplayName: String, CADType: CADObjectTypes
**Методы:**
- `String GetSearchIdentifier()`
- `Void Accept(ICadObjectVisitor visitor)`

### `ICadObjectVisitor`
**Методы:**
- `Void Visit(CADArea cadObject) (+4)`

### `ICalculateParameterValue`
**Методы:**
- `Object Calculate(CalculationInfo parameter, ICalendarAppointment categorySetting)`

### `ICalculateParameterValue`1`
**Методы:**
- `T Calculate(CalculationInfo parameter)`

### `ICalendarAppointment`
**Свойства:** Header: String, Comment: String, Start: DateTime, End: DateTime, AllDay: Nullable`1, Key: Int32, LabelId: Int32, Status: Int32, Setting: CalendarCategorySettingBase, CanChangeTimeInterval: Boolean
**Методы:**
- `Void SetMacroContext(MacroContext context)`
- `MacroContext GetMacroContext()`
- `Object GetCoreObject()`
- `Void Release()`

### `ICalendarCategorySettingParameter`1`
**Методы:**
- `T GetValue(ICalendarAppointment calendarAppointment)`
- `Void SetValue(ICalendarAppointment calendarAppointment, Object value)`

### `ICodeEditBaseExtension`
**Свойства:** Name: String

### `ICodeEditExtension`
**Свойства:** TextCodeEditorExtension: ITextCodeEditExtension, FlowchartCodeEditorExtension: IFlowchartCodeEditExtension, FormulaCreator: IFormulaMacroCreator

### `ICodeEditProvider`
**Свойства:** FormulaCreator: IFormulaMacroCreator, MacroContextCreator: IMacroContextCreator

### `ICodeEditWithExtensionProvider`
**Свойства:** Extension: ICodeEditExtension, ContextObject: ReferenceObject

### `ICommandVisitor`
**Методы:**
- `Void Visit(Fragment3DCommand command) (+3)`

### `ICommonDialog`
**Свойства:** Caption: String, InitialDirectory: String
**Методы:**
- `Boolean Show()`

### `ICommonFileDialog`
**Свойства:** FilterIndex: Int32, Filter: String, FileNames: String[], FileName: String, AddExtension: Boolean, DefaultExt: String
**Методы:**
- `Stream OpenFile()`

### `IconAccessor`
**Свойства:** IsSvgIcon: Boolean [RU: ВекторныйФормат], SvgIcon: Byte[] [RU: Векторная], Icon: Image [RU: Растровая]

### `IconImage`
**Свойства:** IsSvgImage: Boolean, SvgSource: Byte[], IconSource: Byte[], InternalIcon: Icon, SmallImage: Image, MediumImage: Image, LargeImage: Image, ImageSource: ImageSource, SmallIconSize: Size, MediumIconSize: Size, LargeIconSize: Size, IsLargeFont: Boolean, Key: String
**Методы:**
- `Void Save(Stream outputStream)`
- `Byte[] Serialize()`
- `IconImage Get(String name, ResourceManager iconOwner)`
- `Single GetScaleMetric()`

### `IconParameter`
**Свойства:** Value: IconImage, IsNull: Boolean
**Методы:**
- `IconImage GetIcon()`
- `Byte[] GetByteArray()`
- `TypeCode GetTypeCode()`

### `IconsLoader`
**Методы:**
- `Dictionary`2 LoadParameterGroupIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]
- `Dictionary`2 LoadClassObjectIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]
- `Dictionary`2 LoadCatalogFolderIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]
- `Dictionary`2 LoadDialogGroupIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]
- `Dictionary`2 LoadDialogPageIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]
- `Dictionary`2 LoadWorkingPageIcons(ServerConnection connection, ICollection`1 objectIds) (+1)` [has Async]

### `ICounterSelectionRule`
**Методы:**
- `String Run(IDictionary`2 calculatedObjects)`

### `IDataExchangeAccessor`
**Методы:**
- `DataExchangeResultsAccessor Run(DataExchangeRunSettings runSettings) (+1)`
- `DataTransferResultsAccessor From(MacroContext context, List`1 results)`
- `MasterServerMacroProvider Connect(MacroContext context, String server)`

### `IDataExchangeObjectWithIcon`
**Свойства:** Icon: Byte[]

### `IEntryPoint`
**Свойства:** Name: String, Title: String, ReturnType: Type
**Методы:**
- `IEntryPointParameter[] GetParameters()`

### `IEntryPointParameter`
**Свойства:** Name: String, Title: String, Type: Type, IsOptional: Boolean, DefaultValue: Object

### `IEntryPointProvider`
**Методы:**
- `IEnumerable`1 GetEntryPoints()`

### `IEntryPointWithConnectionProvider`
**Методы:**
- `IEnumerable`1 GetEntryPoints(ServerConnection connection)` [has Async]

### `IFileObjectEditingState`
**Свойства:** CanEditDocument: Boolean

### `IFilePreviewContext`
**Свойства:** LastModificationTime: DateTime, FilePath: String, FileExtension: String, Parameters: String, CustomFilePreviewerGuid: Guid, DefaultFilePreviewerGuid: Guid, ShowToolsButtons: Boolean, LinkedObjectId: Int32, LinkedReferenceId: Int32, LinkedObjectGuid: Guid, HierarchyLink: Guid, EnablePrint: Boolean, AsyncModeSupported: Boolean, ConfigurationSettings: String, ObjectContext: String
**Методы:**
- `Void GenerateFile()`
- `Boolean IsChanged(IFilePreviewContext filePreviewContext)`

### `IFilePreviewContextLinkedInstance`
**Свойства:** LinkedObjectInstanceGuid: Guid

### `IFilePreviewControl`
**Свойства:** FilePreviewInformation: String, SupportsSaving: Boolean
**Методы:**
- `Void ShowFile(String fileName, Object context) (+1)`
- `Void ShowFileWithParameters(String fileName, String parameters)`
- `Boolean SaveAs(String filePath)`

### `IFilePreviewManager`
**Методы:**
- `Int32 GetImagePageCount(String filePath)`
- `Byte[] GetPreviewImage(String filePath, Int32 pageIndex)`
- `Boolean IsInstalledPreviewProgram(Boolean isAnyCPUMode)`

### `IFilePreviewPlugin`
**Методы:**
- `Byte[] ExchangeData(Object control, Byte[] data, IFilePreviewPluginCallback callback)`

### `IFilePreviewPluginCallback`
**Методы:**
- `Task`1 BackwardExchangeData(String pluginModuleName, String pluginClassName, Byte[] data)`

### `IFlowchartCodeEditExtension`
**Свойства:** DefaultSupportedTypes: Type[], AccessorTypes: AccessorDefaultType[], ToolboxController: IToolboxController, ToolIcons: Dictionary`2, Namespaces: NamespaceInfo[], ReplaceArguments: Dictionary`2, ContextVariables: ContextVariableInfo[], ObsoleteActivityTypes: Type[], ObsoleteContextVariables: ContextVariableInfo[]

### `IFormulaMacroCreator`
**Методы:**
- `FormulaMacro CreateFormula(String formula)`

### `IGetNumberStrategy`
**Методы:**
- `String GetNumber(CodifierReferenceObject autoNumeratorReferenceObject, ReferenceObject contextReferenceObject)`

### `IInfoAttribute`
**Свойства:** Language: Language, Name: String, Key: String

### `IInputDialog`
**Свойства:** Caption: String, Height: Double, Width: Double, FieldValueChangedFlowchartHandler: ActivityEventHandler
**Методы:**
- `Void AddIntegerField(String name, Int32 value, Boolean required)`
- `Void AddDoubleField(String name, Double value, Int32 decimalPlaces, Boolean required)`
- `Void AddStringField(String name, String mask, MaskType maskType, String value, Boolean multiline, Boolean required, Boolean useAllWidth, Int32 lineCount, Boolean useSpellChecker) (+2)`
- `Void AddDateField(String name, DateTime value, Boolean required, Int32 mode, String mask)`
- `Void AddFlagField(String name, Boolean value, Boolean required, Boolean useAllWidth)`
- `Void AddSelectValueField(String name, Object value, Boolean required, Object[] values)`
- `Void AddMultiselectFromList(String name, Object[] values, Boolean required)`
- `Void AddSelectReferenceField(String name, Object value, Boolean required)`
- `Void AddSelectFromReferenceField(String name, String reference, String parameter, Object value, Boolean required, String filter, Guid rootObjectGuid) (+3)`
- `Void AddMatchReferenceObjectField(String name, String reference, String parameter, String relevanceContext, Object value, Boolean required, String filter, String viewName, Boolean useContainsFilter) (+3)`
- `Void AddButton(String name, Action`1 handler, Nullable`1 width) (+2)`
- `Void AddPanel(String name, String header, Double height, Boolean verticalScrollBar, Boolean autoVerticalScrollBar)`
- `Void AddFieldsToPanel(String panelName, String[] fieldName)`
- `Boolean Show(MacroContext context)`
- `Object GetValue(String name)`
- `Void SetValue(String name, Object value)`
- `Void SetIcon(IconImage icon)`
- `Void AddComment(String name, String comment)`
- `Void AddGroup(String text)`
- `Int32 AddPicture(MacroContext context, String parameterName, Int32 lineCount) (+1)`
- `Void ChangePicture(Int32 position, ObjectAccessor refObject, String parameterName)`
- `Int32 AddIcon(ObjectAccessor refObject, String parameterName, Int32 lineCount)`
- `Void ChangeIcon(Int32 position, ObjectAccessor refObject, String parameterName)`
- `Void AddText(String text, Int32 lineCount) (+1)`
- `Void SetSize(Int32 width, Int32 height)`
- `Void SetElementVisibility(String elementName, Boolean visible) (+1)`
- `Void SetElementEnabled(String elementName, Boolean enabled) (+1)`
- `Void SetElementRequired(String elementName, Boolean required) (+1)`
- `Void SetElementFilter(String elementName, String filter) (+1)`
- `Void SetScrollBarsVisibility(Boolean verticalScrollBar, Boolean autoVerticalScrollBar)`

### `IInteractiveCADControl`
**Свойства:** Handle: IntPtr, SelectedObject: CADObjectInfo, SelectedObjects: IEnumerable`1, Document: SharedDocument, IsInternalControlDisposed: Boolean
**Методы:**
- `Void SelectCadObjects(IReadOnlyCollection`1 items)`
- `Void ChangeTree(String configuration)`
- `InteractiveCADVersionInfo GetVersion()`
- `Void BeginSelectionSession(CADObjectTypes[] selectableTypes)`
- `Void EndSelectionSession()`
- `Void ShowStepText(String str)`
- `IEnumerable`1 GetSelectionAllObjects()`
- `Void SetSelectionFragments(Guid[] guids)`
- `Void SetCADSelection(Boolean enable)`

### `IInteractiveCadControlProvider`
**Свойства:** SynchronizationContext: SynchronizationContext
**Методы:**
- `IInteractiveCADControl FindInteractiveControl(IntPtr ptr)`
- `Boolean LoadApi()`

### `IInteractiveFilePreviewControl`
**Методы:**
- `Boolean IsDocumentChanged()`
- `Void SaveChanges()`
- `Void ShowVirtualAssembly(ShowFileContext showFileContext)`

### `ILayoutItem`
**Свойства:** Name: String
**Методы:**
- `Void Reload()` [has Async]

### `ILayoutItemWithFilter`
**Методы:**
- `Void SetFilter(Filter filter) (+1)`
- `Void SetFilterIsActive(Boolean value)`

### `ILayoutItemWithReferenceGroup`
**Методы:**
- `ParameterGroup GetReferenceGroup()`

### `ILayoutItemWithView`
**Методы:**
- `Void SetView(ISettingsView view)` [has Async]
- `ReadOnlyCollection`1 GetViews()`
- `ISettingsView GetCurrentView()`

### `ILinkAdditionalSettingsOwner`
**Свойства:** ParameterGroup: ParameterGroup, ClassOfGroup: ClassObject

### `IMacroContextCreator`
**Методы:**
- `MacroContext CreateContext(Object owner)`

### `IMacroContextUserInteraction`
**Методы:**
- `Void Initialize(MacroContext context)`
- `Void ShowMessage(String caption, String text, Object[] args)`
- `Boolean ShowQuestion(String text)`
- `Nullable`1 ShowQuestionWithCancel(String text)`
- `Boolean ShowObjectPropertyDialog(ObjectAccessor object, String caption, Boolean inNewWindow, Boolean showConfirmationOnCancel) (+2)`
- `ClassObject ShowClassObjectSelectionDialog(ParameterGroup parameterGroup, String caption)`
- `Void OpenReferenceWindowCore(Reference reference, Filter filter, ReferenceObject rootObject, String viewName, CatalogFolder catalogFolder)`
- `Void OpenProjectEditor(IEnumerable`1 projects, String view, String style)`
- `Void OpenWorksUsage(ReferenceObject project, String view, String style)`
- `Void OpenResourcesUsage(ReferenceObject projectElement, ReferenceObject resource, String view, String style)`
- `IInputDialog CreateInputDialog()`
- `IOpenFileDialog CreateOpenFileDialog()`
- `IOpenFolderDialog CreateOpenFolderDialog()`
- `ISaveFileDialog CreateSaveFileDialog()`
- `ISelectObjectDialog CreateSelectObjectDialog(ReferenceInfo referenceInfo) (+1)`
- `ISelectObjectsFromReferencesDialog CreateSelectObjectsFromReferencesDialog()`
- `ISelectListObjectsDialog CreateSelectListObjectsDialog(List`1 listObjects)`
- `ISelectClassObjectsDialog CreateSelectClassObjectsDialog(ParameterGroup parameterGroup)`
- `IWaitingDialog CreateWaitingDialogCore()`
- `ReferenceObject[] GetSelectedObjects(ILayoutItem layoutItem) (+1)`
- `ComplexHierarchyLink[] GetSelectedHierarchyLinks(ILayoutItem layoutItem) (+1)`
- `Void RefreshReferenceWindow()`
- `Void RefreshReferenceObjects(ICollection`1 objects)`
- `IWindow GetCurrentWindow()`
- `IProgressIndicator GetProgressIndicator()`
- `Object CreateRunBusinessProcessContext(ReferenceObject procedure, IEnumerable`1 objects, IEnumerable`1 appendantObjects, ReferenceObject beginState)`
- `Boolean ShowLinearBusinessProcessDialog(ReferenceObject procedure, IEnumerable`1 objects)`
- `Boolean ShowDataExchangeDialog(ReferenceObject masterDataBindingObject, Object dataSettings)`
- `Void ShowDataExchangeWaitDialog(ReferenceObject masterDataBindingObject, Object dataSettings)`
- `Void RunOnUIThread(Action action)`
- `Void OpenFilePreview(IReadOnlyCollection`1 files)`
- `Void OpenWorkingPage(WorkingPage workingPage)`

### `ImageExtensions`
**Методы:**
- `Icon RenderToIcon(Image image) (+1)`
- `Image GetResizedImage(Image source, Int32 width, Int32 height)`

### `ImageParameter`
**Методы:**
- `Image GetImage()`
- `TypeCode GetTypeCode()`

### `ImageReference`
**Методы:**
- `ImageReferenceObject ImportIcon(String file)`

### `ImageReferenceObject`
**Свойства:** Name: StringParameter, Icon: IconParameter, Image: ImageParameter, IsIcon: Boolean, IsImage: Boolean
**Методы:**
- `String GetFilterExtensions()`
- `Void SaveToFile(String fileName)`

### `IMailFolder`
**Свойства:** Guid: Guid
**Методы:**
- `Int32 GetId()`
- `IEnumerable`1 GetMailItems(Filter filter)`
- `String GetFolderName()`
- `MailItemFolder GetMailItemFolder()`
- `IconImage GetIcon()`

### `IMap`
**Свойства:** ServerName: String, Login: String, SessionPassword: String, Password: String, SSLMode: SSLMode, MoveToDeleted: Boolean, Port: Int32, IsEmpty: Boolean, AskPassword: Boolean, IsModified: Boolean
**Методы:**
- `IMapSettings ToServerSettings()`

### `ImapAccount`
**Свойства:** ImapPasswordAction: SessionPasswordDelegate, SmtpPasswordAction: SessionPasswordDelegate, IsLoggedIn: Boolean, IsImapSessionPasswordEntered: Boolean, IsSmtpSessionPasswordEntered: Boolean, Guid: Guid, CanSaveMessagesOnServer: Boolean, SaveOnServer: Boolean, ParentId: Int32, IsModified: Boolean, Inbox: MailFolder, SentItems: MailFolder, DeletedItems: MailFolder, Smtp: Smtp, Imap: IMap, Email: String, UserName: String, InboxFolderName: String, SentFolderName: String, DeletedFolderName: String, DraftsFolderName: String, Name: String
**Методы:**
- `Boolean CheckImapConnection(String serverName, Int32 port, SSLMode sslMode, String login, String password)`
- `Boolean IsSystemFolder(MailItemFolder folder)`
- `EmailErrorType Relogin(String password)`
- `EmailError CheckConnection()`
- `Void ChangeImapPassword(String password, Boolean save)`
- `Void ChangeSmtpSessionPassword(String password, Boolean save)`
- `Void ChangeImapSessionPassword(String password, Boolean save)`
- `String[] GetServerFolders()`
- `Char GetFolderSeparator()`
- `Void Reconnect()`
- `Boolean SaveFolder(MailItemFolder folder)`
- `Boolean MoveMailFolderTo(MailFolder folder, MailFolder newParentFolder)`
- `Boolean DeleteFolder(MailItemFolder folder, Boolean useAccountSettings)`
- `Boolean MoveMessagesTo(MailFolder toFolder, IEnumerable`1 messages)`
- `Boolean DeleteMessages(IEnumerable`1 messages, Boolean useAccountSettings)`
- `String GetLogFilePath()`
- `MailFolder CreateRootFolder()`
- `Void CheckServerFolders()` [has Async]
- `Boolean IsCheckFolderMessages(MailFolder folder)`
- `Int32 GetCheckingFolderMaxMessagesCount(MailFolder folder)`
- `Boolean IsCheckAnyFolderMessages()`
- `Void CheckFoldersMessages()` [has Async]
- `Void CheckFolderMessages(MailFolder folder, CancellationToken token)` [has Async]
- `List`1 GetRootFolders()` [has Async]
- `MailMessage FindMessage(Int32 globalId, Int32 folderId)`
- `Void SetName(String name)`
- `Boolean CanDelete()`
- `Boolean Delete()`
- `String GetFolderPath(MailFolder folder, String folderName)`
- `EmailError SendTestMessage()`
- `Void SendMessage(MailMessage message)` [has Async]
- `Void SendMessages()` [has Async]
- `Void Save()` [has Async]
- `Boolean SetMessagesRead(IEnumerable`1 messages)`
- `Boolean SetMessagesUnread(IEnumerable`1 messages)`
- `Boolean SetFolderRead(MailItemFolder mailItemFolder)`
- `Boolean SetFolderUnread(MailItemFolder mailItemFolder)`
- `Void RegisterWatcher(ImapAccountWatcher watcher)`
- `Void UnregisterWatcher(ImapAccountWatcher watcher)`

### `ImapAccountTemplate`
**Свойства:** Connection: ServerConnection, CopyAccountUserName: Boolean, CopyAccountEmail: Boolean, CopyAccountLogin: Boolean, Smtp: Smtp, Imap: IMap, Email: String, UserName: String, Id: Int32, Name: String, IsModified: Boolean, Accounts: ReadOnlyCollection`1
**Методы:**
- `Void CopyToAccounts()`
- `ImapAccount AddUser(User user)` [has Async]
- `Boolean RemoveUserAccount(ImapAccount account)`
- `Void Save()` [has Async]
- `Boolean Delete()`

### `ImmediatelyTrigger`
**Свойства:** Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `IModelCallback`
**Методы:**
- `Boolean OnDesktopOperation(DesktopOperationInfo operation, Object context)` [has Async]
- `Boolean CanOverwriteFile(String filePath)`
- `CallbackDialogResult ShowMessage(String message, MessageDialogType type)`
- `Boolean IsWorkerThread()`

### `ImportCallback`
**Методы:**
- `Boolean Invoke(String[] messages, Int64 counter, Int64 totalCount)`
- `IAsyncResult BeginInvoke(String[] messages, Int64 counter, Int64 totalCount, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `ImportCatalogSettings`
**Свойства:** Guid: Guid, CatalogFolders: Guid[]

### `ImportClassSettings`
**Свойства:** Guid: Guid

### `ImportDialogGroupSettings`
**Свойства:** Guid: Guid, DialogPages: IReadOnlyCollection`1, HasDialogPages: Boolean
**Методы:**
- `Boolean AddDialogPage(Guid guid)`
- `Void AddDialogPages(Guid[] guids) (+1)`
- `Boolean ContainsDialogPage(Guid guid)`
- `Boolean RemoveDialogPage(Guid guid)`

### `ImportErrorObjectsCallback`
**Методы:**
- `Void Invoke(List`1 errors)`
- `IAsyncResult BeginInvoke(List`1 errors, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ImportFileCallback`
**Методы:**
- `Boolean Invoke(String filePath)`
- `IAsyncResult BeginInvoke(String filePath, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `ImportLinkSettings`
**Свойства:** Guid: Guid, IncludeAllProperties: Boolean, Properties: IReadOnlyCollection`1
**Методы:**
- `Boolean AddProperty(ParameterProperties property)`
- `Void AddProperties(ParameterProperties[] properties) (+1)`
- `Boolean ContainsProperty(ParameterProperties property)`
- `Boolean RemoveProperty(ParameterProperties property)`

### `ImportModeExtensions`
**Методы:**
- `String GetName(ImportMode mode)`

### `ImportObjectsAsyncCallback`
**Методы:**
- `ValueTask Invoke(Dictionary`2 importedObjects, CancellationToken token)`
- `IAsyncResult BeginInvoke(Dictionary`2 importedObjects, CancellationToken token, AsyncCallback callback, Object object)`
- `ValueTask EndInvoke(IAsyncResult result)`

### `ImportObjectsCallback`
**Методы:**
- `Void Invoke(Dictionary`2 importedObjects)`
- `IAsyncResult BeginInvoke(Dictionary`2 importedObjects, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ImportOptions`
**Свойства:** FileName: String, DataStream: Stream, SearchFile: Func`2, Mode: ImportMode, IncludeStructure: Boolean, IncludeObjects: Boolean, IncludeViews: Boolean, IncludeDialogs: Boolean, IncludeAccesses: Boolean, IncludeApplications: Boolean, IncludeSigningParameters: Boolean, DisableNesting: Boolean, SynchronizeObjects: Boolean, Callback: ImportCallback, ObjectsCallback: ImportObjectsCallback, ObjectsAsyncCallback: ImportObjectsAsyncCallback, ErrorObjectsCallback: ImportErrorObjectsCallback, SynchronizeInvoke: ISynchronizeInvoke

### `ImportParameterGroupSettings`
**Свойства:** Guid: Guid

### `ImportParameters`
**Свойства:** DestinationFolder: FolderObject, Recursive: Boolean, CreateClasses: Boolean, AutoCheckIn: Boolean, UpdateExistingFiles: Boolean, ImportedObjects: List`1, ImportedFiles: List`1, ImportFileCallback: ImportFileCallback, FileExistsCallback: ImportFileCallback, RequiredParametersExceptionCallback: Func`2

### `ImportParameterSettings`
**Свойства:** Guid: Guid

### `ImportReferenceSettings`
**Свойства:** IncludeAllAccesses: Boolean, Accesses: IReadOnlyCollection`1, HasAccesses: Boolean, Catalogs: IReadOnlyCollection`1, HasCatalogs: Boolean, IncludeAllClasses: Boolean, Classes: IReadOnlyCollection`1, HasClasses: Boolean, MasterGroup: DataExchangeParameterGroup, MasterGroupGuid: Guid, DialogGroups: IReadOnlyCollection`1, HasDialogGroups: Boolean, IncludeAllEventHandlers: Boolean, HandlerEvents: IReadOnlyCollection`1, HasEventHandlers: Boolean, IncludeAllEvents: Boolean, Events: IReadOnlyCollection`1, HasEvents: Boolean, IncludeAllLinks: Boolean, Links: IReadOnlyCollection`1, HasLinks: Boolean, IncludeAllObjectLists: Boolean, ObjectLists: IReadOnlyCollection`1, HasObjectLists: Boolean, IncludeAllParameterGroups: Boolean, ParameterGroups: IReadOnlyCollection`1, HasParameterGroups: Boolean, IncludeAllParameters: Boolean, Parameters: IReadOnlyCollection`1, HasParameters: Boolean, Stages: HashSet`1, Transitions: HashSet`1, HasStages: Boolean, HasTransitions: Boolean, IsSchemeExists: Boolean, IncludeAllSignatureTypes: Boolean, SignatureTypes: IReadOnlyCollection`1, HasSignatureTypes: Boolean, IncludeAllViews: Boolean, Views: IReadOnlyCollection`1, HasViews: Boolean
**Методы:**
- `Boolean ContainsView(Guid viewGuid)`
- `Boolean RemoveView(Guid viewGuid)`
- `Boolean AddAccess(Guid accessGuid)`
- `Void AddAccesses(Guid[] accessGuids) (+1)`
- `Boolean ContainsAccess(Guid accessGuid)`
- `Boolean RemoveAccess(Guid accessGuid)`
- `ImportCatalogSettings AddCatalog(Guid guid)`
- `Boolean AddFolders(Guid catalogGuid, Guid[] folderGuids)`
- `Boolean ContainsCatalog(Guid catalogGuid)`
- `Boolean RemoveCatalog(Guid catalogGuid)`
- `Boolean ContainsFolder(Guid folderGuid)`
- `Boolean RemoveFolder(Guid folderGuid)`
- `ImportClassSettings AddClass(Guid guid)`
- `Void AddClasses(Guid[] guids) (+1)`
- `Boolean TryGetClass(Guid guid, ImportClassSettings& settings)`
- `Boolean ContainsClass(Guid guid)`
- `Boolean RemoveClass(Guid guid)`
- `ImportReferenceSettings Create(DataExchangeParameterGroup referenceInfo) (+1)`
- `ImportDialogGroupSettings AddDialogGroup(Guid guid)`
- `Void AddDialogGroups(Guid[] guids) (+1)`
- `Boolean TryGetDialogGroup(Guid guid, ImportDialogGroupSettings& settings)`
- `Boolean ContainsDialogGroup(Guid guid)`
- `Boolean RemoveDialogGroup(Guid guid)`
- `Boolean AddEventHandler(Guid guid)`
- `Void AddEventHandlers(Guid[] guids) (+1)`
- `Boolean ContainsEventHandler(Guid guid)`
- `Boolean RemoveEventHandler(Guid guid)`
- `Boolean AddEvent(Guid guid)`
- `Void AddEvents(Guid[] guids) (+1)`
- `Boolean ContainsEvent(Guid guid)`
- `Boolean RemoveEvent(Guid guid)`
- `ImportLinkSettings AddLink(Guid guid)`
- `Void AddLinks(Guid[] guids) (+1)`
- `Boolean TryGetLink(Guid guid, ImportLinkSettings& settings)`
- `Boolean ContainsLink(Guid guid)`
- `Boolean RemoveLink(Guid guid)`
- `ImportReferenceSettings AddObjectList(Guid guid)`
- `Boolean ContainsObjectList(Guid guid)`
- `Boolean RemoveObjectList(Guid guid)`
- `ImportParameterGroupSettings AddParameterGroup(Guid guid)`
- `Void AddParameterGroups(Guid[] guids) (+1)`
- `Boolean TryGetParameterGroup(Guid guid, ImportParameterGroupSettings& settings)`
- `Boolean ContainsParameterGroup(Guid guid)`
- `Boolean RemoveParameterGroup(Guid guid)`
- `ImportParameterSettings AddParameter(Guid guid)`
- `Void AddParameters(Guid[] guids) (+1)`
- `Boolean TryGetParameter(Guid guid, ImportParameterSettings& settings)`
- `Boolean ContainsParameter(Guid guid)`
- `Boolean RemoveParameter(Guid guid)`
- `ImportSchemeSettings AddScheme(Guid guid)`
- `Boolean AddStage(Int32 stageId)`
- `Void AddStages(IEnumerable`1 stageIds)`
- `Boolean AddTransition(Int32 fromStageId, Int32 toStageId)`
- `Void AddTransitions(IEnumerable`1 transitions)`
- `Boolean ContainsStage(Int32 stageId)`
- `Boolean RemoveStage(Int32 stageId)`
- `Boolean ContainsTransition(Int32 fromStageId, Int32 toStageId)`
- `Boolean RemoveTransition(Int32 fromStageId, Int32 toStageId)`
- `Boolean AddSignatureType(Guid signatureTypeGuid)`
- `Void AddSignatureTypes(Guid[] signatureTypeGuids) (+1)`
- `Boolean ContainsSignatureType(Guid signatureTypeGuid)`
- `Boolean RemoveSignatureType(Guid signatureTypeGuid)`
- `Boolean AddView(Guid viewGuid)`
- `Void AddViews(Guid[] viewGuids) (+1)`

### `ImportSchemeSettings`
**Свойства:** Guid: Guid, Stages: HashSet`1, Transitions: HashSet`1

### `IncompleteConfigurationReference`
**Свойства:** Classes: IncompleteConfigurationTypes

### `IncompleteConfigurationReferenceObject`
**Свойства:** Class: IncompleteConfigurationType, Type: IncompleteConfigurationKind, OptionValues: IList`1, Relations: IList`1, Table: OptionsTableReferenceObject
**Методы:**
- `ReferenceObject AddOptionValue(ReferenceObject optionValue)`
- `ReferenceObject AddRelation(IncompleteConfigurationsRelationReferenceObject relation)`
- `Boolean RemoveOptionValue(ReferenceObject optionValue)`
- `Boolean RemoveRelation(IncompleteConfigurationsRelationReferenceObject relation)`

### `IncompleteConfigurationsRelationReference`
**Свойства:** Classes: IncompleteConfigurationsRelationTypes

### `IncompleteConfigurationsRelationReferenceObject`
**Свойства:** Class: IncompleteConfigurationsRelationType, Type: RelationType, Column: IncompleteConfigurationReferenceObject, Row: IncompleteConfigurationReferenceObject

### `IncompleteConfigurationsRelationType`
**Свойства:** Classes: IncompleteConfigurationsRelationTypes, IsIncompleteConfigurationsRelation: Boolean

### `IncompleteConfigurationsRelationTypes`
**Свойства:** IncompleteConfigurationsRelation: IncompleteConfigurationsRelationType

### `IncompleteConfigurationType`
**Свойства:** Classes: IncompleteConfigurationTypes, IsIncompleteConfiguration: Boolean

### `IncompleteConfigurationTypes`
**Свойства:** IncompleteConfiguration: IncompleteConfigurationType

### `IndirectLinkPath`
**Свойства:** Connection: ServerConnection, CurrentItem: IndirectLinkPathItem
**Методы:**
- `Void AddItem(IndirectLinkPathItem item)`
- `Void RemoveItem(IndirectLinkPathItem item)`
- `String Serialize(ObjectSerializationMode mode, Boolean includeRootItem) (+1)`
- `Boolean SetNextItemAsSelectFromChilden(IndirectLinkPathItem item)`
- `Boolean RemoveItemAsSelectFromChilden(IndirectLinkPathItem item)`
- `IndirectLinkPath Deserialize(String xml, ServerConnection connection)`

### `IndirectLinkPathItem`
**Свойства:** IsReadOnly: Boolean, IsSelectFromChilden: Boolean, Name: String, Type: PathItemType, Path: IndirectLinkPath
**Методы:**
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `String GetFromLinkText()`
- `String GetToLinkText()`
- `ParameterGroup GetFromGroup()`
- `ParameterGroup GetToGroup()`
- `Boolean GetCanSetNextItemAsSelectFromChilden()`

### `IndirectLinkPathItemXML`
**Свойства:** IsReadOnly: Boolean, IsSelectFromChilden: Boolean, Filter: String, ReferenceGuid: Guid, GroupGuid: Guid

### `InfoAttribute`
**Свойства:** Language: Language, Name: String, Key: String, Code: String, EndsWithSemicolon: Boolean, AdditionalName: String
**Методы:**
- `String GetKey(MemberInfo member)`

### `InfoAttributeExtensions`
**Методы:**
- `T GetCurrentLanguageAttribute(MemberInfo member, Language language) (+1)`
- `Boolean HasObsoleteAttribute(MemberInfo member)`

### `InputDialog`
**Свойства:** Caption: String, Height: Double, Width: Double, Item: Object
**Методы:**
- `Void AddInteger(String name, Int32 value, Boolean required)`
- `Void AddDouble(String name, Double value, Int32 decimalPlaces, Boolean required)`
- `Void AddString(String name, String value, Boolean multiline, Boolean required, Boolean useAllWidth, Int32 lineCount)`
- `Void AddMask(String name, String mask, TypeOfMask maskType, String value, Boolean required, Boolean useAllWidth, Int32 lineCount) (+1)`
- `Void AddDate(String name, DateTime value, Boolean required)`
- `Void AddTime(String name, DateTime value, Boolean required)`
- `Void AddPanel(String name, String header, Double height, Boolean verticalScrollBar, Boolean autoVerticalScrollBar)`
- `Void AddFieldsToPanel(String panelName, String[] fieldNames)`
- `Void AddDateTime(String name, DateTime value, Boolean required, String mask)`
- `Void AddFlag(String name, Boolean value, Boolean required, Boolean useAllWidth)`
- `Void AddSelectFromList(String name, Object value, Boolean required, Object[] values) (+1)`
- `Void AddMultiselectFromList(String name, Object[] values, Boolean required) (+1)`
- `Void AddSelectReference(String name, Object value, Boolean required)`
- `Void AddSelectFromReference(String name, String reference, String parameter, Object value, Boolean required, String filter, Guid rootObjectGuid) (+2)`
- `Void AddMatchReferenceObject(String name, String reference, String parameter, String relevanceContext, Object value, Boolean required, String filter, String viewName, Boolean useContainsFilter) (+2)`
- `Void AddButton(String name, Action`1 handler, Nullable`1 width) (+1)`
- `Boolean Show()`
- `Object GetValue(String name)`
- `Void SetValue(String name, Object value)`
- `Void AddComment(String name, String comment)`
- `Void AddGroup(String text)`
- `Void AddText(String text, Int32 lineCount) (+1)`
- `Int32 AddPicture(ObjectAccessor refObj, String imagePath, Int32 lineCount) (+2)`
- `Void ChangePicture(Int32 position, ObjectAccessor refObj, String imagePath)`
- `Int32 AddIcon(ObjectAccessor refObj, String iconPath, Int32 lineCount) (+1)`
- `Void ChangeIcon(Int32 position, ObjectAccessor refObj, String iconPath)`
- `Void SetIcon(Guid guid) (+1)`
- `Void SetSize(Int32 width, Int32 height)`
- `Void SetScrollBarsVisibility(Boolean verticalScrollBar, Boolean autoVerticalScrollBar)`
- `Void SetElementVisibility(String elementName, Boolean visible) (+1)`
- `Void SetElementEnabled(String elementName, Boolean enabled) (+1)`
- `Void SetElementRequired(String elementName, Boolean required) (+1)`
- `Void SetElementFilter(String elementName, String filter)`

### `InstallKitReference`
**Свойства:** Classes: InstallKitTypes

### `InstallKitReferenceObject`
**Свойства:** Class: InstallKitType, Name: StringParameter, Description: StringParameter, Comment: StringParameter, Folder: StringParameter, UsePackage: BooleanParameter, InstallPacketReference: InstallPacketReference, InstallPackets: ReferenceObjectCollection`1
**Методы:**
- `InstallPacketReferenceObject CreateInstallPacket(Guid listObjectClass) (+1)`

### `InstallKitType`
**Свойства:** Classes: InstallKitTypes, IsInstallKit: Boolean

### `InstallKitTypes`
**Свойства:** InstallKit: InstallKitType

### `InstallPacketActionReference`
**Свойства:** Classes: InstallPacketActionTypes

### `InstallPacketActionReferenceObject`
**Свойства:** InstallAction: InstallActions, InstallObjectType: InstallObjectTypes, Class: InstallPacketActionType, Denotation: StringParameter, Action: Int32Parameter, Version: StringParameter, ObjectType: Int32Parameter, ObjectGuid: GuidParameter, Value: StringParameter, GroupGuid: GuidParameter, EventGuid: GuidParameter, Property: StringParameter

### `InstallPacketActionType`
**Свойства:** Classes: InstallPacketActionTypes, IsInstallPacketAction: Boolean

### `InstallPacketActionTypes`
**Свойства:** InstallPacketAction: InstallPacketActionType

### `InstallPacketReference`
**Свойства:** Classes: InstallPacketTypes

### `InstallPacketReferenceObject`
**Свойства:** Class: InstallPacketType, Name: StringParameter, ReferenceGuid: GuidParameter, Settings: StringParameter, InstallFile: FileObject, Objects: AnyReferenceLink, InstallPacketActionReference: InstallPacketActionReference, InstallPacketActions: ReferenceObjectCollection`1
**Методы:**
- `InstallPacketActionReferenceObject CreateInstallPacketAction(Guid listObjectClass) (+1)`

### `InstallPacketType`
**Свойства:** Classes: InstallPacketTypes, IsInstallPacket: Boolean

### `InstallPacketTypes`
**Свойства:** InstallPacket: InstallPacketType

### `InstanceConversionServiceReferenceObject`
**Свойства:** Class: InstanceConversionServicesType, Name: StringParameter, ClientTFlexDOCs: StringParameter, CreateFileVersion: BooleanParameter, StopService: BooleanParameter, Comment: StringParameter

### `InstanceConversionServicesReference`
**Свойства:** Classes: InstanceConversionServicesTypes

### `InstanceConversionServicesType`
**Свойства:** Classes: InstanceConversionServicesTypes
**Методы:**
- `Boolean GetIsInstanceConversionServiceReferenceObject()`

### `InstanceConversionServicesTypes`
**Свойства:** InstanceConversionServiceReferenceObject: InstanceConversionServicesType

### `InstancesGroupInfo`
**Свойства:** MasterReferenceId: Int32, InstancesReferenceId: Int32, LinkToObjectId: Int32, LinkToHierarchyId: Int32, LinkToAltRepId: Int32, InstanceMainClassId: Int32, MasterReference: ReferenceInfo, InstancesReference: ReferenceInfo, LinkToObject: ParameterGroup, LinkToHierarchy: ParameterGroup, InstanceMainClass: ClassObject, LinkToSourceStructureInstances: ParameterGroup, LinkToAltRep: ParameterGroup
**Методы:**
- `Boolean IsInstanceSystemLink(ParameterGroup link)`

### `InstancesMappingTypeHelper`
**Методы:**
- `String GetInstanceMappingTypeStringValue(InstancesMappingType mappingType)`

### `Int16Parameter`
**Методы:**
- `Int16 GetInt16()`
- `TypeCode GetTypeCode()`

### `Int32Parameter`
**Методы:**
- `Int32 GetInt32()`
- `TypeCode GetTypeCode()`

### `Int64Parameter`
**Методы:**
- `Int64 GetInt64()`
- `TypeCode GetTypeCode()`

### `IntDefaultRepositoryItemXMLData`
**Свойства:** MaxValue: Nullable`1, MinValue: Nullable`1, UseMinValue: Boolean, UseMaxValue: Boolean

### `IntegerFieldInputDialog`
**Свойства:** TypeName: String, DefaultValue: InArgument`1

### `InteractiveCADVersionChecker`
**Методы:**
- `Boolean Check(InteractiveCADVersionInfo versionInfo)`
- `Boolean SupportStructureElements(InteractiveCADVersionInfo versionInfo)`

### `InteractiveCADVersionInfo`
**Свойства:** Product: InteractiveCADs, Version: Version

### `IntervalReferenceObject`
**Свойства:** ProductsClassifierObject: ProductsClassifierReferenceObject, ApplicabilitySetMethod: ApplicabilitySetMethod, MilestoneRanges: List`1, DesignNumberRanges: List`1, StructureVariantObject: StructureVariantsReferenceObject, ApplicabilityAction: ApplicabilityActionType, OptionsDescription: String, UseNumberRanges: Boolean, Class: ProductsApplicabilityType, Name: StringParameter, ObjectGuid: GuidParameter, ReferenceGuid: GuidParameter, LinkedObjectID: Int32Parameter, ReferenceID: Int32Parameter, Description: StringParameter, ApplicabilityGroup: ApplicabilityGroupType, Conditions: StringParameter, OptionRecords: List`1, ApplicabilityRecords: List`1
**Методы:**
- `Void SetApplicabilityRecords(List`1 records)`
- `Void SetOptionRecords(List`1 records)`
- `Void CopyRecordsFrom(IntervalReferenceObject other)`

### `IntPropertyData`
**Свойства:** Value: Int32

### `IObjectNode`
**Свойства:** DesktopObject: DesktopObject, Version: Int32
**Методы:**
- `Void AddParameterGroup(IParameterGroupNode node)`
- `ObjectValue GetParameterValue(String parameterPath)`
- `IEnumerable`1 GetRelationObjects(Guid ruleRelationGuid) (+1)`
- `IEnumerable`1 GetParameterGroups()`
- `IEnumerable`1 GetRelations()`
- `Void AddRelation(IRelationNode relation)`
- `Void AddRelationObject(IRelationNode relationNode, IObjectNode node)`
- `Boolean HasParameterGroup(String parameterGroupUniqueId)`
- `Boolean HasRelation(String relationUniqueId)`

### `IObjectsComparisonNode`
**Свойства:** UniqueId: String, Name: String, State: State

### `IOpenFileDialog`
**Свойства:** MultipleSelect: Boolean, SupportMultiDottedExtensions: Boolean

### `IOpenFolderDialog`
**Свойства:** DirectoryName: String

### `IPacketSetReferenceObject`
**Свойства:** PacketSet: DesktopObjectPacketSet`1

### `IParameterGroupNode`
**Методы:**
- `Void AddParameter(IParameterNode parameterNode)`
- `IEnumerable`1 GetParameters()`

### `IParameterNode`
**Свойства:** ParameterGroup: IParameterGroupNode, Value: Object, Diff: String

### `IPhysicalProperties`
**Свойства:** Density: Double, Stress: Double, CompressionLimit: Double, YieldStrength: Double, SpecificHeat: Double, Elasticity: Double, Puasson: Double, Expansion: Double, ThermalConductivity: Double

### `IPluginLibrary`
**Методы:**
- `Void RegisterPlugin()`
- `Void OnCreatingVisualRepresentation(IModelVisualRepresentation VisualRepresentation)`
- `Void OnCreatingReferenceVisualRepresentation(Reference reference, IModelVisualRepresentation VisualRepresentation)`

### `IProgress`
**Методы:**
- `Void Report(String description)`

### `IProgressIndicator`
**Свойства:** Text: String
**Методы:**
- `Void Hide()`
- `Void Show()`

### `IProgressive`
**Свойства:** Percent: Double, AutoCalculation: Boolean
**Методы:**
- `Boolean CanChangePercent()`
- `Boolean CanChangeAutoCalculation()`
- `Void ChangePercent(Double percent)`
- `Void ChangeAutoCalculation(Boolean autoCalculation)`
- `Void RecalculateProgress()`

### `IProjectsHelper`
**Методы:**
- `Void OpenWorkWindow(ReferenceObject work, IntPtr handle)`

### `IProxyValue`
**Методы:**
- `Object GetRealValue()`

### `IQueryFilePreviewControl`
**Методы:**
- `Boolean ExecuteDocumentRequest(FilePreviewRequest request, String& requestId)`

### `IReferenceObjectMatcher`
**Методы:**
- `Boolean Match(ReferenceObjectTerm term, Object obj, MacroContext formulaContext)`

### `IReferenceVariable`
**Свойства:** ReferenceGuid: Guid

### `IRelationNode`
**Методы:**
- `IEnumerable`1 GetObjects()`
- `Void AddRelationObject(IObjectNode node)`

### `IReportGenerationContextWithConfigurationSettings`
**Свойства:** ConfigurationSettingsInfo: String

### `ISaveFileDialog`
**Свойства:** ValidateNames: Boolean, CreatePrompt: Boolean, OverwritePrompt: Boolean

### `ISelectClassObjectsDialog`
**Свойства:** SelectedClassObjects: ClassObject[], AllowedClassObjects: ClassObject[], Caption: String, SelectAbstractClasses: Boolean, CheckboxSelection: Boolean, CheckboxesAutoSelection: Boolean
**Методы:**
- `Boolean Show()`

### `ISelectListObjectsDialog`
**Свойства:** AllowOrderResult: Boolean, ShowSearchPanel: Boolean, HideDefaultColumns: Boolean, MirrorDialog: Boolean, ListObjects: List`1
**Методы:**
- `Void AddColumn(String name, Func`2 calculateValue)`

### `ISelectObjectDialog`
**Свойства:** ReferenceInfo: ReferenceInfo, Reference: Reference, MultipleSelect: Boolean, ShowToolbar: Boolean, Filter: Filter, FocusedObject: ReferenceObject, CheckboxSelection: Boolean, CheckboxesAutoSelection: Boolean, RootObject: ReferenceObject, View: String, Catalog: String, CatalogFolder: String, PrototypeMode: Boolean, IsReadOnly: Boolean

### `ISelectObjectsFromReferencesDialog`
**Свойства:** SelectedObjects: ReferenceObject[], SelectedHierarchyLinks: ComplexHierarchyLink[], Caption: String
**Методы:**
- `Boolean Show()`

### `IServerEventHandlerProvider`
**Свойства:** ServerEventHandler: ServerEventHandler

### `ISettingsContainer`
**Свойства:** Application: String, Context: String, Exists: Boolean, Interface: String, IsNew: Boolean, IsCommon: Boolean, IsLoaded: Boolean, ObjectId: Int32, ParameterGroupId: Int32, FolderGuid: Guid, SharingType: SettingsSharingType, SupportsViews: Boolean, Data: Object, IsLocked: Boolean, CurrentView: ISettingsView, DefaultView: ISettingsView, Views: ReadOnlyCollection`1
**Методы:**
- `Void Lock()`
- `Void Unlock()`
- `Void Clear()`
- `Void Reset()`
- `Void Save()` [has Async]
- `Boolean Load()` [has Async]
- `Boolean Remove()`
- `Boolean Reload(Boolean reloadViews)` [has Async]
- `Void ReloadViews()`
- `Void ApplyViewOnLoading(ISettingsView view)`
- `Void ApplyView(ISettingsView view)`
- `ISettingsView CreateView(String name, SettingsViewType type, Boolean inSettingsContext, Boolean copySettings, ConfigurationUseType configurationUseType, List`1 configurations, SettingsViewAccessType accessType, List`1 users, Boolean showOpenAsCommand, String comment) (+1)`
- `Boolean DeleteView(ISettingsView view)`
- `Void UpdateView(ISettingsView view, String name, SettingsViewType type, Boolean inSettingsContext, Boolean copySettings, ConfigurationUseType configurationUseType, List`1 configurations, SettingsViewAccessType accessType, List`1 users, Boolean showOpenAsCommand, String comment) (+1)`

### `ISettingsView`
**Свойства:** Id: Guid, IsDefault: Boolean, IsInSettingsContext: Boolean, IsShared: Boolean, IsDefaultForAllConfigurations: Boolean, ConfigurationUseType: ConfigurationUseType, Configurations: ReadOnlyCollection`1, AccessType: SettingsViewAccessType, Users: ReadOnlyCollection`1, Name: String, Comment: String, Type: SettingsViewType, ShowOpenAsCommand: Boolean, Owner: ISettingsContainer
**Методы:**
- `Boolean CanUseInCurrentConfiguration()`
- `String GetData()`

### `ISignatureType`
**Свойства:** SignatureType: InArgument`1

### `IsNotOneOfMailCategoryOperator`
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `IsOneOfMailCategoryOperator`
**Свойства:** RequireValueList: Boolean
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `IsOwnerOperator`
**Свойства:** SupportsSecondOperand: Boolean
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `ISupportDynamicPreviewContext`
**Свойства:** LoadByDataModel: Guid, UseDynamicPreview: Boolean

### `ISupportPreviewParameters`
**Методы:**
- `IEnumerable`1 GetPreviewParameters()`

### `ISupportPrint`
**Свойства:** CanPrint: Boolean
**Методы:**
- `Void Print()`

### `ISupportSecondOperatorCustomValue`
**Методы:**
- `String SerializeTermValue(Object value, Nullable`1 mode)`
- `Object ParseTermValue(String value)`
- `Boolean IsValidTermValue(Object value, Term term, Boolean throwOnError)`

### `ISupportServerConnection`
**Методы:**
- `Void SetServerConnection(ServerConnection serverConnection, Boolean isAnnotationEnabled)`

### `ISystemEventHandlerProvider`
**Свойства:** Guid: Guid, HandlerName: String
**Методы:**
- `Object Run(MacroContext context, String entryPoint, Object[] args)`
- `Boolean SupportsParameterGroup(Guid parameterGroupGuid)`

### `ISystemTaskActionExecuter`
**Методы:**
- `String Execute(MacroContext context)`

### `ItemListUseTypeExtensions`
**Методы:**
- `String GetName(ItemListUseType type)`

### `ITextCodeEditExtension`
**Методы:**
- `List`1 GetToolGroups(Language language)`

### `ITFlexCadFilePreview`
**Методы:**
- `Void ShowFile(String fileName, Object context, TFlexCadWindowType windowType, Boolean readOnly, Nullable`1 viewAreaSize)`

### `IToolboxActivityInfo`
**Свойства:** Name: String, ToolboxInterfaceName: String, IsSystem: Boolean, Categories: List`1, Item: IToolboxCategoryActivityInfo
**Методы:**
- `List`1 GetItems()`

### `IToolboxCategoryActivityInfo`
**Свойства:** Name: String, Items: List`1, IsExpandedByDefault: Boolean, AllowSort: Boolean
**Методы:**
- `IToolboxCategoryActivityInfo Copy()`

### `IToolboxController`
**Свойства:** Toolboxes: List`1, ActivityTypes: List`1, BaseActivityTypes: List`1, ActivityItems: List`1, Item: IToolboxActivityInfo, IsRegisterIcons: Boolean
**Методы:**
- `Void RegisterMetadata(Object builder)`
- `Void RegisterIcons()`

### `IToolboxItemActivityInfo`
**Свойства:** Name: String, Category: String, BitmapName: String, IsStandardIcon: Boolean, Description: String, TypeDescription: String, ActivityType: Type, RecalcPropertyNames: String[], ReturnType: Type

### `IToolGroup`
**Свойства:** Name: String, Icon: IconImage

### `IVariable`
**Свойства:** Name: String, TextValue: String, RealValue: Double, IsText: Boolean, Comment: String

### `IViewerServiceOwner`
**Свойства:** AsyncModeSupported: Boolean, Control: Object
**Методы:**
- `Void DoShowPreview(Boolean executeAsynchronously)`

### `IVisualProperties`
**Свойства:** Name: String, AmbientColor: Int32, DiffuseColor: Int32, SpecularColor: Int32, EmissiveColor: Int32, Shininess: Double, Reflection: Double, Transparency: Double

### `IWaitingDialog`
**Методы:**
- `Void Show(String caption, Boolean canCancel)`
- `Void Hide()`
- `Boolean NextStep(String description, Nullable`1 progress) (+1)`

### `IWindow`
**Свойства:** Name: String
**Методы:**
- `Void ReloadItem(String name)`
- `ILayoutItem FindItem(String name)`
- `Void Reload()` [has Async]
- `Void ReloadItems(Predicate`1 layoutItemPredicate)` [has Async]

### `IWorkingInterval`
**Свойства:** Duration: TimeSpan, StartTime: DateTime, EndTime: DateTime, StartSpan: TimeSpan, EndSpan: TimeSpan

### `IWorkTimeChange`
**Свойства:** IsWorkDay: Boolean, Date: DateTime, WorkTimeIntervals: IEnumerable`1

### `IWorkTimeObject`
**Свойства:** StartDate: DateTime, WorkTimeIntervals: IEnumerable`1, PriorityValue: Int32
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `LabelReferenceObject`
**Свойства:** Time: DateTime, Name: String, Comment: String, ImageObject: ImageReferenceObject

### `LabelSetting`
**Свойства:** Figure: Int32

### `LabelsReference`
**Свойства:** Classes: ResourceLinkTypes

### `LabelType`
**Свойства:** Classes: LabelTypes, IsLabel: Boolean

### `LabourResourceLinkObject`
**Свойства:** Employment: Double, BasicRate: Double
**Методы:**
- `Void SetDuration(Int32 duration)`
- `Void UpdateValue()`

### `LastChangeDateParameter`
**Свойства:** IsNull: Boolean, IsReadOnly: Boolean
**Методы:**
- `DateTime GetDateTime()`
- `TypeCode GetTypeCode()`

### `LayoutDescriptionParser`
**Методы:**
- `PageDescription GetDescription(String xml, Func`2 itemDescriptionCreator) (+1)`

### `LayoutItemAccessor`
**Свойства:** Name: String [RU: Наименование], SelectedObjects: RefObjList, SelectedHierarchyLinks: HierarchyLinkList, IsSupportFilter: Boolean [RU: ПоддерживаетФильтрацию], IsSupportView: Boolean [RU: ПоддерживаетФильтрацию], ВыбранныеОбъекты: Объекты [RU only], ВыбранныеПодключения: Подключения [RU only]
**Методы:**
- `Void ApplyFilter(String parameter, Object value) (+5)` [RU: УстановитьТекущийФильтр]
- `Void EnableFilter()` [RU: ВключитьФильтр]
- `Void DisableFilter()` [RU: ВключитьФильтр]
- `Void ApplyView(ValueTuple`2 view) (+2)` [RU: УстановитьТекущийФильтр]
- `ValueTuple`2[] GetViews()` [RU: ВключитьФильтр]
- `Nullable`1 GetCurrentView()` [RU: ВключитьФильтр]
- `Void Reload()` [RU: ВключитьФильтр]
- `Void ОтключитьФильтр()` [RU alternative]
- `Void ПрименитьВид(ValueTuple`2 вид)` [RU alternative]
- `ValueTuple`2[] ПолучитьВиды()` [RU alternative]
- `Nullable`1 ПолучитьТекущийВид()` [RU alternative]
- `Void Обновить()` [RU alternative]

### `LayoutItemObj`
**Методы:**
- `LayoutItemObj CreateInstance(ILayoutItem item, MacroContext context)`

### `LCS`
**Свойства:** Origin: Point3D, PointX: Point3D, PointY: Point3D, PointZ: Point3D
**Методы:**
- `Void Initialize(Point3D origin, Point3D pointX, Point3D pointY, Point3D pointZ)`

### `LcsData`
**Свойства:** Origin: Point3DData, PointX: Point3DData, PointY: Point3DData, PointZ: Point3DData

### `LegacySlaveFileInfo`
**Свойства:** Guid: Guid, Path: String, Id1: Int32, Id2: Int32, Id3: Int32, Id4: Int32
**Методы:**
- `List`1 GetSlaveFiles(ServerConnection connection, Guid masterFileGuid) (+1)`

### `LegendSettings`
**Свойства:** IsLegendVisible: Boolean, Name: String, HorizontalPosition: HorizontalPositionType, VerticalPosition: VerticalPositionType, Orientation: LegendOrientation, LegendMarkerMode: LegendMarkerMode

### `LicenseKeyInfo`
**Свойства:** HaspID: UInt64, ServerAddress: String, SupportEndDate: DateTime, OperationTestingEndDate: DateTime

### `LicenseManager`
**Методы:**
- `LicenseQuota CreateQuota(ModuleLicense license)`

### `LicenseQuota`
**Свойства:** IsAdded: Boolean, IsModified: Boolean, IsDeleted: Boolean, License: ModuleLicense, AvailableCount: Int32, User: UserReferenceObject, UserId: Int32, TotalCount: Int32
**Методы:**
- `Void BeginChanges()`
- `Void CancelChanges()`

### `LinkAccessType`
**Свойства:** AccessTypeID: AccessTypeID, Type: AccessCommandType, Name: String, IsLink: Boolean, Read: AccessCommand, Add: AccessCommand, Remove: AccessCommand

### `LinkedHiearchyLinkAccessor`1`
**Свойства:** Item: T

### `LinkedHierarchyLinksAccessor`2`
**Свойства:** Item: TList

### `LinkedObjectAccessor`1`
**Свойства:** Item: T

### `LinkedObjectPathElement`
**Свойства:** DefaultType: DefaultSupportedType
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean IsEqual(PathElement pathElement)`

### `LinkedObjectPathItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `LinkedObjectsAccessor`2`
**Свойства:** Item: TList

### `LinkExportSettings`
**Свойства:** Connection: ServerConnection, Owner: ExportSettings, LinkGroup: ParameterGroup, IncludeLinkObjectsById: Boolean

### `LinkExtensions`
**Методы:**
- `OneToManyRelation FindToManyRelation(DesktopObject desktopObject, Guid linkGuid) (+1)`
- `OneToOneLink FindToOneLink(DesktopObject desktopObject, Guid linkGuid) (+1)`
- `IconImage GetLinkTypeIcon(LinkVisibility linkVisibility, LinkType linkedType, Boolean throwOnError)`
- `IconImage GetSystemLinkTypeIcon(LinkType linkedType)`
- `IconImage GetCorruptedLinkTypeIcon(LinkType linkedType)`
- `String GetLinkTypeDescription(LinkType type)`

### `LinkFilterSettings`
**Свойства:** Filter: Filter
**Методы:**
- `String Serialize()`
- `Void Deserialize(String data)`

### `LinkGroupBuilder`
**Свойства:** MasterName: String, SlaveName: String, SlaveGroup: ParameterGroup, Swapped: Boolean, LinkType: LinkType, LinkVisibility: LinkVisibility, CheckAccess: AccessRightsMode, LinkRequired: LinkRequired, SelectionPath: String, DoubleDirection: Boolean, SupportsVersions: Boolean, IsAsymmetricLink: Boolean, SearchQueryLinkFilter: String, SearchQueryLinkPathToFilter: String
**Методы:**
- `Void Save()` [has Async]

### `LinkGroupPathElement`
**Свойства:** LinkGuid: Guid, IsToMany: Boolean, IsLink: Boolean, DefaultType: DefaultSupportedType
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean IsEqual(PathElement pathElement)`

### `LinkInfo`
**Свойства:** LinkGroup: ParameterGroup, Master: DesktopObject, MasterObject: ReferenceObject, MasterLink: ComplexHierarchyLink, RootMasterObject: ReferenceObject, RootMasterReference: Reference, Swapped: Boolean, IsOneToOne: Boolean, IsOneToMany: Boolean, IsTableOneToMany: Boolean, IsLinkOneToMany: Boolean, IsAnyReference: Boolean, IsSearchQueryLink: Boolean, IsLinkedReferenceInitialized: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, IsEmptyLinkedObjects: Boolean, IsModified: Boolean, IsChanged: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32, LinkReference: Reference
**Методы:**
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `Void Clear(Boolean full) (+1)`
- `ClassObjectCollection GetAllowedClassesToLink()`
- `List`1 GetDeletedObjects()` [has Async]

### `LinkPathItem`
**Свойства:** Type: PathItemType, UseLinkSeparator: Boolean, SupportSearchType: SupportSearchTypes, Swapped: Boolean
**Методы:**
- `Boolean IsOneToMany()`

### `LinkRequiredExtensions`
**Методы:**
- `String GetName(LinkRequired requirement)`

### `LinkTypeExtensions`
**Методы:**
- `String GetName(LinkType type)`

### `LinkVisibilityExtensions`
**Методы:**
- `String GetName(LinkVisibility visibility)`

### `ListValue`
**Свойства:** List: ParameterValueList, Key: Guid, Name: String, Value: Object, Icon: IconImage

### `LiteConfigurationExt`
**Методы:**
- `Boolean IsLite(BaseConfiguration configuration)`

### `LoadingCallback`
**Методы:**
- `Task Invoke(ServerConnection connection, IProgress waiting, CancellationToken cancellation)`
- `IAsyncResult BeginInvoke(ServerConnection connection, IProgress waiting, CancellationToken cancellation, AsyncCallback callback, Object object)`
- `Task EndInvoke(IAsyncResult result)`

### `LoadOptionsGroupPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `LoadOptionsParameterExtensions`
**Методы:**
- `String GetName(LoadOptionsParameter parameter)`

### `LoadOptionsParameterPathItem`
**Свойства:** Name: String, Type: PathItemType, Parameter: LoadOptionsParameter

### `LoadOptionsParameters`
**Свойства:** Offset: Nullable`1, Count: Nullable`1, OnlyChildrenObjects: Nullable`1, HasRootObjectFilter: Boolean, SortFields: ReadOnlyCollection`1, HasSortFields: Boolean
**Методы:**
- `ReferenceObject GetRootObject(Reference reference)` [has Async]

### `LoadOptionsRootObjectPathItem`
**Свойства:** Name: String, Type: PathItemType

### `LoadOptionsSortFieldPathItem`
**Свойства:** Name: String, Type: PathItemType

### `LoadSettings`
**Свойства:** MasterGroup: ParameterGroup, LoadDeleted: Boolean, LoadBinaryParameters: Boolean, LoadAllHierarchyParameters: Boolean, OmitHasChildrenCheck: Nullable`1, UseConfigurationSettings: Boolean, UseInstanceMode: Boolean, ParentInstance: ReferenceObjectInstance, RelationsForCheck: ReadOnlyCollection`1, RelationsForCheckCount: Int32, Parameters: ParameterInfoCollection, LoadStructureTypes: Boolean, CheckOnlyHasSubfolders: Boolean, Relations: ICollection`1, SortFields: ReadOnlyCollection`1, HasSortFields: Boolean, SelectionContext: String
**Методы:**
- `Boolean Add(ParameterGroup group) (+5)`
- `Void LoadOneToOneTables()`
- `Void AddRange(IEnumerable`1 parameters)`
- `LoadSettings GetLinkLoadSettings(ParameterGroup linkGroup)`
- `Void ClearLinkLoadSettings(ParameterGroup linkGroup)`
- `Void Clear(Boolean useMaster) (+1)`
- `Boolean AddGroup(ParameterGroup group)`
- `Void AddParameters(Guid[] guids) (+1)`
- `Void AddMasterGroupParameters()`
- `Void AddAllParameters()`
- `Boolean Contains(ParameterInfo item)`
- `Boolean Remove(ParameterInfo parameter) (+2)`
- `RelationLoadSettings AddRelation(ParameterGroup relation, Func`2 staticReferenceFunc) (+5)` [has Async]
- `RelationLoadSettings GetRelation(ParameterGroup relation) (+1)`
- `LinkedObjectLoadSettings AddLinkedObjectRelation()`
- `StructureTypeRelationLoadSettings AddStructureTypeRelation()`
- `ApplicabilityRelationLoadSettings AddApplicabilityRelation()`
- `StartProductRelationLoadSettings AddStartProductRelation()`
- `EndProductRelationLoadSettings AddEndProductRelation()`
- `ObjectRemarksRelationLoadSettings AddObjectRemarksRelation()`
- `AuthorRelationLoadSettings AddAuthorRelation()`
- `EditorRelationLoadSettings AddEditorRelation()`
- `OwnerRelationLoadSettings AddOwnerRelation()`
- `OnBehalfOfRelationLoadSettings AddOnBehalfOfRelation()`
- `CredentialRelationLoadSettings AddCredentialRelation()`
- `MasterServerRelationLoadSettings AddMasterServerRelation()`
- `BaseRepresentationLoadSettings AddBaseRepresentationRelation()`
- `Void CheckLink(Int32 relationId, Boolean swapped) (+2)`
- `Boolean ContainsRelationForCheck(Int32 id)`
- `Boolean RemoveRelation(ParameterGroup relation) (+1)`
- `Void Append(LoadSettings settings)`
- `SortField AddSortField(ParameterGroup linkGroup, ParameterInfo parameter, SortOrder order) (+1)` [has Async]
- `Boolean RemoveSortField(SortField field)`
- `Void AddSortFields(SortField[] sortFields) (+1)`
- `Void ClearSortFields()`

### `LocalApplication`
**Свойства:** ReadOnly: Boolean, Type: ApplicationType

### `LocalRepresentationGenerator`
**Методы:**
- `Void Generate(ICollection`1 masterFiles)`
- `Void RegenerateSecondaryFiles(ICollection`1 secondaryFiles)`

### `LocationReferenceEnvironmentExtensions`
**Методы:**
- `IEnumerable`1 GetAvailableLocationReferences(LocationReferenceEnvironment environment)`

### `M`
**Методы:**
- `Double Sin(Double degrees)`
- `Double Asin(Double d)`
- `Double Cos(Double degrees)`
- `Double Acos(Double d)`
- `Double Tg(Double degrees)`
- `Double Atg(Double d)`
- `Double Ctg(Double degrees)`
- `Double Actg(Double d)`

### `Macro`
**Свойства:** Class: MacroType, Name: StringParameter, Comment: StringParameter, References: StringParameter, LogRunHistory: BooleanParameter, DebugMode: BooleanParameter, Code: StringParameter, IsCompiled: Boolean, IsLimitedCountEntryPointParameters: Boolean, IsMethod: Boolean
**Методы:**
- `List`1 GetAdditionalFiles()` [has Async]
- `MacroValidationResults Validate()`
- `Object Run(MacroContext context, String entryPoint, Object[] parameters) (+1)` [has Async]
- `Type GetMacroProviderType()`
- `IEnumerable`1 GetEntryPoints()`

### `MacroColumnData`
**Свойства:** Formula: String, Type: ColumnDataType, IsEmpty: Boolean

### `MacroContext`
**Свойства:** Connection: ServerConnection, Group: ParameterGroup, Reference: Reference, ConfigurationSettings: ConfigurationSettings, ReferenceObject: ReferenceObject, ReferenceObjectInstance: ReferenceObjectInstance, CancellationToken: CancellationToken, HierarchyLink: ComplexHierarchyLink, ModelChangedArgs: ModelEventArgs, ObjectChangedArgs: ObjectChangedEventArgs, ChangedParameter: Parameter, ChangedLink: LinkInfo, ChangedParameterName: String, ChangedLinkName: String, IsAdministrator: Boolean, RefreshCollectionControls: Boolean, CancellingChanges: Boolean, Filter: Filter, Item: Object
**Методы:**
- `Void RaiseEvent(String eventName)`
- `Object RunMacro(String macroName, String entryPoint, Object[] parameters)`
- `Void GenerateError(String text, Object[] args)`
- `Void WriteTextToLogFile(String text)`
- `Void WriteMessageToLogFile(String message, TypeLogMessageAccessor typeLogMessage)`
- `ReportGenerationContext GenerateReport(Report report, ReportGenerationContext reportContext, OpenReportType openReportType)`
- `Void ShowMessage(String caption, String text, Object[] args)`
- `Boolean ShowQuestion(String text)`
- `Nullable`1 ShowQuestionWithCancel(String text)`
- `IInputDialog CreateInputDialog()`
- `ISelectObjectDialog CreateSelectObjectDialog(String referenceName) (+2)`
- `ISelectObjectsFromReferencesDialog CreateSelectObjectsDialogFromReferences()`
- `ISelectListObjectsDialog CreateSelectListObjectsDialog(List`1 listObjects)`
- `ISelectClassObjectsDialog CreateSelectClassObjectsDialog(String referenceName) (+1)`
- `IWaitingDialog GetWaitingDialog()`
- `IWaitingDialog CreateWaitingDialog()`
- `IOpenFileDialog CreateOpenFileDialog()`
- `IOpenFolderDialog CreateOpenFolderDialog()`
- `ISaveFileDialog CreateSaveFileDialog()`
- `T GetUserDialog(String userDialogTypeName, CreateDialogObjectInstanceDelegate`1 dialogObjectCreator, Boolean emptyDialog) (+1)`
- `Boolean ShowObjectPropertyDialog(ObjectAccessor refObj, String caption, Boolean inNewWindow, Boolean showConfirmationOnCancel) (+3)`
- `ClassObject ShowClassObjectSelectionDialog(String referenceName, String caption)`
- `Void OpenProjectEditor(IEnumerable`1 projects, String view, String style)`
- `Void OpenWorksUsage(ReferenceObject project, String view, String style)`
- `Void OpenResourcesUsage(ReferenceObject projectElement, ReferenceObject resource, String view, String style)`
- `Void OpenReferenceWindow(String referenceName, String filterString, ObjectAccessor rootObject, String viewName, String catalogFolder) (+1)`
- `Void RunOnUIThread(Action action)`
- `T CreateInstance()`
- `ReferenceObject[] GetSelectedObjects(ILayoutItem layoutItem) (+1)`
- `ComplexHierarchyLink[] GetSelectedHierarchyLinks(ILayoutItem layoutItem) (+1)`
- `Void RefreshReferenceWindow()`
- `Void RefreshWorkingPageControl(String[] controlNames)`
- `Void RefreshPropertiesDialogContent()`
- `Void RefreshControls(String[] controlNames) (+1)`
- `Void RefreshReferenceObjects(ICollection`1 referenceObjects)`
- `IWindow GetCurrentWindow()`
- `IProgressIndicator GetProgressIndicator()`
- `Void OpenFilePreview(TList objects)`
- `Void OpenWorkingPage(String workingPage)`
- `T GetObjectFromContext(ReferenceObject referenceObject, ComplexHierarchyLink hierarchyLink) (+1)`
- `ClassObject[] GetClassObjects(String referenceName, String[] classObjects)`
- `Void Register(MarshalByRefObject obj)`
- `Void CloseDialog(Boolean saveChanges, Boolean showConfirmationOnCancel)`

### `MacroContextExtensions`
**Методы:**
- `ObjectAccessor CreateObject(MacroContext context, ReferenceObject referenceObject, Language language) (+1)`
- `IEnumerable`1 CreateObjects(MacroContext context, IEnumerable`1 referenceObjects, Language language) (+1)`
- `HierarchyLinkAccessor CreateHierarchyLink(MacroContext context, ComplexHierarchyLink hierarchyLink, Language language) (+1)`
- `IEnumerable`1 CreateHierarchyLinks(MacroContext context, IEnumerable`1 hierarchyLinks, Language language) (+1)`
- `SignatureAccessor CreateSignature(MacroContext context, Signature signature)`
- `InputDialog CreateInputDialog(MacroContext context, String caption)`
- `IEnumerable`1 CreateParameterValueList(MacroContext context, IEnumerable`1 values)`
- `Object GetAccessorValue(MacroContext context, Object obj)`

### `MacroDependencyFinder`
**Методы:**
- `String ReplaceDevExpressVersion(String reference)`

### `MacroEntryPointSelectorData`
**Свойства:** LinkGuid: Guid

### `MacroObjectSavedArgs`
**Свойства:** Type: ObjectChangeType, Sender: Object

### `MacroProvider`
**Свойства:** Context: MacroContext, CurrentConfiguration: ConfSettings, CurrentObject: RefObj, CurrentObjectInstance: RefObjInstance, SelectedObjects: RefObjList, CurrentHierarchyLink: HierarchyLink, SelectedHierarchyLinks: HierarchyLinkList, Parameter: ParameterAccessor [RU: Параметр], Class: ClassObjectAccessor [RU: Тип], Global: GlobalParameterAccessor [RU: ГлобальныйПараметр], Nomenclature: NomenclatureReferenceAccessor [RU: Номенклатура], ProgressIndicator: ProgressIndicatorAccessor [RU: ИндикаторВыполнения], BusinessProcesses: BusinessProcessesReferenceAccessor [RU: БизнесПроцессы], DataExchange: DataExchangeAccessor [RU: ОбменДанными], ProjectManagement: ProjectManagementReferenceAccessor [RU: УправлениеПроектами], Chancellery: ChancelleryReferenceAccessor [RU: Канцелярия], Reports: ReportReferenceAccessor [RU: Отчёты], WaitingDialog: WaitingDialogAccessor [RU: ДиалогОжидания], ChangedParameter: String [RU: ИзмененныйПараметр], ChangedLink: String [RU: ИзмененныйПараметр], CurrentUser: UserRefObj, FilterVariable: VariableAccessor [RU: ПеременнаяФильтра], CancelWhenObjectEndEditProperties: Boolean [RU: ОтменаПриЗавершенииРедактированияСвойств], CurrentWindow: WindowObj, ТекущаяКонфигурация: Конфигурация [RU only], ТекущийОбъект: Объект [RU only], ТекущийЭкземплярОбъекта: ЭкземплярОбъекта [RU only], ВыбранныеОбъекты: Объекты [RU only], ТекущееПодключение: Подключение [RU only], ВыбранныеПодключения: Подключения [RU only], ТекущийПользователь: Пользователь [RU only], ТекущееОкно: Окно [RU only]
**Методы:**
- `Void Run()` [RU: Прервать]
- `RefObj FindObject(String referenceName, String parameter, Object value) (+3)` [RU: НайтиОбъекты]
- `Void ChangeStageObjects(RefObjList objects, String stageName, String comment, Boolean ignoreSchemeStage) (+1)` [RU: НайтиОбъекты]
- `RefObj FindLoadedObject(String referenceName, String parameter, Object value) (+3)` [RU: НайтиОбъекты]
- `RefObjList FindObjects(String referenceName, String parameter, Object value) (+3)` [RU: НайтиОбъекты]
- `RefObj FindPrototype(String referenceName, String filter)` [RU: НайтиЗагруженныйОбъект]
- `RefObj CreateObject(String referenceName, String className, ObjectAccessor parentObject) (+4)` [RU: СоздатьОбъект]
- `CopiedObjects CopyObject(ObjectAccessor prototype, ObjectAccessor parentObject, Boolean copyChildren, Boolean copyLinkedPrototypes)` [RU: ИзменитьСтадиюОбъектов]
- `HierarchyLink CreateHierarchyLink(RefObj parentObject, RefObj childObject)` [RU: НайтиЗагруженныйОбъект]
- `SearchTerm SearchTerm(String parameter, String operator, Object value)` [RU: НайтиОбъекты]
- `Void Error(String text, Object[] args)` [RU: НайтиЗагруженныйОбъект]
- `Void Message(String caption, String text, Object[] args) (+1)` [RU: НайтиОбъекты]
- `Boolean Question(String text)` [RU: СоздатьОбъект]
- `Nullable`1 QuestionWithCancel(String text)` [RU: СоздатьОбъект]
- `Void Break()` [RU: Прервать]
- `Void Cancel(String text, Object[] args) (+2)` [RU: Прервать]
- `Void CloseDialog(Boolean saveChanges, Boolean showConfirmationOnCancel)` [RU: НайтиЗагруженныйОбъект]
- `Void RaiseEvent(String eventName)` [RU: СоздатьОбъект]
- `Object RunMacro(String macro, String entryPoint, Object[] parameters)` [RU: НайтиОбъекты]
- `UserDialogObjectAccessor GetUserDialog(String userDialogTypeName, Boolean emptyDialog) (+1)` [RU: СоздатьОбъект]
- `InputDialog CreateInputDialog(String caption)` [RU: СоздатьОбъект]
- `OpenFileDialog CreateOpenFileDialog(String caption)` [RU: СоздатьОбъект]
- `SaveFileDialog CreateSaveFileDialog(String caption)` [RU: СоздатьОбъект]
- `OpenFolderDialog CreateOpenFolderDialog(String caption)` [RU: СоздатьОбъект]
- `SelectObjectsDialog CreateSelectObjectsDialog(String referenceName)` [RU: СоздатьОбъект]
- `SelectObjectsFromReferencesDialog CreateSelectObjectsFromReferencesDialog()` [RU: Прервать]
- `SelectListObjectsDialog CreateSelectListObjectsDialog(RefObjList refObjList)` [RU: СоздатьОбъект]
- `SelectClassObjectsDialog CreateSelectClassObjectsDialog(String referenceName)` [RU: СоздатьОбъект]
- `Void OpenReferenceWindow(String referenceName, String filter, RefObj rootObject, String viewName, String catalogFolder)` [RU: ОткрытьОкноСправочника]
- `Boolean ShowPropertyDialog(RefObj refObj, Boolean showInNewWindow, Boolean showConfirmationOnCancel) (+3)` [RU: НайтиЗагруженныйОбъект]
- `ClassRefObj ShowClassObjectSelectionDialog(String referenceName, String caption)` [RU: НайтиЗагруженныйОбъект]
- `KeyValuePair`2 IconWithText(String icon, String text)` [RU: НайтиЗагруженныйОбъект]
- `KeyValuePair`2 UniversalIconWithText(String icon, String text)` [RU: НайтиЗагруженныйОбъект]
- `IconObj GetIcon(String icon)` [RU: СоздатьОбъект]
- `ValueList GetValueList(String parameterName, String referenceName, String objectList)` [RU: НайтиОбъекты]
- `Void SaveAll(Boolean checkIn, String comment, Boolean executeCallback)` [RU: НайтиОбъекты]
- `Void CancelAll(Boolean undoCheckOut)` [RU: СоздатьОбъект]
- `Void CheckInObjects(RefObjList objects, String comment, Boolean showDialog)` [RU: НайтиОбъекты]
- `Void UndoCheckOutObjects(RefObjList objects)` [RU: СоздатьОбъект]
- `Void RefreshReferenceWindow()` [RU: Прервать]
- `Void RefreshReferenceObjects(RefObjList objects)` [RU: СоздатьОбъект]
- `Void RefreshWorkingPageControl(String[] controls)` [RU: СоздатьОбъект]
- `Void RefreshControls(String[] controls) (+1)` [RU: СоздатьОбъект]
- `Void RefreshPropertiesDialogContent()` [RU: Прервать]
- `Void OpenFilePreview(RefObj file) (+1)` [RU: СоздатьОбъект]
- `Void OpenWorkingPage(String workingPage)` [RU: СоздатьОбъект]
- `MailTaskObj CreateMailTask()` [RU: Прервать]
- `MailMessageObj CreateMailMessage()` [RU: Прервать]
- `Void LogMessage(String message, TypeLogMessageObj typeLogMessage)` [RU: НайтиЗагруженныйОбъект]
- `Void LogText(String text)` [RU: СоздатьОбъект]
- `ClassRefObj[] GetClassObjects(String reference, String[] classObjects)` [RU: НайтиЗагруженныйОбъект]
- `СкопированныеОбъекты СкопироватьОбъект(ObjectAccessor прототип, ObjectAccessor родитель, Boolean копироватьДочерниеОбъекты, Boolean копироватьСвязанныеПрототипы)` [RU alternative]
- `Объект НайтиПрототип(String справочник, String фильтр)` [RU alternative]
- `Подключение СоздатьПодключение(Объект родительскийОбъект, Объект дочернийОбъект)` [RU alternative]
- `Условие Условие(String параметр, String оператор, Object значение)` [RU alternative]
- `Void Ошибка(String текст, Object[] аргументы)` [RU alternative]
- `Void Сообщение(String заголовок, String текст, Object[] аргументы)` [RU alternative]
- `Boolean Вопрос(String текст)` [RU alternative]
- `Nullable`1 ВопросСОтменой(String текст)` [RU alternative]
- `Void Отменить(String текст, Object[] аргументы)` [RU alternative]
- `Void ЗакрытьДиалог(Boolean сохранитьИзменения, Boolean показатьПодтверждениеПриОтмене)` [RU alternative]
- `Void ИнициироватьСобытие(String событие)` [RU alternative]
- `Object ВыполнитьМакрос(String макрос, String метод, Object[] параметры)` [RU alternative]
- `ПользовательскийДиалог ПолучитьПользовательскийДиалог(String наименованиеТипаДиалога, Boolean вернутьПустойДиалог)` [RU alternative]
- `ДиалогВвода СоздатьДиалогВвода(String заголовок)` [RU alternative]
- `ДиалогВыбораФайла СоздатьДиалогВыбораФайла(String заголовок)` [RU alternative]
- `ДиалогСохраненияФайла СоздатьДиалогСохраненияФайла(String заголовок)` [RU alternative]
- `ДиалогВыбораПапки СоздатьДиалогВыбораПапки(String заголовок)` [RU alternative]
- `ДиалогВыбораОбъектов СоздатьДиалогВыбораОбъектов(String справочник)` [RU alternative]
- `ДиалогВыбораОбъектовИзСправочников СоздатьДиалогВыбораОбъектовИзСправочников()` [RU alternative]
- `ДиалогВыбораОбъектовИзНабора СоздатьДиалогВыбораОбъектовИзНабора(Объекты объектыДляВыбора)` [RU alternative]
- `ДиалогВыбораТипов СоздатьДиалогВыбораТипов(String справочник)` [RU alternative]
- `Boolean ПоказатьДиалогСвойств(Объект объект, Boolean вНовомОкне, Boolean показыватьПодтверждениеПриОтмене)` [RU alternative]
- `ТипОбъекта ПоказатьДиалогВыбораТипа(String имяСправочника, String заголовок)` [RU alternative]
- `KeyValuePair`2 ИконкаСТекстом(String иконка, String текст)` [RU alternative]
- `KeyValuePair`2 УниверсальнаяИконкаСТекстом(String иконка, String текст)` [RU alternative]
- `Иконка Иконка(String иконка)` [RU alternative]
- `СписокЗначений ПолучитьСписокЗначений(String параметр, String справочник, String списокОбъектов)` [RU alternative]
- `Void СохранитьВсё(Boolean применитьИзменения, String комментарий, Boolean показыватьДиалогПодтверждения)` [RU alternative]
- `Void ОтменитьВсё(Boolean отменитьИзмененияНаРабочемСтоле)` [RU alternative]
- `Void ПрименитьИзмененияНаРабочемСтоле(Объекты объекты, String комментарий, Boolean показыватьДиалогПодтверждения)` [RU alternative]
- `Void ОтменитьИзмененияНаРабочемСтоле(Объекты объекты)` [RU alternative]
- `Void ОткрытьОкноПросмотра(Объекты файлы)` [RU alternative]
- `Void ОткрытьРабочуюСтраницу(String рабочаяСтраница)` [RU alternative]
- `Void ОбновитьОкноСправочника()` [RU alternative]
- `Void ОбновитьКонтролРабочейСтраницы(String[] именаЭлементовУправления)` [RU alternative]
- `Void ОбновитьКонтентДиалогаСвойств()` [RU alternative]
- `Void ОбновитьЭлементыУправления(String[] именаЭлементовУправления)` [RU alternative]
- `Void ОбновитьОбъектыСправочника(Объекты объекты)` [RU alternative]
- `Задание СоздатьЗадание()` [RU alternative]
- `Сообщение СоздатьСообщение()` [RU alternative]
- `Void ЗаписатьВЛогСообщение(String message, ТипЗаписиЖурнала typeLogMessage)` [RU alternative]
- `Void ЗаписатьВЛогТекст(String text)` [RU alternative]
- `ТипОбъекта[] ПолучитьТипыОбъектов(String справочник, String[] типы)` [RU alternative]
- `Объект НайтиОбъект(String справочник, String параметр, Object значение)` [RU alternative]

### `MacroProviderAccessorExtensions`
**Методы:**
- `ObjectAccessor GetCurrentObject(MacroProvider macroProvider)`
- `HierarchyLinkAccessor GetCurrentHierarchyLink(MacroProvider macroProvider)`
- `ObjectAccessor GetCurrentUser(MacroProvider macroProvider)`

### `MacroReference`
**Свойства:** Instance: MacroReference, Classes: MacroTypes
**Методы:**
- `Macro GetMacro(Guid guid)`
- `Macro Find(Guid guid) (+1)` [has Async]

### `MacroRunHistoryReference`
**Свойства:** Classes: MacroRunHistoryTypes

### `MacroRunHistoryReferenceObject`
**Свойства:** Class: MacroRunHistoryType, StartTime: DateTime, EndTime: DateTime, Duration: Int64, User: String, Host: String, ErrorText: String, EntryPoint: String, Macro: Macro

### `MacroRunHistoryType`
**Свойства:** Classes: MacroRunHistoryTypes, IsRecord: Boolean

### `MacroRunHistoryTypes`
**Свойства:** Record: MacroRunHistoryType

### `MacroTaskAction`
**Свойства:** Connection: ServerConnection, MacroGuid: Guid, Macro: Macro, EntryPoint: String, Data: String, Name: String
**Методы:**
- `TaskActionResult Execute(MacroContext context)`

### `MacroTemplate`
**Методы:**
- `String Run(String text, MacroContext context, IFormulaMacroCreator formulaCreator) (+1)`

### `MacroType`
**Свойства:** IsMacro: Boolean, IsTechnologyMacro: Boolean, IsCSharpMacro: Boolean, IsFlowchartMacro: Boolean, IsTemplateFlowchartMacro: Boolean

### `MacroTypes`
**Свойства:** Macro: MacroType, TechnologyMacro: MacroType, CSharpMacro: MacroType, FlowchartMacro: MacroType, TemplateFlowchartMacro: MacroType

### `MacroValidationResults`
**Свойства:** HasErrors: Boolean, HasWarnings: Boolean, IsTextValidation: Boolean, CompilationResult: CompilationResult, IsFlowchartValidation: Boolean, FlowchartResults: ValidationResults, ResultException: Exception
**Методы:**
- `Void ThrowIfError()`

### `MailAccessInfo`
**Свойства:** AccountId: Nullable`1, OwnerId: Nullable`1, UserObjectId: Int32, UserObject: UserReferenceObject, AccessType: MailAccessType, IsModified: Boolean
**Методы:**
- `MailAccessInfo ToServer()`

### `MailAccessManager`
**Свойства:** Account: Account, Owner: User, AccessType: MailAccessType, Connection: ServerConnection
**Методы:**
- `MailAccessManager GetManager(User user, MailAccessType accessType) (+1)`
- `Void SetMessagesAccess(UserReferenceObject userObject, MailMessagesAccess access)`
- `Void SetTasksAccess(UserReferenceObject userObject, MailTasksAccess access)`
- `Void RemoveAccess(UserReferenceObject userObject)`
- `Void Save()` [has Async]
- `IEnumerator`1 GetEnumerator()`

### `MailAddress`
**Свойства:** Name: String, Email: String

### `MailAppointment`
**Свойства:** IsTask: Boolean
**Методы:**
- `Object GetCoreObject()`
- `MacroContext GetMacroContext()`
- `Void Release()`

### `MailBodyTypeAccessor`
**Свойства:** Text: MailBodyTypeObj, Rtf: MailBodyTypeObj, Html: MailBodyTypeObj, ФорматТекст: ФорматТекста [RU only], ФорматRtf: ФорматТекста [RU only], ФорматHtml: ФорматТекста [RU only]
**Методы:**
- `Object GetRealValue()`

### `MailBodyTypeConverter`
**Методы:**
- `ConvertResponse Convert(MailItem item, MailBodyType to, Object context) (+1)`
- `Converter Conveter(MailBodyType bodyType)`

### `MailCategory`
**Свойства:** Connection: ServerConnection, Icon: IconImage, Id: Int32, Guid: Guid, IsPublic: Boolean, Color: Nullable`1, Name: String, IsModified: Boolean
**Методы:**
- `MailCategory ToServer()`

### `MailCategoryManager`
**Свойства:** Connection: ServerConnection, Categories: ReadOnlyCollection`1
**Методы:**
- `MailCategory Find(Int32 categoryId) (+2)`
- `MailCategory CreateCategory()`
- `MailCategory AddCategory(String name, Nullable`1 color) (+2)`
- `Void RemoveCategories(IEnumerable`1 categories)`
- `Boolean Save()`
- `Void RemoveCategory(MailCategory category, List`1 items)`
- `Void ClearCategories(List`1 items)`
- `Void Reload()`

### `MailCheckStatusField`
**Методы:**
- `List`1 GetComparisonOperators()`

### `MailExtensions`
**Методы:**
- `RuleType ToModel(MailRuleType type)`
- `MailRuleType ToServer(RuleType type)`

### `MailField`
**Свойства:** IsSystem: Boolean, FromExtendedData: Boolean, VisibleInEditor: Boolean, IsXmlDataType: Boolean, XQuery_FieldType: String, XQuery_ElementPath: String, XQuery_AttributeName: String, SupportsTasks: Boolean, SupportsMessages: Boolean, Name: String, Title: String, Nullable: Boolean, Type: ParameterType
**Методы:**
- `Boolean TryGetValue(MailItem item, Object& value)`
- `Boolean TryGetStringValue(MailItem item, String& value)`
- `List`1 GetComparisonOperators()`
- `String ConvertToString(Object value)`
- `String ConvertToServerString(Object value)`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`
- `Object ParseServer(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `MailFolder`
**Свойства:** MessageCount: Int32, UnreadMessageCount: Int32, Type: MailFolderType
**Методы:**
- `MailFolder GetParent()`
- `List`1 GetSubfolders()` [has Async]
- `Boolean HasSubfolders()`
- `List`1 GetMessages(Int32 count, Int32 startIndex) (+1)`
- `List`1 GetUnreadMessages()`
- `List`1 GetReadMessages()`

### `MailFolderAddedHandler`
**Методы:**
- `Void Invoke(MailFolder folder)`
- `IAsyncResult BeginInvoke(MailFolder folder, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `MailItem`
**Свойства:** RealSender: MailUser, Account: Account, IsMessage: Boolean, IsTask: Boolean, Id: Int32, GlobalId: Int32, Guid: Guid, From: MailAddress, To: IEnumerable`1, SentDate: Nullable`1, ReceivedDate: Nullable`1, ReadDate: Nullable`1, Subject: String, BodyType: MailBodyType, Body: String, Categories: MailCategoryCollection, Attachments: AttachmentCollection, AttachmentCount: Int32, VisibleAttachmentCount: Int32, IsModified: Boolean, IsSent: Boolean, IsRead: Boolean, IsDraft: Boolean, IsDeleted: Boolean
**Методы:**
- `Void SetBody(String body, MailBodyType type)`
- `Void ResetAttachments()`
- `MailMessage Reply(Boolean copyBody)`
- `MailMessage ReplyAll(Boolean copyBody)`
- `MailMessage Forward(Boolean copyBody)`
- `Void BuildBody(String text, String comments)`
- `Boolean TryGetValue(MailField field, Object& value)`
- `Boolean TryGetStringValue(MailField field, String& value)`

### `MailItemAttachment`
**Свойства:** Item: MailItem, Name: String, IsMessage: Boolean, IsTask: Boolean

### `MailItemFolder`
**Свойства:** Account: Account, IsModified: Boolean, Id: Int32, Guid: Guid, Name: String, Comment: String, Icon: IconImage, IsSystem: Boolean
**Методы:**
- `Boolean CanDelete()`
- `Boolean SetItemsRead()`
- `Boolean SetItemsUnread()`

### `MailItemReminder`
**Свойства:** Object: Object

### `MailLoadSettings`
**Свойства:** Count: Int32, Startindex: Int32, LoadBody: Boolean, LoadToUsers: Boolean, LoadFromUser: Boolean, ObjectKey: ObjectKey, Filter: Filter

### `MailMessage`
**Свойства:** Account: Account, IsMessage: Boolean, To: MailAddressCollection, Copy: MailAddressCollection, Folder: MailFolder, Uid: Int32, AccountId: Int32
**Методы:**
- `Void Save()`
- `Void Send()`
- `Boolean MoveTo(MailFolder folder)`
- `Boolean SetRead(IEnumerable`1 messages) (+1)`
- `Boolean SetUnread(IEnumerable`1 messages) (+1)`
- `Boolean Delete()`

### `MailMessageAccessor`
**Свойства:** Owner: UserRefObj, Recipients: List`1, CopyRecipients: List`1, Subject: String [RU: Заголовок], Body: String [RU: Заголовок], BodyType: MailBodyTypeObj, SendDate: Nullable`1 [RU: ВремяОтправки], ReceivedDate: Nullable`1 [RU: ВремяОтправки], ReadDate: Nullable`1 [RU: ВремяОтправки], FileAttachments: List`1 [RU: ФайлыВложения], RefObjAttachments: RefObjList, Folder: String [RU: Заголовок], Владелец: Объект [RU only], Получатели: List`1 [RU only], ПолучателиКопии: List`1 [RU only], ФорматТекста: ФорматТекста [RU only], ОбъектыВложения: Объекты [RU only]
**Методы:**
- `Boolean AddRecipient(UserRefObj user)` [RU: ДобавитьПолучателя]
- `Boolean DeleteRecipient(UserRefObj user)` [RU: ДобавитьПолучателя]
- `Boolean AddCopyRecipient(UserRefObj user)` [RU: ДобавитьПолучателя]
- `Boolean DeleteCopyRecipient(UserRefObj user)` [RU: ДобавитьПолучателя]
- `Void Save()` [RU: Сохранить]
- `Void Send()` [RU: Сохранить]
- `Boolean Delete()` [RU: Сохранить]
- `Boolean AddFileAttachments(String filePath)` [RU: ДобавитьПолучателя]
- `Boolean DeleteFileAttachment(String filePath)` [RU: ДобавитьПолучателя]
- `Boolean AddRefObjAttachment(RefObj refObj)` [RU: ДобавитьПолучателя]
- `Boolean DeleteRefObjAttachment(RefObj refObj)` [RU: ДобавитьПолучателя]
- `Object GetRealValue()` [RU: Сохранить]
- `Boolean УдалитьПолучателя(Пользователь пользователь)` [RU alternative]
- `Boolean ДобавитьПолучателяКопии(Пользователь пользователь)` [RU alternative]
- `Boolean УдалитьПолучателяКопии(Пользователь пользователь)` [RU alternative]
- `Void Отправить()` [RU alternative]
- `Void Удалить()` [RU alternative]
- `Boolean ДобавитьФайлВложения(String путьКФайлу)` [RU alternative]
- `Boolean УдалитьФайлВложения(String путьКФайлу)` [RU alternative]
- `Boolean ДобавитьОбъектВложения(Объект объект)` [RU alternative]
- `Boolean УдалитьОбъектВложения(Объект объект)` [RU alternative]

### `MailMessageField`
**Свойства:** SupportsTasks: Boolean

### `MailMessageObj`
**Методы:**
- `MailMessageObj CreateInstance(MailMessage mailMessage, MacroContext context)`

### `MailMessagesAccessInfo`
**Свойства:** AccessType: MailAccessType, Access: MailMessagesAccess
**Методы:**
- `MailAccessInfo ToServer()`

### `MailResolution`
**Свойства:** CanReject: Boolean, Responsible: User, CheckStatus: CheckStatusType, Comment: String

### `MailRule`
**Свойства:** Account: Account, Id: Int32, Guid: Guid, PriorityIndex: Int32, IsActive: Boolean, Name: String, IsModified: Boolean, RuleType: RuleType, UseFromTerm: Boolean, UseSubjectTerm: Boolean, FromAddress: MailAddress, Subject: String, Actions: ReadOnlyCollection`1
**Методы:**
- `Void AddAction(MailRuleAction action)`
- `Void RemoveAction(MailRuleAction action)`

### `MailRuleAction`
**Свойства:** Rule: MailRule, Name: String, IsModified: Boolean
**Методы:**
- `MailRuleAction ToServer()`

### `MailService`
**Свойства:** Connection: ServerConnection, CategoryManager: MailCategoryManager, Accounts: ReadOnlyCollection`1, AccountTemplates: ReadOnlyCollection`1, DOCsAccount: DOCsAccount, ReminderManager: ReminderManager
**Методы:**
- `Void ReloadAccountTemplates()`
- `Boolean RegisterMailField(MailField field)`
- `MailField GetMailField(String name)`
- `ICollection`1 GetMailFields(Boolean isInEditor)`

### `MailSettingFolder`
**Свойства:** Guid: Guid
**Методы:**
- `Int32 GetId()`
- `String GetFolderName()`
- `IconImage GetIcon()`
- `MailItemFolder GetMailItemFolder()`
- `IEnumerable`1 GetMailItems(Filter filter)`

### `MailTask`
**Свойства:** Account: Account, IsTask: Boolean, From: MailUser, OnBehalf: MailUser, Controller: MailUser, CanChangeController: Boolean, Executors: MailTaskExecutorCollection, To: MailTaskToCollection, Emails: List`1, StartDate: Nullable`1, EndDate: Nullable`1, CanChangeEndDate: Boolean, CheckDate: Nullable`1, CanChangeCheckDate: Boolean, PercentComplete: Int32, Priority: MailTaskPriority, Status: MailTaskStatus, ParentTask: MailTask, IsAttachment: Boolean, AcceptType: MailTaskAcceptType, CanAccept: Boolean, CanReject: Boolean, CanComplete: Boolean, CanCancel: Boolean, CanSuspend: Boolean, CanRestore: Boolean, CanUpdatePercentComplete: Boolean, CanDelete: Boolean, CanDelegate: Boolean
**Методы:**
- `Void Save()`
- `Void Send()`
- `Boolean CanAddExecutor(MailTaskExecutor item)`
- `Boolean Accept()`
- `Boolean Reject(String comment)`
- `Boolean Complete(String comment, Object state)`
- `Boolean Cancel(String comment)`
- `Boolean Suspend()`
- `Boolean Restore()`
- `Void ReloadExecutors()`
- `Boolean UpdatePercentComplete(Int32 percentComplete)`
- `Boolean SetRead(IEnumerable`1 tasks) (+1)`
- `Boolean SetUnread(IEnumerable`1 tasks) (+1)`
- `Boolean Delete(IEnumerable`1 tasks) (+1)`
- `MailTask Delegate()`
- `MailTask Replan()`

### `MailTaskAccessor`
**Свойства:** Subject: String [RU: Тема], Body: String [RU: Тема], StartDate: Nullable`1 [RU: ДатаНачала], EndDate: Nullable`1 [RU: ДатаНачала], CheckDate: Nullable`1 [RU: ДатаНачала], Executors: RefObjList, FileAttachments: List`1 [RU: ФайлыВложения], RefObjAttachments: RefObjList, PropertyHyperlink: String [RU: Тема], Hyperlink: String [RU: Тема], Исполнители: Объекты [RU only], ОбъектыВложения: Объекты [RU only]
**Методы:**
- `Void Save()` [RU: Сохранить]
- `Void Send()` [RU: Сохранить]
- `Boolean AddExecutor(String fullName) (+1)` [RU: ДобавитьИсполнителя]
- `Boolean DeleteExecutor(String fullName) (+1)` [RU: ДобавитьИсполнителя]
- `Boolean AddFileAttachment(String filePath)` [RU: ДобавитьИсполнителя]
- `Boolean DeleteFileAttachment(String filePath)` [RU: ДобавитьИсполнителя]
- `Boolean AddRefObjAttachment(RefObj refObj)` [RU: ДобавитьИсполнителя]
- `Boolean DeleteRefObjAttachment(RefObj refObj)` [RU: ДобавитьИсполнителя]
- `Object GetRealValue()` [RU: Сохранить]
- `Void Отправить()` [RU alternative]
- `Boolean УдалитьИсполнителя(String исполнитель)` [RU alternative]
- `Boolean ДобавитьФайлВложения(String путьКФайлу)` [RU alternative]
- `Boolean УдаляетФайлВложения(String путьКФайлу)` [RU alternative]
- `Boolean УдалитьФайлВложения(String путьКФайлу)` [RU alternative]
- `Boolean ДобавитьОбъектВложения(Объект объект)` [RU alternative]
- `Boolean УдалитьОбъектВложения(Объект объект)` [RU alternative]

### `MailTaskExecutor`
**Свойства:** Name: String, User: User, UserId: Int32, ReceivedDate: Nullable`1, ReadDate: Nullable`1, AcceptDate: Nullable`1, CompleteDate: Nullable`1, PercentComplete: Int32, Status: MailTaskStatus, Comment: String

### `MailTaskExtensions`
**Методы:**
- `String GetCaption(MailTaskPriority priority) (+1)`
- `String GetPropertyHyperlink(MailTask mailTask, String serverAddress)` [has Async]
- `String GetHyperlink(MailTask mailTask, String serverAddress)` [has Async]

### `MailTaskField`
**Свойства:** SupportsMessages: Boolean
**Методы:**
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `MailTaskObj`
**Методы:**
- `MailTaskObj CreateInstance(MailTask mailTask, MacroContext context)`

### `MailTaskPriorityConverter`
**Методы:**
- `Object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, Object value, Type destinationType)`

### `MailTasksAccessInfo`
**Свойства:** AccessType: MailAccessType, Access: MailTasksAccess
**Методы:**
- `MailAccessInfo ToServer()`

### `MailTaskStatusConverter`
**Методы:**
- `Object ConvertTo(ITypeDescriptorContext context, CultureInfo culture, Object value, Type destinationType)`

### `MailTerm`
**Свойства:** Field: MailField, ParameterName: String

### `MailUpdateProvider`
**Методы:**
- `MailMessage[] Update(IEnumerable`1 messages)`

### `MailUser`
**Свойства:** Connection: ServerConnection, Name: String, Email: String, User: User, UserId: Int32

### `ManualAssignmentFolderReferenceObject`
**Свойства:** LinkedAssignments: IEnumerable`1
**Методы:**
- `Void AddAssignments(IEnumerable`1 assignments)`
- `Void RemoveAssignments(IEnumerable`1 assignments)`

### `MappingOptions`
**Свойства:** Mode: TreeMovingMode, Macros: Macro, MethodName: String, UniqueKeyPath: IEnumerable`1, ValidateConflicts: Boolean

### `MaskTypeAccessor`
**Свойства:** Simple: TypeOfMask, Numeric: TypeOfMask, TimeSpan: TypeOfMask, DateTime: TypeOfMask, RegEx: TypeOfMask, Простая: ТипМаски [RU only], Числовая: ТипМаски [RU only], ПромежутокВремени: ТипМаски [RU only], ДатаИВремя: ТипМаски [RU only], РегулярноеВыражение: ТипМаски [RU only]
**Методы:**
- `Object GetRealValue()`

### `MasterFileReferenceObject`
**Свойства:** ByDefault: BooleanParameter
**Методы:**
- `List`1 GetDefaultSecondaryRepresentations()`
- `SecondaryRepresentationReferenceObject AddLinkDefaultRepresentation(SecondaryRepresentationReferenceObject secondaryRepresentation)`
- `Boolean RemoveLinkDefaultRepresentation(SecondaryRepresentationReferenceObject secondaryRepresentation)`

### `MasterObjectPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `MasterServerMacroProvider`
**Методы:**
- `Void Disconnect()` [RU: Отключиться]

### `MasterServerPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `MaterialMarkPhysicalPropertiesReference`
**Свойства:** Classes: MaterialMarkPhysicalPropertiesTypes

### `MaterialMarkPhysicalPropertiesReferenceObject`
**Свойства:** Class: MaterialMarkPhysicalPropertiesType, Density: DoubleParameter, HeatConductivity: DoubleParameter, HeatCapacity: DoubleParameter, HeatExpansionLinear: DoubleParameter, HeatExpansionVolume: DoubleParameter, ElectroConductivity: DoubleParameter, KickViscosity: DoubleParameter, HB: DoubleParameter, HR: DoubleParameter, HV: DoubleParameter, SpinSoundness: DoubleParameter, BreakSoundness: DoubleParameter, DielectricSoundness: DoubleParameter, Condition: StringParameter, ThermalTreatment: StringParameter, Temperature: DoubleParameter, MeltingTemperature: DoubleParameter, YieldStrength: DoubleParameter, CompressionStrength: DoubleParameter, ElasticModulus: DoubleParameter, PoissonRatio: DoubleParameter

### `MaterialMarkPhysicalPropertiesType`
**Свойства:** Classes: MaterialMarkPhysicalPropertiesTypes, IsPhysicalProperties: Boolean

### `MaterialMarkPhysicalPropertiesTypes`
**Свойства:** PhysicalProperties: MaterialMarkPhysicalPropertiesType

### `MaterialMarkReference`
**Свойства:** Classes: MaterialMarkTypes

### `MaterialMarkReferenceObject`
**Свойства:** Class: MaterialMarkType, PhysicalProperties: ReferenceObjectCollection, VisualProperties: MaterialsVisualPropertiesReferenceObject, MaterialInterChangeLink: ReferenceObjectCollection, MaterialIncompatibilityLink: ReferenceObjectCollection, MaterialWeldabilityLink: ReferenceObjectCollection, MaterialChemicalStructure: ReferenceObjectCollection, MaterialMarkLinksAssortment: ReferenceObjectCollection, MaterialLinksMark: ReferenceObjectCollection, PartMaterial: ReferenceObjectCollection
**Методы:**
- `ReferenceObject CreatePhysicalProperties(Guid listObjectClass) (+1)`
- `ReferenceObject AddMaterialInterChangeLink(ReferenceObject newLinkedObject)`
- `Boolean RemoveMaterialInterChangeLink(ReferenceObject linkedObject)`
- `ReferenceObject AddMaterialIncompatibilityLink(ReferenceObject newLinkedObject)`
- `Boolean RemoveMaterialIncompatibilityLink(ReferenceObject linkedObject)`
- `ReferenceObject AddMaterialWeldabilityLink(ReferenceObject newLinkedObject)`
- `Boolean RemoveMaterialWeldabilityLink(ReferenceObject linkedObject)`
- `ReferenceObject CreateMaterialChemicalStructure(Guid listObjectClass) (+1)`
- `ReferenceObject AddMaterialMarkLinksAssortment(ReferenceObject newLinkedObject)`
- `Boolean RemoveMaterialMarkLinksAssortment(ReferenceObject linkedObject)`
- `ReferenceObject AddMaterialLinksMark(ReferenceObject newLinkedObject)`
- `Boolean RemoveMaterialLinksMark(ReferenceObject linkedObject)`
- `ReferenceObject AddPartMaterial(ReferenceObject newLinkedObject)`
- `Boolean RemovePartMaterial(ReferenceObject linkedObject)`

### `MaterialMarkType`
**Свойства:** Classes: MaterialMarkTypes, IsAbstractMaterialMark: Boolean, IsFolder: Boolean

### `MaterialMarkTypes`
**Свойства:** MaterialMark: MaterialMarkType, Folder: MaterialMarkType, Metal: MaterialMarkType, Steel: MaterialMarkType, Alloys: MaterialMarkType, CastIron: MaterialMarkType, Polymer: MaterialMarkType

### `MaterialPhysicalProperties`
**Свойства:** Density: Double, Stress: Double, CompressionLimit: Double, YieldStrength: Double, SpecificHeat: Double, Elasticity: Double, Puasson: Double, Expansion: Double, ThermalConductivity: Double

### `MaterialReference`
**Свойства:** Classes: MaterialTypes

### `MaterialReferenceObject`
**Свойства:** PhysicalProperties: IPhysicalProperties, VisualProperties: IVisualProperties, Name: StringParameter, Denotation1: StringParameter, Denotation2: StringParameter, Denotation3: StringParameter, Denotation4: StringParameter, MaterialMark: AbstractMarkReferenceObject

### `MaterialResourceLinkObject`
**Свойства:** SpendingType: ResourceSpendingType, AutoCalc: Boolean, Price: Double
**Методы:**
- `Void UpdateValue()`

### `MaterialsVisualPropertiesReference`
**Свойства:** Classes: MaterialsVisualPropertiesTypes

### `MaterialsVisualPropertiesReferenceObject`
**Свойства:** Class: MaterialsVisualPropertiesType, Name: StringParameter, AmbientColor: Int32Parameter, DiffuseColor: Int32Parameter, SpecularColor: Int32Parameter, EmissiveColor: Int32Parameter, Shininess: DoubleParameter, Reflection: DoubleParameter, Transparency: DoubleParameter, BumpType: Int32Parameter, PatternType: StringParameter, PatternScale: DoubleParameter, MaterialTexture: ReferenceObject, MaterialBumpTexture: ReferenceObject

### `MaterialsVisualPropertiesType`
**Свойства:** Classes: MaterialsVisualPropertiesTypes, IsMaterialMarkVisualProperties: Boolean

### `MaterialsVisualPropertiesTypes`
**Свойства:** MaterialMarkVisualProperties: MaterialsVisualPropertiesType

### `MaterialType`
**Свойства:** Classes: MaterialTypes, IsMaterial: Boolean

### `MaterialTypes`
**Свойства:** Material: MaterialType

### `MathExtensions`
**Методы:**
- `Double DegreesToRadians(Double degrees) (+1)`
- `Double RadiansToDegrees(Double radians)`

### `MdiTypeExtension`
**Методы:**
- `String GetText(MdiType mdiType)`
- `IconImage GetIcon(MdiType mdiType)`
- `AccessCommand GetAccessCommand(MdiType mdiType)`
- `Boolean IsAdministrationMdiType(MdiType mdiType)`

### `MenuLink`
**Свойства:** OpenType: LinkOpenType

### `MenuLinkGroup`
**Свойства:** Configuration: WebConfiguration, IsRoot: Boolean, SourceText: String, Text: String, HideNavigationMenu: Boolean, ShowHeader: Boolean, ShowFooter: Boolean, Address: String, Children: LinkGroupCollection, Parent: MenuLinkGroup, Icon: IconImage, HasChildren: Boolean, CanContainChildren: Boolean, Theme: String
**Методы:**
- `String GetFullAddress(String source)`
- `Void AddChild(MenuLinkGroup group)`

### `MessageCountChangedHandler`
**Методы:**
- `Void Invoke(MailFolder folder)`
- `IAsyncResult BeginInvoke(MailFolder folder, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `MessageLoadSettings`
**Свойства:** LoadCopyUsers: Boolean

### `MessageRecipient`
**Свойства:** RecipientType: MessageRecipientType, Value: String

### `MessageTemplate`
**Свойства:** FormatType: FormatType, Class: MessageTemplateType, Name: StringParameter, Header: StringParameter, Body: StringParameter, TextFormat: Int32Parameter
**Методы:**
- `String FormatHeader(MacroContext context, IFormulaMacroCreator formulaCreator) (+1)`
- `ValueTuple`2 FormatHeaderWithExceptionsFixation(MacroContext context)`
- `String FormatBody(MacroContext context, IFormulaMacroCreator formulaCreator) (+1)`
- `ValueTuple`2 FormatBodyWithExceptionsFixation(MacroContext context)`
- `Object Calculate(String formula, MacroContext context)`
- `ValueTuple`2 CalculateWithExceptionFixation(String formula, MacroContext context)`
- `Object GetValue(String formula, MacroContext context)`
- `String FormatText(String text, MacroContext context, FormatType formatType, IFormulaMacroCreator formulaCreator) (+1)`
- `ValueTuple`2 FormatTextWithExceptionsFixation(String text, MacroContext context, FormatType formatType, IFormulaMacroCreator formulaCreator) (+1)`

### `MessageTemplateReference`
**Свойства:** Classes: MessageTemplateTypes

### `MessageTemplateType`
**Свойства:** Classes: MessageTemplateTypes, IsMessageTemplate: Boolean

### `MessageTemplateTypes`
**Свойства:** MessageTemplate: MessageTemplateType

### `ModelObject`
**Свойства:** Name: String, UniqueId: String

### `ModelObjectCollection`1`
**Свойства:** Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Boolean Add(T modelObject)`
- `T Find(String name)`
- `Void ForEach(Action`1 action)`
- `IEnumerator`1 GetEnumerator()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`

### `ModelObjectData`
**Свойства:** Name: String, UniqueId: String

### `ModificationActionReferenceObject`
**Свойства:** Class: ModificationActionType, Content: StringParameter, IsAutoText: BooleanParameter

### `ModificationActionsReference`
**Свойства:** Classes: ModificationActionTypes

### `ModificationActionType`
**Свойства:** Classes: ModificationActionTypes, IsDeleteAction: Boolean, IsAddAction: Boolean, IsEditAction: Boolean, IsReplaceAction: Boolean, IsEditObjectAction: Boolean

### `ModificationNoticeBaseReferenceObject`
**Свойства:** Name: StringParameter, AssignedTo: StringParameter, ReleaseDate: DateTimeParameter, ChangingDate: DateTimeParameter, ReserveComment: StringParameter, IntroductionComment: StringParameter, Text: StringParameter, ChangingReason: StringParameter, ChangingState: Int32Parameter, EditStageParameter: GuidParameter, ReadonlyStageParameter: GuidParameter, EditStage: Stage, ReadonlyStage: Stage, LinkedFiles: ReferenceObject[], LinkedObjects: ReferenceObject[], LinkedObjectsGuid: Guid, LinkedFilesGuid: Guid
**Методы:**
- `Void SetReadyToApplyState()`

### `ModificationNoticeType`
**Свойства:** Classes: ModificationNoticeTypes, IsNFC: Boolean, IsAdditionalNFC: Boolean, IsPreliminaryNFC: Boolean, IsAdditionalPreliminaryNFC: Boolean, IsProposalToChange: Boolean

### `ModificationNoticeTypes`
**Методы:**
- `ClassObject GetModificationNoticeBaseClass()`

### `ModificationNoticeWithActionsReferenceObject`
**Свойства:** ActionObjects: ActionReferenceObject[]
**Методы:**
- `Void RaiseActionChangingObjectChange(ActionReferenceObject action, Boolean isAdded, ReferenceObject oldLinkedObject)`
- `Void RaiseActionDeleted(ActionReferenceObject action)`
- `Void SetReadyToApplyState()`
- `Void SetApplyingState()`
- `Boolean SetAppliedState(Boolean useStatusForActions) (+1)`

### `ModificationReference`
**Свойства:** Classes: ModificationTypes

### `ModificationReferenceObject`
**Свойства:** Class: ModificationType, Name: StringParameter, ModificationContent: StringParameter, UsingAreaContent: StringParameter, ModificationNotice: ReferenceObject, DesignContext: DesignContextObject

### `ModificationType`
**Свойства:** Classes: ModificationTypes, IsModification: Boolean

### `ModificationTypes`
**Свойства:** Modification: ModificationType

### `ModificationUsingAreaReference`
**Свойства:** Classes: ModificationUsingAreaTypes

### `ModificationUsingAreaReferenceObject`
**Свойства:** Class: ModificationUsingAreaType, Content: StringParameter, IsAutoText: BooleanParameter
**Методы:**
- `List`1 GetHierarchyLinkMatches()`
- `Void CreateHierarchyLinkMatching(ComplexHierarchyLink sourceLink, ComplexHierarchyLink addedLink, ComplexHierarchyLink deletedLink, Int32 action)`

### `ModificationUsingAreaType`
**Свойства:** Classes: ModificationUsingAreaTypes, IsUsingArea: Boolean

### `ModificationUsingAreaTypes`
**Свойства:** UsingAreaType: ModificationUsingAreaType

### `ModuleLicense`
**Свойства:** Id: Int32, IsModuleSet: Boolean, Name: String, Functions: IList`1
**Методы:**
- `List`1 GetLicenses()`

### `ModuleSetLicense`
**Свойства:** Modules: IList`1, IsModuleSet: Boolean

### `MonthElementReferenceObject`
**Свойства:** ShowLeadingZeros: BooleanParameter
**Методы:**
- `String GetTestValue(String parameter)`

### `MonthelyObject`
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `MonthTrigger`
**Свойства:** Months: Boolean[], MonthDays: Boolean[], LastDay: Boolean, Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `MoveFileReferenceObjectToStorageContext`
**Свойства:** CheckedOutObjectsWithChangedStorage: HashSet`1, Type: DesktopOperationInfoContextType

### `NamePathItem`
**Свойства:** Name: String, Type: PathItemType, Icon: IconImage, SupportSearchType: SupportSearchTypes

### `NamespaceInfo`
**Свойства:** Namespace: String, Assembly: String

### `NavigationPanelReference`
**Свойства:** CommonFolder: ReferenceObject, PrivateFolder: ReferenceObject, Classes: NavigationPanelTypes
**Методы:**
- `List`1 GetRootObjects()`
- `Void RefreshDesktop()`
- `Boolean IsDesktop(GroupObject group)`

### `NavigationPanelReferenceObject`
**Свойства:** NameParameter: StringParameter, IconParameter: IconParameter, DataParameter: StringParameter, Data: String, Icon: IconImage, IconGuid: Guid, Class: NavigationPanelType
**Методы:**
- `Void SetIcon(IconImage icon, Guid iconGuid)`

### `NavigationPanelType`
**Свойства:** Classes: NavigationPanelTypes, IsFolder: Boolean, IsGroup: Boolean, IsShortcut: Boolean

### `NavigationPanelTypes`
**Свойства:** Group: NavigationPanelType, Folder: NavigationPanelType, Shortcut: NavigationPanelType

### `NomenclatureAnalogueReferenceObject`
**Свойства:** AnalogueLinkedObject: ReferenceObject

### `NomenclatureEquivalentGroupReference`
**Свойства:** Classes: NomenclatureEquivalentGroupTypes

### `NomenclatureEquivalentGroupReferenceObject`
**Свойства:** Class: NomenclatureEquivalentGroupType, Comment: StringParameter, Count: DoubleParameter, EquivalentLinkedObject: ReferenceObject

### `NomenclatureEquivalentGroupType`
**Свойства:** Classes: NomenclatureEquivalentGroupTypes, IsNomenclatureEquivalentGroupReferenceObject: Boolean

### `NomenclatureEquivalentGroupTypes`
**Свойства:** NomenclatureEquivalentGroupReferenceObject: NomenclatureEquivalentGroupType

### `NomenclatureEquivalentReferenceObject`
**Свойства:** EquivalentGroup: IEnumerable`1
**Методы:**
- `ReferenceObject CreateEquivalentGroup(Guid listObjectClass) (+1)`
- `Void FormatComment()`

### `NomenclatureHierarchyLink`
**Свойства:** Amount: DoubleParameter, Unit: StringParameter, Remarks: StringParameter, UseInSpecification: BooleanParameter, UseInStructure: BooleanParameter, BomSection: StringParameter, Position: Int32Parameter, AmountForAssembly: DoubleParameter, AmountForComplect: DoubleParameter, XMin: DoubleParameter, XMax: DoubleParameter, YMin: DoubleParameter, YMax: DoubleParameter, ZMin: DoubleParameter, ZMax: DoubleParameter, Placement: StringParameter, StructureTypes: StructureTypesCollection, CadDocumentContext: ByteArrayParameter, CadObjectIdentifier: GuidParameter, PassToCad: BooleanParameter, CategoriesLink: OneToManyLink, ProductStructure: Int32, InsertedProductStructureId: Nullable`1
**Методы:**
- `Void BeginChanges(Boolean forceEndChanges)`
- `Boolean RestoreLink()`
- `Void UpdateFromLink(ComplexHierarchyLink sourceHierarchyLink, Boolean copyParameters, CopyReferenceObjectsContext copyContext, Boolean copyApplicability) (+1)`
- `Boolean SubstituteForCurrentDesignContext()`
- `Void ApplyDesignContextChangesToMainContext()`
- `Void MoveDesignContextChangesToOtherContext(DesignContextObject designContext)`
- `Void CancelDesignContextChanges()`

### `NomenclatureLinkedObjectStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean, ShowCreateCommandLock: Nullable`1, ShowAddCommandLock: Nullable`1, ShowDeleteCommandLock: Nullable`1, ShowRemoveCommandLock: Nullable`1, CanContainMultipleReferencesDetalization: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `NomenclatureObject`
**Свойства:** Denotation: StringParameter, VariantName: StringParameter, Code: StringParameter, Version: StringParameter, Format: StringParameter, Mass: DoubleParameter, IsEndOfProduct: BooleanParameter, Letter: StringParameter, AltRepName: StringParameter, AltRepCode: StringParameter, AltRepGroupGuid: GuidParameter, IsAltRep: Boolean, BaseVersion: NomenclatureObject, IsVersion: Boolean, IsBaseVersion: Boolean, IsVariant: Boolean, ModificationNotices: ModificationNoticeWithActionsReferenceObject[], HasLinkedObject: Boolean, LinkedObject: ReferenceObject, IsLinkedObjectLoaded: Boolean, LinkedObjectId: Int32, LinkedObjectReferenceId: Int32, IsMaterialObject: Boolean
**Методы:**
- `Void SetBaseVersion(NomenclatureObject newBaseVersion, String versionName, String denotation)`
- `String GetBaseDenotation()`
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`
- `List`1 GetVersions()` [has Async]
- `List`1 GetVariants()` [has Async]
- `NomenclatureObject GetMainObject()` [has Async]
- `Boolean IsVariantOf(NomenclatureObject object)`
- `NomenclatureObject CreateVersion(String versionName, Boolean copyChildren, Boolean copyFiles, IEnumerable`1 skip, Boolean changeCopyFilesFolder, String copyFilesFolderPath, String denotation) (+3)`
- `NomenclatureObject CreateAltRep(String altRepName, String altRepCode, Boolean copyChildren, IEnumerable`1 skip, Boolean copyFiles, String copyFilesNewFolderPath) (+1)`
- `NomenclatureObject CreateVariant(String variantName, Boolean copyChildren, Boolean copyFiles, IEnumerable`1 skip, Boolean changeCopyFilesFolder, String copyFilesFolderPath) (+3)`
- `List`1 UpdateByVariant(NomenclatureObject variantObject)`
- `List`1 GetSimilarObjects()`
- `ComplexHierarchyLink AddToParent(NomenclatureReferenceObject parentObject, IDictionary`2 linkParameters)`
- `List`1 GetAltReps()` [has Async]
- `Boolean CanCopy(ParameterInfo parameter) (+1)`
- `NomenclatureObject GetBaseRepresentationObject()` [has Async]

### `NomenclatureObjectEntrancesTree`
**Свойства:** MainObject: NomenclatureObject, ProductStructure: ProductStructureReferenceObject, StructuresEntrances: IEnumerable`1, IncludeStructures: Boolean, ExpandEndProducts: Boolean
**Методы:**
- `Void Reload(Boolean includeStructures, Boolean expandEndProducts)`

### `NomenclatureObjectPathElement`
**Свойства:** DefaultType: DefaultSupportedType
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean IsEqual(PathElement pathElement)`

### `NomenclatureObjectPathItem`
**Свойства:** Name: String, Type: PathItemType, UseLinkSeparator: Boolean, SupportSearchType: SupportSearchTypes

### `NomenclatureReference`
**Свойства:** DigitalStructureContext: DigitalStructureContext, Classes: NomenclatureTypes, LinkedToProductStructure: Boolean
**Методы:**
- `NomenclatureObject FindByLinkedObject(ReferenceObject linkedObject)` [has Async]
- `Dictionary`2 FindByLinkedObjects(IEnumerable`1 linkedObjects)` [has Async]
- `NomenclatureObject CreateNomenclatureObject(ReferenceObject linkedObject, NomenclatureReferenceObject parentObject, IDictionary`2 linkParameters, NomenclatureObject source, Boolean checkRevisions, Boolean isRevisionsContainer, Guid revisionsContainerGuid) (+1)`
- `List`1 CreateNomenclatureObjects(CreateObjectsData objectsData)` [has Async]
- `EntrancesTree GetEntrances(NomenclatureObject nomenclatureObject, Boolean includeStructures, Boolean expandEndProducts)`
- `ComplexHierarchyLink CreateEmptyHierarchLink(ReferenceObject childObject)`

### `NomenclatureReferenceAccessor`
**Методы:**
- `RefObj LinkObject(RefObj refObj, RefObj parentObject) (+1)` [RU: Подключить]
- `RefObj CreateObject(String className, RefObj parentObject) (+1)` [RU: Подключить]
- `Объект СоздатьОбъект(String имяТипа, Объект родительскийОбъект)` [RU alternative]

### `NomenclatureReferenceObject`
**Свойства:** ProductStructureId: Int32, InsertedProductStructureId: Int32, Parent: NomenclatureReferenceObject, Class: NomenclatureType, Name: StringParameter, MainMaterialLink: OneToOneLink, MainMaterial: MaterialReferenceObject, LinkedTPReference: Reference, CanContainChildren: Boolean
**Методы:**
- `List`1 GetFiles()`
- `ComplexHierarchyLink CreateParentLink(ReferenceObject parentObject)`
- `ComplexHierarchyLink CreateChildLink(ReferenceObject childObject)`
- `ComplexHierarchyLinkInstanceData CreateChildLinkWithInstancesData(ReferenceObject childObject, ReferenceObjectInstance sourceStructureObjectInstance, ReferenceObjectInstance parentObjectInstance)`
- `ComplexHierarchyLinkInstanceData CreateChildLinkWithBaseInstancesData(ReferenceObject childObject, ReferenceObjectInstance baseInstance, ReferenceObjectInstance currentObjectInstance)`
- `Boolean CanCreateChildObject(ClassObject childClass)`

### `NomenclatureRule`
**Свойства:** NomenclatureParameter: ParameterInfo, ReferenceParameter: ParameterInfo
**Методы:**
- `Boolean CanCreateFor(ParameterInfo nomenclatureParameter, ParameterInfo referenceParameter)`

### `NomenclatureSubstituteReferenceObject`
**Свойства:** Comment: StringParameter, Class: NomenclatureSubstitutesType

### `NomenclatureSubstitutesReference`
**Свойства:** Classes: NomenclatureSubstitutesTypes

### `NomenclatureSubstitutesType`
**Свойства:** Classes: NomenclatureSubstitutesTypes, IsNomenclatureAnalogueReferenceObject: Boolean, IsNomenclatureEquivalentReferenceObject: Boolean

### `NomenclatureSubstitutesTypes`
**Свойства:** NomenclatureAnalogueReferenceObject: NomenclatureSubstitutesType, NomenclatureEquivalentReferenceObject: NomenclatureSubstitutesType

### `NomenclatureType`
**Свойства:** Classes: NomenclatureTypes, IsFolder: Boolean, IsObject: Boolean, IsMaterialObject: Boolean, IsDocument: Boolean, IsBillOfMaterials: Boolean, IsMaterial: Boolean, IsAssembly: Boolean, IsDetail: Boolean, IsStandardItem: Boolean, IsDrawing: Boolean, IsTechnologicalProcess: Boolean, IsEquipment: Boolean, IsTechnologicalNode: Boolean, IsProduct: Boolean, IsPiece: Boolean, IsScheme: Boolean, IsOtherProducts: Boolean, SupportsVersions: Boolean, SupportsAltReps: Boolean, HasLinkedClass: Boolean, LinkedClassId: Int32, LinkedClass: ClassObject, LinkedReferenceId: Int32, LinkedReferenceInfo: ReferenceInfo, LinkedReference: Reference, LinkedInheritClasses: Boolean, BaseNomenclatureType: NomenclatureType, Rules: ReadOnlyCollection`1, Attributes: NomenclatureTypeAttributes
**Методы:**
- `Boolean CreateInheritClasses()`
- `NomenclatureRule FindRule(ParameterInfo parameter)`

### `NomenclatureTypeAttribute`
**Свойства:** HierarchyParameter: ParameterInfo, IsSystem: Boolean, CanChangeCaption: Boolean, Caption: String, Value: Object, CanRemove: Boolean

### `NomenclatureTypeAttributes`
**Свойства:** DefaultNewObjectFolder: DefaultNewObjectFolderAttribute

### `NomenclatureTypeBuilder`
**Свойства:** Classes: NomenclatureTypes, Class: NomenclatureType, Base: NomenclatureType, LinkedClass: ClassObject, LinkedInheritClasses: Boolean

### `NomenclatureTypes`
**Свойства:** Folder: NomenclatureType, Object: NomenclatureType, MaterialObject: NomenclatureType, Document: NomenclatureType, Detail: NomenclatureType, Assembly: NomenclatureType, Drawing: NomenclatureType, StandardItem: NomenclatureType, Material: NomenclatureType, Product: NomenclatureType, TechnologicalProcess: NomenclatureType, TechnologicalNode: NomenclatureType, Complete: NomenclatureType, Complex: NomenclatureType, ElectronicComponent: NomenclatureType, Equipment: NomenclatureType, Piece: NomenclatureType, BillOfMaterials: NomenclatureType, Scheme: NomenclatureType, OtherProduct: NomenclatureType
**Методы:**
- `IReadOnlyCollection`1 GetLinkedGroups()`
- `ParameterGroup FindLinkedGroup(Int32 id) (+1)`

### `NomParametersMatchingReference`
**Свойства:** Classes: NomParametersMatchingTypes

### `NomParametersMatchingReferenceObject`
**Свойства:** Class: NomParametersMatchingType, LinkedReferenceParameter: GuidParameter, NomenclatureParameter: GuidParameter

### `NomParametersMatchingType`
**Свойства:** Classes: NomParametersMatchingTypes, IsNomParametersMatchingReferenceObject: Boolean

### `NomParametersMatchingTypes`
**Свойства:** NomParametersMatchingReferenceObject: NomParametersMatchingType

### `NomParametersSynchroReference`
**Свойства:** Classes: NomParametersSynchroTypes
**Методы:**
- `Guid GetLinkGuidToLinkedReference(Guid classGuid, Guid referenceGuid)` [has Async]
- `NomParametersSynchroReferenceObject GetParametersSynchronizationObject(Guid classGuid, Guid referenceGuid, Boolean includeLinkedInheritClasses)` [has Async]
- `Boolean SupportsNomenclature(Guid referenceGuid)`

### `NomParametersSynchroReferenceObject`
**Свойства:** Class: NomParametersSynchroType, NomenclatureClass: GuidParameter, LinkedReference: GuidParameter, LinkedReferenceClass: GuidParameter, LinkGuidToLinkedReference: GuidParameter, UseLinkedInheritClasses: BooleanParameter, UseBaseClassSettings: Boolean, FolderIsMacro: Boolean, Macro: String, ForbidSelectionFromOtherFolders: Boolean, ShowFolderDialog: Boolean, CreateUserSubfolder: Boolean, DefaultFolderGuid: Guid, NomParametersMatching: ReferenceObjectCollection`1
**Методы:**
- `ReferenceObject FindDefaultParent(Reference reference)`

### `NomParametersSynchroType`
**Свойства:** Classes: NomParametersSynchroTypes, IsNomParametersSynchroReferenceObject: Boolean

### `NomParametersSynchroTypes`
**Свойства:** NomParametersSynchroReferenceObject: NomParametersSynchroType

### `NotContainsMailCategoryOperator`
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `NotEqualMailCategoryOperator`
**Свойства:** Type: ComparisonOperatorType
**Методы:**
- `Boolean Compare(Object firstOperand, Object secondOperand)`

### `NumberElementsReference`
**Свойства:** Classes: NumberElementsTypes

### `NumberElementsReferenceObject`
**Свойства:** Class: NumberElementsType, Name: StringParameter
**Методы:**
- `String GetTextValue(ReferenceObject referenceObject)`
- `String GetTestValue(String parameter)`
- `String GetRegexTemplate(ReferenceObject referenceObject)`

### `NumberElementsType`
**Свойства:** Classes: NumberElementsTypes, IsNumberElements: Boolean, IsYear: Boolean, IsMonth: Boolean, IsSomeText: Boolean, IsCounter: Boolean, IsParameterText: Boolean, IsCurrentDate: Boolean, IsFormula: Boolean

### `NumberElementsTypes`
**Свойства:** NumberElements: NumberElementsType, Year: NumberElementsType, Month: NumberElementsType, SomeText: NumberElementsType, Counter: NumberElementsType, ParameterText: NumberElementsType, CurrentDate: NumberElementsType, Formula: NumberElementsType

### `NumberRange`
**Свойства:** StartNumber: Int32, EndNumber: Int32
**Методы:**
- `String GetRangeMask(ServerConnection connection)`
- `Boolean Validate(Int32 startNumber, Int32 endNumber, ServerConnection connection)`
- `String GetValidationMessage(String numberRangeString)`

### `NumericRevisionLevelObject`
**Свойства:** RegexTemplate: String
**Методы:**
- `String GetNextValue(String previousValue)`
- `Int32 Compare(String x, String y)`

### `ObjectAccessor`
**Свойства:** Item: DynamicType, Parameter: ParameterAccessor [RU: Параметр], Id: Int32 [RU: Идентификатор], Guid: Guid [RU: ГлобальныйИдентификатор], Author: UserRefObj, Owner: RefObj, ParentObject: RefObj, NewParentObject: RefObj, ParentObjects: RefObjList, ChildObjects: RefObjList, AllChildObjects: RefObjList, AllParentObjects: RefObjList, MasterObject: RefObj, RootObject: RefObj, LinkedObject: LinkedObjectAccessor`1, LinkedObjects: LinkedObjectsAccessor`2, LinkedHierarchyLink: LinkedHiearchyLinkAccessor`1, LinkedHierarchyLinks: LinkedHierarchyLinksAccessor`2, ChildHierarchyLinks: HierarchyLinkList, AllChildHierarchyLinks: HierarchyLinkList, ParentHierarchyLinks: HierarchyLinkList, Reference: ReferenceAccessor [RU: Справочник], Class: ClassRefObj, Changing: Boolean [RU: Редактируется], IsAdded: Boolean [RU: Редактируется], IsDeleted: Boolean [RU: Редактируется], Signatures: SignatureObjList, IsCheckedOut: Boolean [RU: Редактируется], IsCheckedOutByCurrentUser: Boolean [RU: Редактируется], Access: AccessAccessor [RU: Доступ], PropertyHyperlink: String [RU: СсылкаНаСвойства], Hyperlink: String [RU: СсылкаНаСвойства], Автор: Пользователь [RU only], ПользовательВладелец: Объект [RU only], РодительскийОбъект: Объект [RU only], НовыйРодительскийОбъект: Объект [RU only], РодительскиеОбъекты: Объекты [RU only], ДочерниеОбъекты: Объекты [RU only], ВсеДочерниеОбъекты: Объекты [RU only], ВсеРодительскиеОбъекты: Объекты [RU only], Владелец: Объект [RU only], КорневойОбъект: Объект [RU only], СвязанныйОбъект: LinkedObjectAccessor`1 [RU only], СвязанныеОбъекты: LinkedObjectsAccessor`2 [RU only], СвязанноеПодключение: LinkedHiearchyLinkAccessor`1 [RU only], СвязанныеПодключения: LinkedHierarchyLinksAccessor`2 [RU only], ДочерниеПодключения: Подключения [RU only], ВсеДочерниеПодключения: Подключения [RU only], РодительскиеПодключения: Подключения [RU only], Тип: ТипОбъекта [RU only], Подписи: Подписи [RU only]
**Методы:**
- `Void SetAccess(RefObj user, String accessName, AccessDirectionObj accessDirection) (+1)` [RU: ПрименитьИзменения]
- `Void DeleteAccess(RefObj user, String accessName) (+1)` [RU: Подключить]
- `Void DeleteAllAccesses()` [RU: Изменить]
- `Void OnCreated()` [RU: Изменить]
- `T CastTo(Func`2 objectValidate, Func`3 objectCreator)` [RU: Подключить]
- `T To()` [RU: Изменить]
- `HierarchyLink GetChildLink(RefObj childObj)` [RU: ВернутьРодительскоеПодключение]
- `HierarchyLink GetParentLink(RefObj parentObj)` [RU: ВернутьРодительскоеПодключение]
- `Void AddLink(String linkName, ObjectAccessor refObj)` [RU: Подключить]
- `Void RemoveLink(String linkName, ObjectAccessor refObj) (+1)` [RU: Подключить]
- `Void BeginChanges()` [RU: Изменить]
- `Void BeginChangesKeepingSignatures()` [RU: Изменить]
- `Void BeginChangesClass(String className)` [RU: ВернутьРодительскоеПодключение]
- `Void CheckIn(String comment, Boolean showDialog, Boolean keepCheckedOut)` [RU: ПрименитьИзменения]
- `Void SetOwnerUser(RefObj user)` [RU: ВернутьРодительскоеПодключение]
- `Void Save()` [RU: Изменить]
- `Void CancelChanges(Boolean undoCheckOut)` [RU: ВернутьРодительскоеПодключение]
- `RefObj CreateListObject(String objectListName, String className) (+1)` [RU: Подключить]
- `Boolean Delete()` [RU: Изменить]
- `RefObj Copy(String className, RefObj parentObject, String[] skipParameters) (+1)` [RU: Изменить]
- `RefObj FullCopy(String[] copyLinks)` [RU: ВернутьРодительскоеПодключение]
- `Boolean AddSignature(String signatureType, RefObj user)` [RU: Подключить]
- `Boolean SetSignature(String signatureType, RefObj user, String resolution) (+1)` [RU: Подключить]
- `Boolean ChangeStage(String stageName, String comment, Boolean ignoreSchemeStage) (+1)` [RU: Подключить]
- `Void RaiseEvent(String eventName)` [RU: ВернутьРодительскоеПодключение]
- `Подключение ВернутьДочернееПодключение(Объект дочернийОбъект)` [RU alternative]
- `Void Отключить(String имяСвязи, ObjectAccessor объект)` [RU alternative]
- `Void ИзменитьСохранивПодписи()` [RU alternative]
- `Void ИзменитьТип(String тип)` [RU alternative]
- `Void ЗадатьПользователяВладельца(Объект пользователь)` [RU alternative]
- `Void Сохранить()` [RU alternative]
- `Void ОтменитьИзменения(Boolean отменитьИзмененияНаРабочемСтоле)` [RU alternative]
- `Объект СоздатьОбъектСписка(String имяСпискаОбъектов, String тип)` [RU alternative]
- `Boolean Удалить()` [RU alternative]
- `Объект Копия(String тип, Объект родительскийОбъект, String[] пропущенныеПараметры)` [RU alternative]
- `Объект ПолнаяКопия(String[] копируемыеСвязи)` [RU alternative]
- `Boolean ДобавитьПодпись(String типПодписи, Объект пользователь)` [RU alternative]
- `Boolean Подписать(String типПодписи, Объект пользователь, String резолюция)` [RU alternative]
- `Boolean ИзменитьСтадию(String стадия, String комментарий, Boolean игнорироватьСхемуПереходов)` [RU alternative]
- `Void ИнициироватьСобытие(String событие)` [RU alternative]
- `Void НазначитьДоступ(Объект пользователь, String доступ, НаправлениеДоступа направлениеДоступа)` [RU alternative]
- `Void УдалитьДоступ(Объект пользователь, String доступ)` [RU alternative]
- `Void УдалитьВсеДоступы()` [RU alternative]

### `ObjectAccessorList`1`
**Свойства:** Item: T, Count: Int32
**Методы:**
- `List`1 To()`
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `ObjectAccessType`
**Свойства:** AccessTypeID: AccessTypeID, Type: AccessCommandType, Name: String, IsObject: Boolean, Read: AccessCommand, Delete: AccessCommand, Change: AccessCommand, CreateChildren: AccessCommand, Print: AccessCommand, ChangeAccess: AccessCommand, Copy: AccessCommand, ClearHistory: AccessCommand, ReadHistory: AccessCommand, ChangeStage: AccessCommand, ChangeSignature: AccessCommand, EditSaveSignature: AccessCommand, ChangeClass: AccessCommand, Moving: AccessCommand, CreateDuplicate: AccessCommand, UnlockReferenceObject: AccessCommand, ChangeOwner: AccessCommand, ObjectEditingRemarks: AccessCommand, ObjectVersionDelete: AccessCommand, ObjectChangeOrderIndex: AccessCommand, ObjectCreateHierarchyLink: AccessCommand, ObjectDeleteHierarchyLink: AccessCommand, ObjectChangeInstances: AccessCommand

### `ObjectAttachment`
**Свойства:** Connection: ServerConnection, Reference: ReferenceInfo, Class: ClassObject, Object: ReferenceObject, Name: String, ReferenceName: String, ReferenceId: Int32, ObjectId: Int32, ClassId: Int32, IsObject: Boolean

### `ObjectColumnData`
**Свойства:** IsEmpty: Boolean, Type: ColumnDataType

### `ObjectCreatedCallback`
**Методы:**
- `Void Invoke(Int32 referenceId, Int32 objectId, Int32 clientView)`
- `IAsyncResult BeginInvoke(Int32 referenceId, Int32 objectId, Int32 clientView, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ObjectCreator`
**Методы:**
- `Boolean IsExistObjectForContext(Context context, Boolean findInAllAssemblies) (+1)`
- `Object CreateObject(Type createType, Context context) (+4)`
- `Boolean TryCreateObject(Context context, T& createdObject)`
- `Object CreateObjectByFoundContext(Type createType, Guid reference, ClassObject classObject) (+3)`

### `ObjectFormat`
**Свойства:** MasterGroup: ParameterGroup, Type: ObjectFormatType, Format: String
**Методы:**
- `Void FillSettings(LoadSettings loadSettings, Boolean loadLinks)` [has Async]

### `ObjectFormatBuilder`
**Свойства:** MasterGroup: ParameterGroup, Type: ObjectFormatType, Format: String
**Методы:**
- `ObjectFormat Save()`

### `ObjectInstanceAccessor`
**Свойства:** SourceObject: RefObj, SourceHierarchyLink: HierarchyLink, ИсходныйОбъект: Объект [RU only], ИсходноеПодключение: Подключение [RU only]

### `ObjectInstancePathItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `ObjectIterator`
**Свойства:** Count: Int32, Offset: Int32, LastId: Int32, PartNumber: Int32, State: LoadState

### `ObjectLinkChangedEventArgsBase`
**Свойства:** Link: LinkInfo, AddedObject: ReferenceObject, RemovedObject: ReferenceObject, Type: ObjectChangeType, Sender: Object

### `ObjectParameterChangedEventArgsBase`
**Свойства:** Parameter: Parameter, NewValue: Object, OldValue: Object, Type: ObjectChangeType, Sender: Object

### `ObjectParameterFormat`
**Свойства:** Link: ParameterGroup, Parameter: ParameterInfo, Path: ReferencePath, Format: String

### `ObjectParameterFormatBuilder`
**Свойства:** Link: ParameterGroup, Parameter: ParameterInfo, Format: String

### `ObjectPathElement`
**Свойства:** ReferenceObjectGuid: Guid, HierarchyLinkGuid: Guid, DefaultType: DefaultSupportedType
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean NeedReplaceParentOnAdd(PathElement parent)`
- `Boolean IsEqual(PathElement pathElement)`

### `ObjectPropertyActivityBase`
**Свойства:** Object: InArgument`1, Action: InArgument`1, Link: InArgument`1

### `ObjectPropertyManager`
**Методы:**
- `Boolean GetPropertyValue(String actionString, ObjectAccessor referenceObject, Object& result, String linkName)`
- `Boolean SetPropertyValue(String actionString, IEnumerable`1 objects, Object value)`

### `ObjectRemarksPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `ObjectsComparisonExt`
**Методы:**
- `String GetComparisonKey(ReferenceObject referenceObject) (+2)`

### `ObjectsComparisonSettings`
**Свойства:** ComparisonRules: ComparisonRuleBase
**Методы:**
- `Void Add(ComparisonRuleBase rule)`
- `Void Delete(ComparisonRuleBase rule)`
- `ObjectsComparisonSettings CreateFullCopy()`

### `ObjectSearchAreaSettings`
**Свойства:** Name: String, Paths: ReferencePath[], Filters: Filter[]

### `ObjectSearchSettings`
**Свойства:** SearchAreas: ObjectSearchAreaSettings[]

### `ObjectsForComparisonStorage`
**Свойства:** ReferenceGroup: ParameterGroup, ReferenceGuid: Guid, ObjectsForComparison: IReadOnlyList`1, NeedToCompare: Boolean
**Методы:**
- `Void Add(DesktopObject referenceObject)`
- `Void InsertAt(Int32 index, DesktopObject referenceObject)`
- `Void Remove(DesktopObject referenceObject)`
- `Void RemoveAt(Int32 index)`
- `Void Swap(Int32 firstIndex, Int32 secondIndex)`
- `Void SetSettings(ObjectsComparisonSettings settings)`
- `ObjectsComparisonSettings GetSettings()`
- `IList`1 GetDiff()` [has Async]
- `Void UpdatePositions(ReferenceObject[] referenceObjects, Int32[] positions)`

### `ObjectsListsGroup`
**Свойства:** ClassObject: ClassObject, IsFolder: Boolean, HasChildren: Boolean

### `ObjectStage`
**Свойства:** Stage: Stage, StartDate: DateTime, EndDate: Nullable`1, User: User, IsActual: Boolean, Comment: String, Item: Object

### `ObjectStageChangedEventArgsBase`
**Свойства:** NewStage: Stage, OldStage: Stage, Type: ObjectChangeType, Sender: Object

### `ObjectStageInfo`
**Методы:**
- `ObjectStage GetActualObjectStage()`
- `IReadOnlyList`1 GetStagesHistory(Boolean reload)`

### `ObjectStageParameterExtension`
**Методы:**
- `String GetName(ObjectStageParameter parameter)`

### `ObjectStageParameterPathItem`
**Свойства:** Icon: IconImage, Name: String, Parameter: ObjectStageParameter, SupportSearchType: SupportSearchTypes, Type: PathItemType

### `ObjectStagesPathItem`
**Свойства:** Icon: IconImage, Name: String, Group: ParameterGroup, SupportSearchType: SupportSearchTypes, Type: PathItemType
**Методы:**
- `Boolean IsOneToMany()`

### `ObjectStructureDataLoader`
**Методы:**
- `List`1 LoadReference(Reference reference, StructureGroup parentGroup, Boolean loadDeleted, MacroContext filterContext, Filter filter)`
- `Boolean StructureGroupHasChildren(StructureGroup structureGroup, ReferenceObject parentObject, Boolean loadDeleted)`
- `Boolean ReferenceObjectHasChildren(ReferenceObject referenceObject, StructureGroup parentGroup, Boolean loadDeleted)`
- `List`1 LoadStructureGroup(StructureGroup structureGroup, ReferenceObject parentObject, Boolean loadDeleted)`

### `ObjectValue`
**Свойства:** Value: Object, IsCollection: Boolean, IsObject: Boolean, IsHierarchyLink: Boolean, IsParameter: Boolean
**Методы:**
- `T GetValue()`
- `Boolean ToBoolean(IFormatProvider provider)`
- `Byte ToByte(IFormatProvider provider)`
- `Char ToChar(IFormatProvider provider)`
- `DateTime ToDateTime(IFormatProvider provider)`
- `Decimal ToDecimal(IFormatProvider provider)`
- `Double ToDouble(IFormatProvider provider)`
- `Int16 ToInt16(IFormatProvider provider)`
- `Int32 ToInt32(IFormatProvider provider)`
- `Int64 ToInt64(IFormatProvider provider)`
- `SByte ToSByte(IFormatProvider provider)`
- `Single ToSingle(IFormatProvider provider)`
- `Object ToType(Type conversionType, IFormatProvider provider)`
- `UInt16 ToUInt16(IFormatProvider provider)`
- `UInt32 ToUInt32(IFormatProvider provider)`
- `UInt64 ToUInt64(IFormatProvider provider)`

### `ObjectValue`1`
**Свойства:** Value: T

### `ObjectVisualProperties`
**Свойства:** AmbientColor: Int32, DiffuseColor: Int32, SpecularColor: Int32, EmissiveColor: Int32, Shininess: Double, Reflection: Double, Transparency: Double, Name: String

### `ObjectWithGuidCreatedallback`
**Методы:**
- `Void Invoke(Guid referenceGuid, Guid objectGuid, Int32 clientView)`
- `IAsyncResult BeginInvoke(Guid referenceGuid, Guid objectGuid, Int32 clientView, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `OnBehalfOfPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `OnBehalfTaskField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `OneToManyLink`
**Свойства:** IsModified: Boolean, IsLinkOneToMany: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean
**Методы:**
- `List`1 GetLinkedObjectsId()` [has Async]
- `IEnumerable`1 GetLinkedObjects()` [has Async]
- `List`1 GetObjectsFromReference(Reference reference, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData)` [has Async]
- `ReferenceObject AddLinkedObject(ReferenceObject linkedObject)` [has Async]
- `ReferenceObject AddLinkedObjectWithNoCopy(ReferenceObject linkedObject)` [has Async]
- `List`1 AddLinkedObjectsWithNoCopy(ICollection`1 linkedObjects) (+1)` [has Async]
- `Boolean RemoveLinkedObject(ReferenceObject linkedObject)` [has Async]
- `Boolean RemoveLinkedObjectWithNoCopy(ReferenceObject linkedObject)` [has Async]
- `Void RemoveAll()` [has Async]
- `Void RemoveAllWithNoCopy(Reference reference)` [has Async]
- `ReferenceObject GetSwappedLinkedObject()`
- `List`1 GetSwappedLinkedObjects()`
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `Byte[] GetContext(ReferenceObject linkedObject)` [has Async]
- `Boolean SetContext(ReferenceObject linkedObject, Byte[] context)` [has Async]

### `OneToManyLinkToComplexHierarchy`
**Свойства:** IsModified: Boolean, IsLinkOneToMany: Boolean, LinkReference: Reference, Objects: ReferenceObjectCollection, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, IsLinkedReferenceInitialized: Boolean, IsEmptyLinkedObjects: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32
**Методы:**
- `IReadOnlyCollection`1 GetLinkedComplexLinks()` [has Async]
- `ComplexHierarchyLink AddLinkedComplexLink(ComplexHierarchyLink linkedComplexLink)` [has Async]
- `Boolean RemoveLinkedComplexLink(ComplexHierarchyLink linkedComplexLink)` [has Async]
- `Void RemoveAll()` [has Async]
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `Byte[] GetContext(ReferenceObject linkedObject)`
- `IEnumerator`1 GetEnumerator()`

### `OneToManyLinkToComplexHierarchyManager`
**Свойства:** LinkGroups: ParameterGroupCollection
**Методы:**
- `Boolean IsRelationModified(Guid linkGroupGuid)`

### `OneToManyMultiSelectorControlData`
**Свойства:** ParameterPath: String, PopupViewId: Guid, ShowContextMenu: Boolean, ShowSelectObjectButton: Boolean

### `OneToManyRelation`
**Свойства:** LinkReference: Reference, Objects: ReferenceObjectCollection, IsLinkedReferenceInitialized: Boolean, IsEmptyLinkedObjects: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32
**Методы:**
- `IEnumerable`1 GetLinkedObjects()` [has Async]
- `IEnumerator`1 GetEnumerator()`

### `OneToManyRelationManager`
**Свойства:** Swapped: Boolean, LinkGroups: ParameterGroupCollection
**Методы:**
- `Boolean IsRelationModified(Guid linkGroupGuid)`

### `OneToManyTable`
**Свойства:** IsModified: Boolean, IsTableOneToMany: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, CountLoaded: Int32
**Методы:**
- `IEnumerable`1 GetLinkedObjects()` [has Async]
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `Void DeleteAll()` [has Async]

### `OneToOneLink`
**Свойства:** LinkReference: Reference, LinkedObject: ReferenceObject, IsAdded: Boolean, IsModified: Boolean, IsDeleted: Boolean, IsChanged: Boolean, IsLoaded: Boolean, IsOneToOne: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, IsEmptyLinkedObjects: Boolean, IsLinkedReferenceInitialized: Boolean, State: LoadState, CountLoaded: Int32
**Методы:**
- `Nullable`1 GetLinkedObjectId()` [has Async]
- `TReferenceObject GetLinkedObject()` [has Async]
- `Void Load()` [has Async]
- `ReferenceObject GetObjectFromReference(Reference reference, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData)` [has Async]
- `Void Reload()` [has Async]
- `ReferenceObject SetLinkedObject(ReferenceObject linkedObject)` [has Async]
- `ReferenceObject SetLinkedObjectWithShallowCopy(ReferenceObject linkedObject)`
- `ReferenceObject SetLinkedObjectWithNoCopy(ReferenceObject linkedObject, Reference reference)` [has Async]
- `List`1 GetSwappedLinkedObjects()`
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`

### `OneToOneLinkManager`
**Свойства:** Swapped: Boolean, LinkGroups: ParameterGroupCollection
**Методы:**
- `List`1 ToReferenceObjectList()`

### `OneToOneLinkToComplexHierarchy`
**Свойства:** LinkReference: Reference, LinkedComplexLink: ComplexHierarchyLink, IsAdded: Boolean, IsDeleted: Boolean, IsChanged: Boolean, IsOneToOne: Boolean, IsTableOneToMany: Boolean, IsLinkOneToMany: Boolean, IsAnyReference: Boolean, IsLinkedReferenceInitialized: Boolean, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean, IsEmptyLinkedObjects: Boolean, IsModified: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32
**Методы:**
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`
- `ComplexHierarchyLink SetLinkedComplexLink(ComplexHierarchyLink linkedComplexLink)`
- `Void Reload()`

### `OneToOneLinkToComplexHierarchyManager`
**Свойства:** LinkGroups: ParameterGroupCollection
**Методы:**
- `List`1 ToComplexHierarchyLinkList()`

### `OpenDocumentContext`
**Свойства:** Reference: Int32, ReferenceObject: Guid, HierarchyLink: Guid, AdditionalReferenceObjects: List`1, StructureConfiguration: String, MainFileTypeInStructure: String, IsLaunchedPdm: Boolean, IsSpecialConfigurationSettings: Boolean, IsVirtualAssembly: Boolean, ReferenceObjectInstance: Guid, WorkSessionParameters: WorkSessionParameters

### `OpenDocumentManager`
**Методы:**
- `Void Write(String fileKey, OpenDocumentContext context) (+1)`
- `OpenDocumentContext Read(String fileKey) (+1)`
- `Void Clear()`

### `OpenFileDialog`
**Свойства:** AddExtension: Boolean, Caption: String, DefaultExt: String, FileName: String, FileNames: String[], Filter: String, FilterIndex: Int32, InitialDirectory: String, MultipleSelect: Boolean, SupportMultiDottedExtensions: Boolean
**Методы:**
- `Boolean Show()`
- `Stream OpenFile()`

### `OpenFolderDialog`
**Свойства:** Caption: String, DirectoryName: String, InitialDirectory: String
**Методы:**
- `Boolean Show()`

### `OpenIdProvider`
**Свойства:** Id: Guid, Name: String, Authority: String, ClientId: String, Scope: String, RedirectPath: String

### `OptionRecordsCreator`
**Методы:**
- `Task`1 CreateOptionRecords(IntervalReferenceObject applicabilityObject, OptionsFilter optionsFilter, CancellationToken cancellationToken)`

### `OptionRecordsReference`
**Свойства:** Classes: OptionRecordsTypes

### `OptionRecordsReferenceObject`
**Свойства:** Class: OptionRecordsType, LinkedObjectID: Int32Parameter, ReferenceID: Int32Parameter, ApplicabilityGroup: ApplicabilityGroupType, OptionCodes: StringParameter, OptionValueCodes: StringParameter

### `OptionRecordsType`
**Свойства:** Classes: OptionRecordsTypes, IsOptionRecordsType: Boolean

### `OptionRecordsTypes`
**Свойства:** OptionRecordsType: OptionRecordsType

### `OptionsCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`
- `String Serialize(List`1 optionValues)`

### `OptionsFilter`
**Методы:**
- `String Serialize()`
- `OptionsFilter Deserialize(String xml, ServerConnection connection)`
- `OptionsFilter GetOptionFilter(String filterString, ServerConnection connection)`

### `OptionsTableReference`
**Свойства:** Classes: OptionsTableTypes

### `OptionsTableReferenceObject`
**Свойства:** Class: OptionsTableType, Name: String, Kind: OptionTableKind, OptionsTableSet: OptionsTableSetReferenceObject, IncompleteConfigurations: IList`1, OptionsInRows: IList`1, OptionsInColumns: IList`1
**Методы:**
- `IncompleteConfigurationReferenceObject AddIncompleteConfiguration(IncompleteConfigurationReferenceObject configuration)`
- `ReferenceObject AddOptionToColumns(ProjectOptionsReferenceObject option)`
- `ReferenceObject AddOptionToRows(ProjectOptionsReferenceObject option)`
- `IncompleteConfigurationReferenceObject[] GetIncompleteConfigurationsInColumns()`
- `IncompleteConfigurationReferenceObject[] GetIncompleteConfigurationsInRows()`
- `Boolean RemoveIncompleteConfiguration(IncompleteConfigurationReferenceObject configuration)`
- `Boolean RemoveOptionFromColumns(ProjectOptionsReferenceObject option)`
- `Boolean RemoveOptionFromRows(ProjectOptionsReferenceObject option)`
- `ProjectOptionsReferenceObject[] GetOrderedOptions(IList`1 options, String[] optionsOrder)`

### `OptionsTableSetReference`
**Свойства:** Classes: OptionsTableSetTypes

### `OptionsTableSetReferenceObject`
**Свойства:** ConfigurationManagerObject: ReferenceObject, Class: OptionsTableSetType, Name: String, Comment: String, OptionsTables: IList`1, Constraints: IList`1, ProjectOptions: IList`1, ProjectOptionValues: IList`1
**Методы:**
- `OptionsTableReferenceObject AddTable(OptionsTableReferenceObject table)`
- `OptionsTableSetReferenceObject CopyTableSet()`
- `OptionsTableReferenceObject[] GetMajorTables()`
- `OptionsTableReferenceObject[] GetMinorTables()`
- `Boolean RemoveTable(OptionsTableReferenceObject table)`

### `OptionsTableSetType`
**Свойства:** Classes: OptionsTableSetTypes, IsOptionsTableSet: Boolean

### `OptionsTableSetTypes`
**Свойства:** OptionsTableSet: OptionsTableSetType

### `OptionsTableType`
**Свойства:** Classes: OptionsTableTypes, IsOptionsTable: Boolean, IsDiversityTable: Boolean

### `OptionsTableTypes`
**Свойства:** OptionsTable: OptionsTableType, DiversityTable: OptionsTableType

### `OptionTerm`
**Свойства:** Connection: ServerConnection, Filter: OptionsFilter, Option: ProductOptionsReferenceObject, ParameterName: String

### `OrderingSearchRule`
**Свойства:** Descending: Boolean

### `OrderParameter`
**Свойства:** Value: String, IsNull: Boolean
**Методы:**
- `Int32 GetTaskPostition(BaseTaskObject task)`
- `Void AddTask(BaseTaskObject task)`
- `Void MoveTask(BaseTaskObject movedTask, BaseTaskObject targetTask, Int32 shift)`
- `Void InsertTasks(BaseTaskObject targetTask, List`1 tasks, Boolean before)`
- `Void InsertBefore(BaseTaskObject targetTask, List`1 tasks)`
- `Void InsertAfter(BaseTaskObject targetTask, List`1 tasks)`
- `Void RemoveTask(BaseTaskObject task)`
- `Void RemoveAllTasks()`
- `TypeCode GetTypeCode()`
- `Void Refresh()`

### `OrElseOperator`
**Свойства:** LogicalType: LogicalActivityOperatorType
**Методы:**
- `Nullable`1 CompareFirst(Boolean firstOperand)`
- `Boolean CompareSecond(Boolean secondOperand)`

### `OutputDocument`
**Свойства:** Class: ReportType, Name: StringParameter, ContentType: ReportContentType, OpenFile: Boolean, OverwriteReportFile: Boolean, ContentReference: StringParameter, ContentReferenceGuid: Guid, ObjectList: StringParameter, ContentReferencePath: ReferencePath, MenuName: StringParameter, FilterXml: StringParameter, OpenType: OpenReportType, HasTemplateProperties: Boolean, AllowCustomizeDesign: Boolean, CanExecute: Boolean, ContentReferenceObjectClassGuids: Guid[], ContentReferenceReportClassGuids: Guid[], TemplateFile: FileObject, Generator: ReportGenerator
**Методы:**
- `Void EditTemplateProperties(IWin32Window owner)`
- `Void CustomizeDesign(IWin32Window owner) (+1)`
- `Void CustomizeDesign_Core(IntPtr owner)`
- `Filter GetFilter()`
- `ReferenceFilterObject GetFilterObject()`
- `Void SetFilter(Filter filter)`
- `Void SetFilterObject(ReferenceFilterObject filterObject)`
- `Boolean CanGenerateForClass(ClassObject classObject, Boolean throwOnError)`
- `ReportGenerationContext Generate(ReferenceObject obj, ComplexHierarchyLink link) (+4)`
- `Boolean ValidateLicense(Boolean throwOnError)`
- `Void InitializeContext(ReportGenerationContext context, Boolean generating)`

### `OwnerMailField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `OwnerPathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `PackageHelper`
**Методы:**
- `Package Create(Stream stream) (+1)`
- `Package Open(Stream stream) (+1)`
- `Uri CreateRelativeUri(String filePath)`
- `Stream AddXmlContent(Package package, String fileName)`
- `Stream AddFile(Package package, String fileName)`
- `Stream GetFile(Package package, String fileName)`

### `Padding`
**Свойства:** Empty: Padding, All: Int32, Left: Int32, Right: Int32, Top: Int32, Bottom: Int32
**Методы:**
- `Boolean TryParse(String value, Padding& padding, String separator)`

### `PageInfo`
**Свойства:** Name: String, Visible: Boolean, Type: Int32, Index: Int32, Properties: PageProperties

### `PageProperties`
**Свойства:** Paper: PaperInfo

### `PaneSettings`
**Свойства:** Name: String, Id: Guid, IsDefault: Boolean, Height: Double, MirrorHeight: Double, BackgroundImagePath: String, IsAxisXVisible: Boolean, AxisXTitleCaption: String, AxisXTitleAlignment: TitleAlignmentType, AxisXFormatString: String, IsAxisXLogarithmic: Boolean, AxisXLogarithmicBase: Double, AxisXDateTimeGridAlignment: DateTimeMeasurementUnitType, AxisXDateTimeMeasureUnit: DateTimeMeasurementUnitType, IsAxisYVisible: Boolean, AxisYTitleCaption: String, AxisYTitleAlignment: TitleAlignmentType, AxisYFormatString: String, AxisYDateTimeGridAlignment: DateTimeMeasurementUnitType, AxisYDateTimeMeasureUnit: DateTimeMeasurementUnitType, IsAxisYLogarithmic: Boolean, AxisYLogarithmicBase: Double, AxisXGridLinesVisible: Boolean, AxisXGridLinesMinorVisible: Boolean, AxisXInterlaced: Boolean, AxisXMinScrollValue: String, AxisXMaxScrollValue: String, AxisYGridLinesVisible: Boolean, AxisYGridLinesMinorVisible: Boolean, AxisYInterlaced: Boolean, AxisYMinScrollValue: String, AxisYMaxScrollValue: String

### `PaperInfo`
**Свойства:** Format: String, Orientation: PaperOrientation

### `Parameter`
**Свойства:** Value: Object, EmptyValue: Object, IsEmpty: Boolean, IsNull: Boolean, IsModified: Boolean, IsReadOnly: Boolean, ParameterInfo: ParameterInfo, Owner: ParameterCollection, HasNullValueFromValueList: Boolean, HasValueOutsideUneditableValueList: Boolean
**Методы:**
- `Void SetNull()`
- `Void SetModified()`
- `Boolean GetBoolean()`
- `Byte GetByte()`
- `Int16 GetInt16()`
- `Int32 GetInt32()`
- `Int64 GetInt64()`
- `String GetString()`
- `Single GetSingle()`
- `Double GetDouble()`
- `Decimal GetDecimal()`
- `Guid GetGuid()`
- `Byte[] GetByteArray()`
- `DateTime GetDateTime()`
- `IconImage GetIcon()`
- `Image GetImage()`
- `Object GetValue(Type type) (+1)`
- `Boolean ToBoolean(IFormatProvider provider)`
- `Byte ToByte(IFormatProvider provider)`
- `Char ToChar(IFormatProvider provider)`
- `DateTime ToDateTime(IFormatProvider provider)`
- `Decimal ToDecimal(IFormatProvider provider)`
- `Double ToDouble(IFormatProvider provider)`
- `Int16 ToInt16(IFormatProvider provider)`
- `Int32 ToInt32(IFormatProvider provider)`
- `Int64 ToInt64(IFormatProvider provider)`
- `SByte ToSByte(IFormatProvider provider)`
- `Single ToSingle(IFormatProvider provider)`
- `Object ToType(Type conversionType, IFormatProvider provider)`
- `UInt16 ToUInt16(IFormatProvider provider)`
- `UInt32 ToUInt32(IFormatProvider provider)`
- `UInt64 ToUInt64(IFormatProvider provider)`
- `TypeCode GetTypeCode()`

### `Parameter`1`
**Свойства:** Value: T, EmptyValue: T, IsEmpty: Boolean, IsNull: Boolean

### `ParameterAccessor`
**Свойства:** Item: DynamicType
**Методы:**
- `String Value(String parameterName)` [RU: Значение]

### `ParameterActivityStatusExtensions`
**Методы:**
- `String GetActivityStatusName(ParameterActivityStatus status)`

### `ParameterColumnData`
**Свойства:** IsManualSetter: Boolean, CanSetGetter: String, ValueSetter: String, LinkAggregator: String, Parameter: String, DisplayMask: String, Type: ColumnDataType, IsEmpty: Boolean, ValueSetterPath: Object, CanSetGetterPath: Object, LinkAggregationPath: Object, ParameterPath: Object, SystemParameter: SystemParameterType
**Методы:**
- `T GetParameterPath(ParameterGroup group)`

### `ParameterContainer`
**Свойства:** ParameterValues: ParameterCollection, Item: Parameter, Item: Parameter, Item: Parameter
**Методы:**
- `IEnumerator`1 GetEnumerator()`

### `ParameterDataSettings`
**Свойства:** Type: SeriesParameter, CalculationType: CalculationValueType, UniversalPathString: String, DataType: ParameterDataType, ParameterGuid: Guid, CalculateString: String
**Методы:**
- `Void CopyPropertiesTo(ParameterDataSettings parameter)`

### `ParameterEditTypeExtension`
**Методы:**
- `InplaceEditType ToInplaceEditType(ParameterEditType parameterEditType) (+1)`
- `String GetText(InplaceEditType inplaceEditType)`
- `Boolean IsEditingInDialogAllowed(ParameterEditType parameterEditType)`
- `Boolean IsEditingInGridForbidden(ParameterEditType parameterEditType)`

### `ParameterEditTypeExtensions`
**Методы:**
- `String GetEditTypeName(ParameterEditType type)`

### `ParameterGroup`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, IsClassesLoaded: Boolean, SystemObjectType: SystemObjectType, ReferenceInfo: ReferenceInfo, ReferenceGroup: ParameterGroup, HierarchyGroup: ParameterGroup, Classes: ClassTree, ActivityStatus: GroupActivityStatus, Type: ParameterGroupType, HierarchyType: ReferenceHierarchyType, MasterGroup: ParameterGroup, SlaveGroupId: Int32, SlaveGroup: ParameterGroup, Name: String, CheckAccess: AccessRightsMode, SupportsEncryption: Boolean, SupportsExtendedParameters: Boolean, SupportsMandatoryAccess: Boolean, ExtendedParameteresStorage: ExtendedParametersStorage, Comment: String, Visibility: ReferenceVisibility, Icon: IconImage, TypeIcon: IconImage, TableName: String, TableNameGenerated: Boolean, SupportsDesktop: Boolean, SupportsRecycleBin: Boolean, SupportsDataChangeLog: Boolean, SupportsRevisions: Boolean, SupportsClasses: Boolean, SupportsSystemObjects: Boolean, SupportsPrototypes: Boolean, SupportsOrder: Boolean, SupportsOwner: Boolean, SupportsSignature: Boolean, UseAllSignatureTypes: Boolean, SupportsObjectsInstances: Boolean, SupportsStructureTypes: Boolean, IsObjectsInstancesImpl: Boolean, SignatureTypes: List`1, SupportsPrivateFolders: Boolean, SupportsNomenclature: Boolean, SupportsConfigurationSettings: Boolean, SupportsDesignContexts: Boolean, SupportsActivityDates: Boolean, SupportsApplicability: Boolean, SupportsSubstitutesInContext: Boolean, Swapped: Boolean, LinkToSameReference: Boolean, LinkType: LinkType, LinkVisibility: LinkVisibility, LinkRequired: LinkRequired, DoubleDirectionLink: Boolean, IsAsymmetricLink: Boolean, DefaultVisibleParameter: ParameterInfo, UserControl: String, SelectionPath: String, CanEdit: Boolean, CanEditExtendedParameters: Boolean, CanDelete: Boolean, Parameters: ParameterInfoCollection, SearchQueryLinkFilter: Filter, SearchQueryLinkPathToFilter: ReferencePath, SystemParameters: ParameterInfoCollection, Indexes: ReadOnlyCollection`1, UniqueIndex: UniqueIndex, EventHandlers: EventHandlerCollection, Dialog: Dialog, Dialogs: DialogManager, WebDialog: Dialog, WebDialogs: WebDialogManager, RevisionNamingRule: RevisionNamingRuleObject, ConfiguratorGuid: Guid, Configurator: Configurator, InstancesGroupInfo: InstancesGroupInfo, HasHierarchy: Boolean, IsReference: Boolean, IsLinkGroup: Boolean, IsCorruptedLink: Boolean, IsTableOneToOne: Boolean, IsLinkToOne: Boolean, IsToManyRelation: Boolean, IsLinkToMany: Boolean, IsAnyReferenceLink: Boolean, IsSearchQueryLink: Boolean, IsTableOneToMany: Boolean, IsHierarchyTable: Boolean, IsCommonTableOneToOne: Boolean, Item: ParameterInfo, Item: ParameterInfo, Item: ParameterInfo, Item: ParameterInfo, ClassParameterInfo: ParameterInfo, AuthorParameterInfo: ParameterInfo, EditorParameterInfo: ParameterInfo, CreationDateParameterInfo: ParameterInfo, EditDateParameterInfo: ParameterInfo, ParentParameterInfo: ParameterInfo, SupportsStages: Boolean, Scheme: Scheme, DefaultStage: SchemeStage, CanChangeClass: Boolean, SupportMultiAttachment: Boolean, XmlId: String, AuthorAccess: AccessGroup, ObjectFormat: ObjectFormat
**Методы:**
- `Boolean ReloadOneToOneParameters()`
- `Boolean TryParseXmlId(String xmlId, Int32& id, Boolean& deleted)`
- `T GetGroupSettings(Guid settingsId, Int32 classId)` [has Async]
- `Boolean SetGroupSettings(Guid settingsId, Int32 classId, T settings)` [has Async]
- `Boolean ClearGroupSettings(Guid settingsId, Int32 classId)` [has Async]
- `ClassObjectCollection GetAllowedClassesToLink()`
- `SigningParametersInfo GetSigningParametersInfo()` [has Async]
- `Void SetSigningParameters(List`1 signingParameters)` [has Async]
- `Boolean Contains(ParameterGroup group)`
- `Boolean HasSlaveGroup()`
- `String GetSecondCaption()`
- `ParameterGroup GetSwappedLink()`
- `List`1 GetEventHandlers(ParameterGroupEvent event)` [has Async]

### `ParameterGroupBuilder`
**Свойства:** DefaultVisibleParameter: ParameterInfo, ObjectFormat: ObjectFormat, SupportsOrder: Boolean, SupportsSignature: Boolean, UseAllSignatureTypes: Boolean, SignatureTypes: List`1, CanChangeClass: Boolean
**Методы:**
- `Void Save(Boolean createNameParameter) (+1)` [has Async]

### `ParameterGroupBuilderBase`
**Свойства:** Connection: ServerConnection, ParameterGroup: ParameterGroup, Type: ParameterGroupType, MasterGroup: ParameterGroup, Name: String, TableName: String, TableNameGenerated: Boolean, Comment: String, Icon: IconImage, CanChangeIcon: Boolean, UserControl: String, IsAdded: Boolean, IsModified: Boolean
**Методы:**
- `Void Save()` [has Async]
- `Void Delete(ParameterGroup group)` [has Async]

### `ParameterGroupEvent`
**Свойства:** Id: Int32, Guid: Guid, Name: String, IsSystem: Boolean
**Методы:**
- `Int32 CompareTo(ParameterGroupEvent other)`

### `ParameterGroupExtensions`
**Методы:**
- `Boolean IsCharacteristicLink(ParameterGroup parameterGroup)`

### `ParameterGroupExtensions`
**Методы:**
- `Icon CloneIcon(ParameterGroup parameterGroup) (+1)`
- `Boolean IsInherit(ParameterGroup group, Guid groupGuid)`

### `ParameterGroupHelper`
**Методы:**
- `ReferenceInfo GetReference(ParameterGroup group)`
- `Boolean TryParse(String path, ServerConnection connection, ParameterGroup& group)`
- `String CombineListObjectPath(String reference, String listObject)`
- `ParameterGroup FindRelation(ServerConnection connection, String referenceName, String relationName) (+2)`
- `String CombineRelativePath(ParameterGroup group)`

### `ParameterGroupInfo`
**Свойства:** Reference: ReferenceInfo, Class: ClassObject, IsReferenceInfo: Boolean, IsClass: Boolean, IsHierarchy: Boolean, Parameters: ParameterInfoCollection
**Методы:**
- `ParameterGroupInfo LoadReferenceInfo(ReferenceInfo referenceInfo)`
- `ParameterGroupInfo LoadClass(ClassObject classObject)`
- `ParameterGroupInfo LoadHierarchy(ReferenceInfo referenceInfo)`
- `ParameterInfo GetParameter(Guid parameterGuid)`

### `ParameterGroupManager`
**Свойства:** Guid: Guid, Id: Int32, OneToOneParameters: ParameterInfoCollection, RequiredParameters: ReadOnlyCollection`1, Events: EventCollection, OneToOneTables: ParameterGroupCollection, OneToOneLinks: ParameterGroupCollection, OneToOneLinksToComplexHierarchy: ParameterGroupCollection, OneToManyTables: ParameterGroupCollection, OneToManyLinks: ParameterGroupCollection, OneToManyLinksToComplexHierarchy: ParameterGroupCollection, AnyReferenceLinks: ParameterGroupCollection, SearchQueryLinks: ParameterGroupCollection
**Методы:**
- `List`1 GetEventHandlers(ParameterGroupEvent event)`
- `SigningParametersInfo GetSigningParametersInfo()` [has Async]
- `Void SetSigningParameters(List`1 signingParameters)` [has Async]
- `ParameterGroupCollection GetRelations()`
- `ParameterGroup FindRelation(Int32 groupId) (+1)`
- `ParameterGroupCollection GetLinks()` [has Async]
- `ParameterGroupCollection GetCorruptedLinks()`
- `List`1 GetRequiredParameters()`
- `ParameterGroupCollection GetOneToOneRelations()` [has Async]
- `ParameterGroupCollection GetOneToManyRelations(Boolean includeAnyReferenceLinks) (+1)` [has Async]
- `ParameterGroupCollection GetAllGroups()`
- `ParameterGroupCollection GetSwappedLinks()`
- `ParameterGroup FindSwappedLink(Int32 groupId) (+1)`
- `ParameterGroupCollection GetSwappedToOneLinks()`
- `ParameterGroupCollection GetSwappedToManyLinks()`
- `ParameterGroup FindOneToManyTable(Int32 id) (+2)`

### `ParameterGroupRule`
**Свойства:** Guid: Guid
**Методы:**
- `IObjectsComparisonNode Run(IObjectNode left, IObjectNode right)`

### `ParameterGroupStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `ParameterGroupType`
**Свойства:** Type: Int32, Name: String, IsLink: Boolean, IsReference: Boolean, IsTable: Boolean, Icon: IconImage
**Методы:**
- `Int32 CompareTo(ParameterGroupType other)`

### `ParameterGroupVisibilityExtensions`
**Методы:**
- `String GetName(ParameterGroupVisibility visibility)`

### `ParameterHelper`
**Методы:**
- `ParameterInfo FindParameter(ClassObject classObject, String parameterName)`

### `ParameterInfo`
**Свойства:** Group: ParameterGroup, Connection: ServerConnection, Type: ParameterType, Name: String, Comment: String, Length: Int32, Format: String, DecimalPlaces: Int32, FieldName: String, IsVisible: Boolean, EditType: ParameterEditType, Nullable: Boolean, IsRequired: Boolean, DefaultValue: Object, IsIndexed: Boolean, IsFullTextSearchEnabled: Boolean, Encrypted: Boolean, CertificateGuid: Guid, Certificate: Certificate, PreviousPropertiesState: ObjectPropertiesState, ValueList: ParameterValueList, RangeInfo: ParameterRangeInfo, UserControl: String, IsPrimaryKey: Boolean, ActivityStatus: ParameterActivityStatus, Unit: Unit, TypeName: String, IsSystem: Boolean, SystemType: SystemParameterType, CanEdit: Boolean, CanBeIndexed: Boolean, CanBeFullTextSearchEnabled: Boolean, CanDelete: Boolean, IsSystemKey: Boolean, IsCheckOutStateField: Boolean, SystemObjectType: SystemObjectType, TypeIcon: IconImage, SupportsSearch: Boolean, Alias: ExtendedParameterReferenceLink, Aliases: ExtendedParameterReferenceLinksList, IsExtended: Boolean, IsVirtual: Boolean, IsGenerated: Boolean, IsSupportedAliases: Boolean, XmlId: String
**Методы:**
- `Void FixParameterState()`
- `Boolean IsLinkedToGroup(Int32 groupId)`
- `Boolean IsLinkedToGroupClass(Int32 groupId, Int32 classId)`
- `List`1 GetComparisonOperators()`
- `List`1 GetIndexes()`
- `Int32 CompareTo(ParameterInfo other)`
- `Object GetFormat(Type formatType)`
- `Boolean SkipUsingServerTermValue(ComparisonOperator comparisonOperator)`
- `Boolean TryParseXmlId(String xmlId, Int32& id, Boolean& deleted)`
- `String SerializeValue(Object value, ObjectSerializationMode mode)`
- `Object ParseValue(String value)`

### `ParameterInfoBuilder`
**Свойства:** ParameterInfo: ParameterInfo, ParameterGroup: ParameterGroup, Connection: ServerConnection, IsAdded: Boolean, IsModified: Boolean, IsExtendedParameterBuilder: Boolean, IsVirtualParameterBuilder: Boolean, Type: ParameterType, Name: String, Comment: String, MaxLength: Int32, ParameterFormat: String, FieldName: String, IsVisible: Boolean, CertificateGuid: Guid, AllowEdit: Boolean, AllowChangeFromGrid: Boolean, InplaceEditType: InplaceEditType, AllowNull: Boolean, AlwaysPresent: Boolean, DefaultValue: Object, IsIndexed: Boolean, IsFullTextSearchEnabled: Boolean, Unit: Unit, ContainsValueList: Boolean, IsNewValueList: Boolean, ParameterValueList: ValueList, ParameterRangeInfo: ParameterRangeInfo, ContainsRangeInfo: Boolean, UserControl: String, PreviousPropertiesState: ObjectPropertiesState
**Методы:**
- `Void CopyFrom(ParameterInfo sourceParameter)`
- `Void Save()` [has Async]
- `Void Delete(ParameterInfo parameter)` [has Async]
- `Void FixParameterState()`

### `ParameterInfoBuildersFactory`
**Методы:**
- `ParameterInfoBuilder CreateParameterInfoBuilder(ParameterInfo parameterInfo)`
- `ParameterInfoBuilder Create(ParameterGroup parameterGroup, ParameterInfo parameterInfo)`

### `ParameterInfoExtensions`
**Методы:**
- `Type GetRealType(ParameterInfo parameterInfo)`
- `Type GetRealServerType(ParameterInfo parameterInfo)`
- `ParameterType GetRealParameterType(ParameterInfo parameterInfo)`

### `ParameterInfoExtensions`
**Методы:**
- `String Serialize(ParameterInfo parameterInfo, ParameterGroupInfo groupInfo)`
- `String DeSerilizeParameterGuid(String text)`
- `String DeSerilizeClassGuid(String text)`
- `ParameterInfo DeSerialize(ServerConnection connection, String text, ParameterGroupInfo& groupInfo) (+1)`

### `ParameterInfoGeneralType`
**Свойства:** AllParameterInfoGeneralTypes: ReadOnlyCollection`1, ExtendedParameterInfoGeneralTypes: ReadOnlyCollection`1, Name: String
**Методы:**
- `ParameterInfoGeneralType GetParameterGeneralType(ParameterType parameterType)`
- `List`1 GetCompatibleTypes(ParameterInfoGeneralType generalType)`

### `ParameterInfoGeneralTypeExtensions`
**Методы:**
- `Int32 GetId(ParameterInfoGeneralType type)`
- `ParameterInfoGeneralType GetGeneralType(Int32 id)`

### `ParameterMatchingControlXMLData`
**Свойства:** MatchingReferenceGuid: String, MatchingParameterGuid: String, ClearLinkAction: Int32, LinkToFillGuid: String, CanUseNotExistValue: Boolean, ShowPopupOnMaching: Boolean, AllowClear: Boolean, AllowSelectFromDialog: Boolean, DisableFilterInDialog: Boolean, DisableFilterWhenLinkFilled: Boolean, Filter: Filter, MaxLoadCount: Int32, UseRelevance: Boolean, ContextFormulaSource: String, UseContainsFilter: Boolean, ViewId: String, ViewName: String, СonformityParameters: List`1 [RU only]
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `ParameterObjectValue`
**Свойства:** Parameter: Parameter, IsParameter: Boolean
**Методы:**
- `Boolean ToBoolean(IFormatProvider provider)`
- `Byte ToByte(IFormatProvider provider)`
- `Char ToChar(IFormatProvider provider)`
- `DateTime ToDateTime(IFormatProvider provider)`
- `Decimal ToDecimal(IFormatProvider provider)`
- `Double ToDouble(IFormatProvider provider)`
- `Int16 ToInt16(IFormatProvider provider)`
- `Int32 ToInt32(IFormatProvider provider)`
- `Int64 ToInt64(IFormatProvider provider)`
- `SByte ToSByte(IFormatProvider provider)`
- `Single ToSingle(IFormatProvider provider)`
- `Object ToType(Type conversionType, IFormatProvider provider)`
- `UInt16 ToUInt16(IFormatProvider provider)`
- `UInt32 ToUInt32(IFormatProvider provider)`
- `UInt64 ToUInt64(IFormatProvider provider)`

### `ParameterPathItem`
**Свойства:** Parameter: ParameterInfo, Name: String, Type: PathItemType, Icon: IconImage
**Методы:**
- `Boolean SkipUsingServerTermValue(ComparisonOperator comparisonOperator)`

### `ParameterRangeInfo`
**Свойства:** Id: Int32, Guid: Guid, Name: String, MinParameterId: Int32, MaxParameterId: Int32, Owner: ParameterInfo
**Методы:**
- `Boolean ValidateRange(ParameterInfo parameterInfo, Object value, ReferenceObject referenceObject, Boolean throwOnError)`

### `ParameterRule`
**Свойства:** Guid: Guid, ParameterInfo: ParameterInfo
**Методы:**
- `IObjectsComparisonNode Run(IObjectNode left, IObjectNode right)`

### `ParametersAssocReference`
**Свойства:** Classes: ParametersAssocTypes

### `ParametersAssocReferenceObject`
**Свойства:** Class: ParametersAssocType, Name: StringParameter, ApplicationParameter: StringParameter, ApplicationParameterType: StringParameter, DOCsParameterDescription: StringParameter, DOCsParameterType: Int32Parameter, LinkDirection: Int32Parameter

### `ParametersAssocType`
**Свойства:** Classes: ParametersAssocTypes, IsParametersAssociation: Boolean

### `ParametersAssocTypes`
**Свойства:** ParametersAssociation: ParametersAssocType

### `ParameterTextElementReferenceObject`
**Свойства:** Parameter: StringParameter, StartPosition: Int32Parameter, SymbolCount: Int32Parameter
**Методы:**
- `String GetTestValue(String parameter)`

### `ParameterType`
**Свойства:** DefaultMantissaLength: Int32, Id: Int32, Name: String, FullName: String, MaxSize: Int32, IsVariantSize: Boolean, IsSigned: Boolean, IsString: Boolean, IsInt: Boolean, IsFloat: Boolean, IsMoney: Boolean, IsNumber: Boolean, IsDateTime: Boolean, IsBoolean: Boolean, IsBlob: Boolean, IsSupported: Boolean, CanBeEncrypted: Boolean, CanBeIndexed: Boolean, CanBeFullTextSearchEnabled: Boolean, CanUseInUniqueIndex: Boolean, SupportsNullable: Boolean, AlwaysNullable: Boolean, SupportsSize: Boolean, SupportsMaxSize: Boolean, AlwaysMaxSize: Boolean, SupportsValueList: Boolean, SupportsRange: Boolean, ParameterFormatter: ICustomFormatter, LanguageType: Type, DefaultValue: Object, MinValue: Object, MaxValue: Object
**Методы:**
- `List`1 GetTypeList(Boolean supportedOnly)`
- `Object Parse(String s, IFormatProvider provider, ComparisonOperator operator) (+1)`
- `Boolean TryParse(String s, IFormatProvider provider, Object& result) (+1)`
- `Object ParseDefaultValue(String s, IFormatProvider provider) (+1)`
- `Boolean TryParseDefaultValue(String s, IFormatProvider provider, Object& result) (+1)`
- `String ConvertToString(Object value)`
- `Boolean SupportsConversionTo(Int32 typeId) (+1)`
- `List`1 GetConversionList()`
- `List`1 GetComparisonOperators()`
- `Type GetObjectParameterType()`

### `ParameterValueList`
**Свойства:** ParameterInfo: ParameterInfo, Type: ParameterType, Nullable: Boolean, IsFixed: Boolean, IsEditable: Boolean, IsExpandable: Boolean, IsEditableList: Boolean, CanAdd: Boolean, CanEditList: Boolean, CanChangeReferenceStructure: Boolean, CanEdit: Boolean, CanDelete: Boolean, Item: ListValue, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `ListValue AddValue(Object value, IconImage icon, String name) (+1)`
- `Void UpdateValue(Int32 index, Object value)`
- `Void UpdateListValue(Int32 index, ListValue value)`
- `Void DeleteValue(Int32 index)`
- `Void SetValues(IEnumerable`1 values)`
- `Object GetValue(String name)`
- `String GetName(Object value)`
- `Int32 IndexOf(ListValue item)`
- `Void Insert(Int32 index, ListValue item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(ListValue item)`
- `Void Clear()`
- `Boolean Contains(ListValue item)`
- `Void CopyTo(ListValue[] array, Int32 arrayIndex)`
- `Boolean Remove(ListValue item)`
- `IEnumerator`1 GetEnumerator()`

### `ParentHierarchyLinksPathItem`
**Свойства:** Type: PathItemType, Name: String
**Методы:**
- `Boolean IsOneToMany()`

### `ParentObjectPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `PasswordParameter`
**Свойства:** IsReadOnly: Boolean, IsEmpty: Boolean
**Методы:**
- `String GetString()`
- `TypeCode GetTypeCode()`

### `PasswordPolicySettings`
**Свойства:** Connection: ServerConnection, Interface: String, ParameterGroupId: Int32, SupportsViews: Boolean, SharingType: SettingsSharingType
**Методы:**
- `Void ValidateNewPassword(String oldPassword, String newPassword)`
- `Void Save()` [has Async]

### `PasswordPolicySettingsData`
**Свойства:** Duration: Nullable`1, MinimumLength: Int32, NecessaryUseDigits: Boolean, NecessaryUseCapitalLetters: Boolean, NecessaryUseSpecialSymbols: Boolean, MinimalCountOfChangedSymbols: Int32

### `PathCalculationSettings`
**Свойства:** Distinct: Boolean, WithStaticReference: Boolean

### `PathColumnInfo`
**Свойства:** SystemColumn: ObjectSearchSystemColumnType, Path: ReferencePath, IsVisibleDefault: Boolean, IsVisibleForce: Nullable`1

### `PathElement`
**Свойства:** Path: String, DisplayName: String, DefaultType: DefaultSupportedType, Type: Type, Parent: PathElement
**Методы:**
- `String GetDisplayNameFromParts(String[] parts)`
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean NeedReplaceParentOnAdd(PathElement parent)`
- `Boolean IsEqual(PathElement pathElement1, PathElement pathElement2) (+1)`

### `PathItem`
**Свойства:** Parent: PathItem, Items: ReadOnlyCollection`1, Operators: ReadOnlyCollection`1, Path: ReferencePath, Name: String, Type: PathItemType, Icon: IconImage, SupportsSearch: Boolean, SupportSearchType: SupportSearchTypes, UseLinkSeparator: Boolean
**Методы:**
- `Void ReloadItems()`
- `String GetUniqueId()`
- `Boolean IsOneToMany()`
- `Boolean SkipUsingServerTermValue(ComparisonOperator comparisonOperator)`
- `Boolean IsSame(PathItem other)`

### `PathItemGroup`
**Свойства:** PathItem: PathItem, HasChildren: Boolean, IsGroupedMethod: Boolean

### `PathPerformer`
**Методы:**
- `PathPerformer Build(PathPerformerSettings settings)`
- `ValueTuple`2 GetValueLanguageType()`
- `ValueTuple`2 GetOneValueLanguageType()`
- `Object GetValue(ReferenceObject referenceObject, ComplexHierarchyLink hierarchyLink)`
- `Object GetOneValue(ReferenceObject referenceObject, ComplexHierarchyLink hierarchyLink)`

### `PathPerformerSettings`
**Свойства:** Type: PathPerformerType, FromHierarchy: Boolean
**Методы:**
- `PathPerformerSettings Create(ReferencePath path)`

### `PercentMailField`
**Методы:**
- `List`1 GetComparisonOperators()`

### `Periodical`
**Свойства:** PeriodValue: Int32, Period: Int32Parameter
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `PhysicalStructureObject`
**Свойства:** Name: StringParameter, Date: DateTimeParameter, ProductStructureId: Int32Parameter
**Методы:**
- `Void SetProduct(NomenclatureObject product)`
- `Void Export()`

### `PhysicalStructureReference`
**Свойства:** Classes: PhysicalStructureTypes

### `PhysicalStructureReferenceObject`
**Свойства:** Class: PhysicalStructureType, PhysicalStructureFiles: ReferenceObjectCollection, PhysicalStructureFolder: ReferenceObject, Product: ReferenceObject
**Методы:**
- `ReferenceObject AddPhysicalStructureFiles(ReferenceObject newLinkedObject)`
- `Boolean RemovePhysicalStructureFiles(ReferenceObject linkedObject)`

### `PhysicalStructureType`
**Свойства:** Classes: PhysicalStructureTypes, IsPhysicalStructure: Boolean, IsStructureElement: Boolean

### `PhysicalStructureTypes`
**Свойства:** PhysicalStructure: PhysicalStructureType, StructureElement: PhysicalStructureType

### `PictureFieldInputDialog`
**Свойства:** TypeName: String, Object: InArgument`1, ImagePath: InArgument`1, LineCount: InArgument`1

### `PlanningCategoryColumnData`
**Свойства:** IsEmpty: Boolean, PlanningCategory: Guid, Type: ColumnDataType

### `PluginInterfacesMap`
**Свойства:** Map: PluginInterfacesMap
**Методы:**
- `Void RegisterPluginType(Type interfaceType, Context context, Type classType) (+1)`

### `Point`
**Свойства:** Id: Guid, AdditionalData: Object, SourceReferenceObject: ReferenceObject, SourcePoints: ReadOnlyCollection`1, Argument: PointParameterValueEx, ArgumentType: ParameterDataType, StringArgument: String, DateTimeArgument: DateTime, NumericalArgument: Double, DateTimeValue: DateTime, NumericalValue: Double, DateTimeValue2: DateTime, NumericalValue2: Double, Value: PointParameterValue, Value2: PointParameterValue, Weight: Double, CloseValue: Double, HighValue: Double, LowValue: Double, OpenValue: Double, GroupBounds: BoundsInterval, ArgumentBounds: BoundsInterval, Group: PointParameterValueEx

### `Point2D`
**Свойства:** X: Double, Y: Double

### `Point2DData`
**Свойства:** X: Double, Y: Double

### `Point3D`
**Свойства:** Z: Double

### `Point3DData`
**Свойства:** Z: Double

### `PointGroup`
**Свойства:** Points: List`1, Bounds: BoundsInterval, AdditionalData: Object

### `PointParameterValue`
**Свойства:** ValueType: ParameterDataType, DateTimeValue: DateTime, NumericalValue: Double
**Методы:**
- `Int32 CompareTo(PointParameterValue other) (+5)`

### `PointParameterValueEx`
**Свойства:** ValueType: ParameterDataType, DateTimeValue: DateTime, NumericalValue: Double, StringValue: String
**Методы:**
- `Int32 CompareTo(PointParameterValueEx other) (+5)`

### `PointsGroup`
**Свойства:** Id: Guid, Points: List`1, GroupBounds: BoundsInterval, ArgumentBounds: BoundsInterval, AdditionalData: Object

### `PointViewParameters`
**Свойства:** Id: Guid, LabelText: String, Color: Nullable`1

### `PositionInMenuExtensions`
**Методы:**
- `String GetName(PositionInMenu positionInMenu)`

### `PossibleValue`
**Свойства:** Class: PossibleValueType, Name: StringParameter, ConfigurationTerms: ReferenceObjectCollection`1, ConfigurationVariables: ReferenceObjectCollection`1
**Методы:**
- `Task GenerateVariables(CancellationToken cancellationToken)`
- `ConfigurationTerm CreateConfigurationTerm(Guid listObjectClass) (+1)`
- `ConfigurationVariable CreateConfigurationVariable(Guid listObjectClass) (+1)`

### `PossibleValuesReference`
**Свойства:** Classes: PossibleValuesTypes

### `PossibleValuesTypes`
**Свойства:** PossibleValue: PossibleValueType

### `PossibleValueType`
**Свойства:** Classes: PossibleValuesTypes, IsPossibleValue: Boolean

### `PreviewParameterInfo`
**Свойства:** Type: Type, Value: Object, Name: String

### `PrintingProfileReference`
**Свойства:** Classes: PrintingProfileTypes

### `PrintingProfileType`
**Свойства:** Classes: PrintingProfileTypes, IsTimeChartPrintingProfile: Boolean

### `PrintingProfileTypes`
**Свойства:** TimeChartPrintingProfile: PrintingProfileType

### `ProductCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `ProductDesignNumberCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `ProductDocumentObject`
**Свойства:** MaterialsLink: OneToManyRelation, MainMaterialLink: OneToOneLink, BasicMaterial: MaterialReferenceObject, MaterialsMark: AbstractMarkReferenceObject

### `ProductionUnit`
**Свойства:** Number: StringParameter, Code: StringParameter, ShortName: StringParameter, FunctionType: Int32Parameter, AreaFixingType: Int32Parameter, PurposeType: Int32Parameter, EquipmentLink: OneToManyLink, LinkedEquipmentReference: Reference
**Методы:**
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`

### `ProductMilestoneCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `ProductOptionsReference`
**Свойства:** AllOptions: IList`1, Classes: ProdutOptionsTypes

### `ProductOptionsReferenceObject`
**Свойства:** Class: ProductOptionsType, Name: StringParameter, Code: String, Comment: String, Status: OptionStatus, DefaultMajorMinor: DefaultProductOptionKind, PossibleOptionValues: ReferenceObjectCollection, ProjectOptions: IEnumerable`1
**Методы:**
- `ReferenceObject AddPossibleOptionValues(ReferenceObject newLinkedObject)`
- `Boolean RemovePossibleOptionValues(ReferenceObject linkedObject)`

### `ProductOptionsType`
**Свойства:** Classes: ProdutOptionsTypes, IsOption: Boolean

### `ProductOptionValuesReference`
**Свойства:** Classes: ProductOptionValuesTypes

### `ProductOptionValuesReferenceObject`
**Свойства:** Class: ProductOptionValuesType, Value: StringParameter, Image: ImageParameter, Comment: StringParameter, Code: String, Status: OptionStatus, Option: ProductOptionsReferenceObject, ProjectOptionValues: IEnumerable`1

### `ProductOptionValuesType`
**Свойства:** Classes: ProductOptionValuesTypes, IsValue: Boolean

### `ProductOptionValuesTypes`
**Свойства:** Value: ProductOptionValuesType

### `ProductsApplicabilityReference`
**Свойства:** Classes: ProductsApplicabilityTypes
**Методы:**
- `ApplicabilityInterval CreateInterval()`
- `ApplicabilityConditions CreateConditions()`
- `IEnumerable`1 GetIntervals(Guid objectGuid) (+1)`
- `List`1 GetApplicabilityObjects(List`1 objectGuids)` [has Async]
- `Void CopyApplicability(DesktopObject fromObject, DesktopObject toObject)`
- `IEnumerable`1 CopyIntervals(Guid fromObject, Guid toObject)`
- `ApplicabilityConditions CopyConditions(Guid fromObject, Guid toObject)`
- `Void DeleteIntervals(Guid objectGuid)`
- `ApplicabilityConditions GetApplicabilityConditions(Guid objectGuid) (+1)`
- `List`1 GetApplicability(IEnumerable`1 objectGuids)` [has Async]
- `Void DeleteApplicabilityConditions(Guid objectGuid)`
- `Void DeleteApplicability(IEnumerable`1 objectGuids)` [has Async]
- `Void AddUnsavedApplicability(IntervalReferenceObject obj)`
- `Void RemoveUnsavedApplicability(IntervalReferenceObject obj)`

### `ProductsApplicabilityType`
**Свойства:** Classes: ProductsApplicabilityTypes, IsInterval: Boolean, IsConditions: Boolean, IsBaseApplicability: Boolean, IsModifiedApplicability: Boolean

### `ProductsApplicabilityTypes`
**Свойства:** Interval: ProductsApplicabilityType, Conditions: ProductsApplicabilityType, BaseApplicability: ProductsApplicabilityType, ModifiedApplicability: ProductsApplicabilityType

### `ProductsClassifierActionReferenceObject`
**Свойства:** Class: ProductsClassifierActionsType, Action: Int32Parameter, AllValues: BooleanParameter, OptionActionType: OptionActionType, SelectedOption: ProductOptionsReferenceObject, SelectedOptionValue: ProductOptionValuesReferenceObject, ChangingOption: ProductOptionsReferenceObject, ChangingOptionValues: ReferenceObjectCollection`1
**Методы:**
- `ReferenceObject AddChangingOptionValue(ProductOptionValuesReferenceObject newLinkedObject)`
- `Boolean RemoveChangingOptionValue(ProductOptionValuesReferenceObject linkedObject)`

### `ProductsClassifierActionsReference`
**Свойства:** Classes: ProductsClassifierActionsTypes

### `ProductsClassifierActionsType`
**Свойства:** Classes: ProductsClassifierActionsTypes

### `ProductsClassifierActionsTypes`
**Свойства:** ActionType: ProductsClassifierActionsType

### `ProductsClassifierOptionsReference`
**Свойства:** Classes: ProductsClassifierOptionsTypes

### `ProductsClassifierOptionsReferenceObject`
**Свойства:** Class: ProductsClassifierOptionsType, IsHidden: BooleanParameter, IsNotEditable: BooleanParameter, OptionGroup: StringParameter, Option: ProductOptionsReferenceObject, DefaultOptionValue: ProductOptionValuesReferenceObject, OptionValues: ReferenceObjectCollection`1
**Методы:**
- `ReferenceObject AddOptionValue(ProductOptionValuesReferenceObject newLinkedObject)`
- `Boolean RemoveOptionValue(ProductOptionValuesReferenceObject linkedObject)`

### `ProductsClassifierOptionsType`
**Свойства:** Classes: ProductsClassifierOptionsTypes, IsOption: Boolean

### `ProductsClassifierOptionsTypes`
**Свойства:** Option: ProductsClassifierOptionsType

### `ProductsClassifierReference`
**Свойства:** Classes: ProductsClassifierTypes
**Методы:**
- `ProductsClassifierReferenceObject Find(String denotation)` [has Async]

### `ProductsClassifierReferenceObject`
**Свойства:** Parent: ProductsClassifierReferenceObject, Class: ProductsClassifierType, Name: StringParameter, Denotation: StringParameter, Image: ImageParameter, SpecificStructure: BooleanParameter, OptionsManagement: Boolean, DesignStructure: NomenclatureReferenceObject, ProjectOptionValues: IEnumerable`1, OptionsObjectList: OneToManyTable, Options: IEnumerable`1, OptionActionsObjectList: OneToManyTable, OptionActions: IEnumerable`1, InstancesLink: OneToManyLink, Instances: IEnumerable`1, Specifications: IEnumerable`1, SpecificationRequirements: ReferenceObject, ProductsSpecificationsLink: OneToManyLink, SerialProductNumbersLink: OneToManyLink, LinkedOptionTableSet: OptionsTableSetReferenceObject, ProjectOptionValueLink: OneToManyLink, OptionSetLink: OneToManyLink, OptionSets: IEnumerable`1, DesignNumbers: IEnumerable`1, SerialProductNumbers: IEnumerable`1, Milestones: IEnumerable`1
**Методы:**
- `Boolean IncludedInApplicabilityInterval(ReferenceObject productsInterval)`
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`

### `ProductsClassifierReferenceObjectHelper`
**Методы:**
- `List`1 GetAvalableProducOptionValues(ProductsClassifierReferenceObject product, Nullable`1 activityDate, Boolean& isLimitedByProduct)`
- `Boolean MatchByActivityDate(ProductsClassifierReferenceObject product, Nullable`1 activityDate)`
- `ProductsClassifierReferenceObject GetParentProduct(ProductsClassifierReferenceObject obj)`

### `ProductsClassifierType`
**Свойства:** Classes: ProductsClassifierTypes, IsProject: Boolean, IsProduct: Boolean, IsProductModification: Boolean, IsProductConfiguration: Boolean

### `ProductsClassifierTypes`
**Свойства:** Project: ProductsClassifierType, Product: ProductsClassifierType, ProductModification: ProductsClassifierType, ProductConfiguration: ProductsClassifierType

### `ProductsDesignNumbersReference`
**Свойства:** Classes: ProductsDesignNumbersTypes

### `ProductsDesignNumbersReferenceObject`
**Свойства:** Class: ProductsDesignNumbersType, Number: Int32Parameter, Description: StringParameter, Product: ProductsClassifierReferenceObject, Configuration: ProductsClassifierReferenceObject

### `ProductsDesignNumbersType`
**Свойства:** Classes: ProductsDesignNumbersTypes, IsProductDesignNumber: Boolean

### `ProductsDesignNumbersTypes`
**Свойства:** ProductDesignNumber: ProductsDesignNumbersType

### `ProductsInstancesReference`
**Свойства:** Classes: ProductsInstancesTypes

### `ProductsInstancesReferenceObject`
**Свойства:** Class: ProductsInstancesType, SerialNumber: StringParameter, Number: Int32Parameter, Product: ProductsClassifierReferenceObject

### `ProductsInstancesType`
**Свойства:** Classes: ProductsInstancesTypes, IsProductInstance: Boolean

### `ProductsInstancesTypes`
**Свойства:** ProductInstance: ProductsInstancesType

### `ProductsMilestonesReference`
**Свойства:** Classes: ProductsMilestonesTypes

### `ProductsMilestonesReferenceObject`
**Свойства:** Class: ProductsMilestonesType, MilestoneNumber: Int32Parameter, Description: StringParameter, Product: ProductsClassifierReferenceObject, Configuration: ReferenceObject

### `ProductsMilestonesType`
**Свойства:** Classes: ProductsMilestonesTypes, IsProductMilestone: Boolean

### `ProductsMilestonesTypes`
**Свойства:** ProductMilestone: ProductsMilestonesType

### `ProductsTermGroup`
**Свойства:** Connection: ServerConnection, Products: List`1

### `ProductStructure`
**Свойства:** ObjectId: String, Name: String

### `ProductStructureData`
**Свойства:** ObjectId: String, Name: String

### `ProductStructureReference`
**Свойства:** Classes: ProductStructureTypes
**Методы:**
- `Void InsertProductStructure(ProductStructureReferenceObject parentStructure, NomenclatureObject parentObject, ProductStructureReferenceObject structure)`
- `Void ReplaceByStructure(ProductStructureReferenceObject parentStructure, Guid hierarchyLinkId, ProductStructureReferenceObject replacementStructure)`

### `ProductStructureReferenceObject`
**Свойства:** Class: ProductStructureType, Name: StringParameter, Processes: ReferenceObjectCollection, NomenclatureObject: NomenclatureObject
**Методы:**
- `ReferenceObject AddTP(ReferenceObject newLinkedObject)`
- `Boolean RemoveTP(ReferenceObject linkedObject)`

### `ProductStructureType`
**Свойства:** Classes: ProductStructureTypes, IsProductStructureReferenceObject: Boolean, IsTechnologicalStructureReferenceObject: Boolean

### `ProductStructureTypes`
**Свойства:** ProductStructure: ProductStructureType, TechnologicalStructure: ProductStructureType

### `ProductTechnicalRequirementsReference`
**Свойства:** Classes: ProductTechnicalRequirementsTypes

### `ProductTechnicalRequirementsReferenceObject`
**Свойства:** Class: ProductTechnicalRequirementsType, Name: StringParameter, RequirementText: StringParameter, TechnicalCADData: ByteArrayParameter, Number: Int32Parameter, OriginalTTLink: ReferenceObject
**Методы:**
- `Void SetOriginalTTObject(ReferenceObject newLinkedObject)`

### `ProductTechnicalRequirementsType`
**Свойства:** Classes: ProductTechnicalRequirementsTypes, IsProductTechnicalRequirementsReferenceObject: Boolean

### `ProductTechnicalRequirementsTypes`
**Свойства:** ProductTechnicalRequirementsReferenceObject: ProductTechnicalRequirementsType

### `ProdutOptionsTypes`
**Свойства:** Option: ProductOptionsType

### `ProgressIndicatorAccessor`
**Свойства:** Text: String [RU: Текст]
**Методы:**
- `Void Hide()` [RU: Скрыть]
- `Void Show()` [RU: Скрыть]
- `Void Показать()` [RU alternative]

### `ProgressParameter`
**Свойства:** IsReadOnly: Boolean, Value: Double

### `ProjectDateTimeEditRepositoryItemXMLData`
**Свойства:** ShiftToWorkTimeAtValueChange: Boolean

### `ProjectMailTask`
**Свойства:** CanReject: Boolean, Responsible: User, Project: ProjectReferenceObject, CopyTo: User[]
**Методы:**
- `Void Send()`

### `ProjectMailTaskData`
**Свойства:** Task: ProjectMailTask, ResponsibleGuid: Guid, Responsible: User, ProjectGuid: Guid, Project: ProjectReferenceObject, CopyTo: List`1
**Методы:**
- `User[] GetCopyTo()`
- `Void SetCopyTo(User[] users)`

### `ProjectManagementReferenceAccessor`
**Методы:**
- `Void OpenProjectEditor(RefObjList projects, String view, String style)` [RU: ОткрытьРедакторПроектов]
- `Void OpenWorksUsage(RefObj project, String view, String style)` [RU: ОткрытьРедакторПроектов]
- `Void OpenResourcesUsage(RefObj project, RefObj resource, String view, String style)` [RU: ОткрытьИспользованиеРесурсов]
- `Void ОткрытьИспользованиеРабот(Объект проект, String вид, String стиль)` [RU alternative]

### `ProjectObject`
**Свойства:** Calendar: CalendarReferenceObject
**Методы:**
- `List`1 GetPlanList()`
- `Void AddPlan(ProjectObject plan)`

### `ProjectOptionsReference`
**Свойства:** Classes: ProjectOptionsTypes

### `ProjectOptionsReferenceObject`
**Свойства:** Class: ProjectOptionsType, Code: String, Kind: ProjectOptionsKind, IsMajor: Boolean, Values: IList`1, ProductImpact: OptionImpactKind, ProductOption: ProductOptionsReferenceObject, OptionsTableSets: OptionsTableSetReferenceObject, OptionsTableInColumns: ReferenceObjectCollection, OptionsTableInRows: ReferenceObjectCollection, OptionsTableInHiddenOptions: ReferenceObjectCollection
**Методы:**
- `String GetProductOptionName()`

### `ProjectOptionsType`
**Свойства:** Classes: ProjectOptionsTypes, IsProjectOption: Boolean

### `ProjectOptionsTypes`
**Свойства:** ProjectOption: ProjectOptionsType

### `ProjectOptionValuesReference`
**Свойства:** Classes: ProjectOptionValuesTypes

### `ProjectOptionValuesReferenceObject`
**Свойства:** Class: ProjectOptionValuesType, Name: StringParameter, Code: String, ProjectOption: ProjectOptionsReferenceObject, ProductOptionValue: ProductOptionValuesReferenceObject, ConfigurationManagerObjects: IEnumerable`1, IncompleteEquipments: IEnumerable`1, OptionsTableSet: OptionsTableSetReferenceObject

### `ProjectOptionValuesType`
**Свойства:** Classes: ProjectOptionValuesTypes, IsProjectOptionValues: Boolean

### `ProjectOptionValuesTypes`
**Свойства:** ProjectOptionValue: ProjectOptionValuesType

### `ProjectReference`
**Свойства:** Classes: ProjectTypes
**Методы:**
- `Boolean ShowErrorLinkDialog(TaskLinkReferenceObject errorLink)`
- `IComparer`1 GetAfterLoadSortComparer()`

### `ProjectReferenceObject`
**Свойства:** Name: String, AutoCheckOut: Boolean
**Методы:**
- `Void CheckInProject(Boolean ShowSaveDialog)`

### `ProjectStylesReference`
**Свойства:** Classes: ProjectStylesTypes

### `ProjectStylesReferenceObject`
**Свойства:** Class: ProjectStylesType, Name: StringParameter, TaskHeight: PercentParameter, ProgressHeight: PercentParameter, TaskShift: PercentParameter, ProgressShift: PercentParameter, TaskColor: Int32Parameter, ProgressColor: Int32Parameter, LineSkew: Boolean, LeftEndStyle: ImageReferenceObject, RightEndStyle: ImageReferenceObject

### `ProjectStylesType`
**Свойства:** Classes: ProjectStylesTypes, IsProjectStyle: Boolean

### `ProjectStylesTypes`
**Свойства:** ProjectStyle: ProjectStylesType

### `ProjectTasksOrder`
**Свойства:** Tasks: List`1

### `ProjectType`
**Свойства:** Classes: ProjectTypes, IsBaseTask: Boolean, IsTask: Boolean, IsProject: Boolean, IsProjectsFolder: Boolean

### `ProjectTypes`
**Свойства:** Project: ProjectType, Task: ProjectType, BaseTask: ProjectType

### `PropertiesDisplayTypeExtensions`
**Методы:**
- `String GetName(PropertiesDisplayType type)`

### `Property`
**Свойства:** Name: String, Value: Object, DataValue: DynamicData

### `Property`1`
**Свойства:** Value: T

### `PropertyData`
**Свойства:** Name: String

### `ProtectedPreviewAttribute`
**Свойства:** IsSystem: Boolean, CanChangeCaption: Boolean, Caption: String, Value: Object, CanRemove: Boolean

### `QualityAnalysisResult`
**Свойства:** State: QualityAnalysisState, FullMessage: String, ShortMessage: String, IsFixable: Boolean

### `RawSettingsView`
**Свойства:** Id: Guid, Name: String, ConfigurationUseType: ConfigurationUseType, Configurations: ReadOnlyCollection`1, Type: SettingsViewType, InSettingsContext: Boolean

### `ReadOnlyGuidParameter`
**Свойства:** IsReadOnly: Boolean

### `RealPropertyData`
**Свойства:** Value: Double

### `RecursiveLoadDirectionExtensions`
**Методы:**
- `Boolean HasChildren(RecursiveLoadDirection loadDirection)`
- `Boolean HasParents(RecursiveLoadDirection loadDirection)`
- `Boolean HasChildrenOneLevel(RecursiveLoadDirection loadDirection)`
- `Boolean HasParentsOneLevel(RecursiveLoadDirection loadDirection)`

### `RedirectRuleAction`
**Свойства:** To: List`1, TextTemplate: String, SubjectTemplate: String
**Методы:**
- `MailRuleAction ToServer()`

### `Reference`
**Свойства:** Connection: ServerConnection, ConfigurationSettings: ConfigurationSettings, ConfigurationSettingsLinkGroup: ParameterGroup, SpecialConfigurationSettings: ConfigurationSettings, LinkInfo: LinkInfo, Storage: ReferencesStorage, LoadSettings: LoadSettings, PrototypeMode: Boolean, Prototypes: Reference, IsSlave: Boolean, Name: String, Icon: IconImage, ParameterGroup: ParameterGroup, Objects: ReferenceObjectCollection, Classes: ClassTree, Id: Int32, SearchQueries: SearchQueryReference, UndoManager: UndoManager
**Методы:**
- `List`1 IsUniqueObjects(ICollection`1 objects, Boolean reload)` [has Async]
- `Void LoadSignatures(IEnumerable`1 objects)` [has Async]
- `Void ReloadSignatures(IEnumerable`1 objects)` [has Async]
- `Void EndChanges(IEnumerable`1 objects) (+2)` [has Async]
- `List`1 CheckLooping(IEnumerable`1 hierarchyLinks)` [has Async]
- `Void Delete(IEnumerable`1 objects) (+1)` [has Async]
- `List`1 DeleteDesktopObjects(IEnumerable`1 objects)` [has Async]
- `IReadOnlyCollection`1 CreateComplexHierarchyLinks(IEnumerable`1 parents, IEnumerable`1 children, Boolean linkFromParents) (+1)` [has Async]
- `IReadOnlyCollection`1 CreateParentComplexHierarchyLinksWithInstanceData(IEnumerable`1 parents, IEnumerable`1 children)` [has Async]
- `IReadOnlyCollection`1 CreateChildComplexHierarchyLinksWithInstanceData(IEnumerable`1 parents, IEnumerable`1 children)` [has Async]
- `Void ImportFromParentStructure(IEnumerable`1 objects, StructureTypesReferenceObject activeStructure, StructureTypesReferenceObject parentStructure, DesignContextObject designContext)` [has Async]
- `Void ChangeMasterServer(IReadOnlyCollection`1 objects, ReferenceObject masterServer, String comment)` [has Async]
- `Void Unlock(IEnumerable`1 objects)` [has Async]
- `Void UpdateLastRevisionNames(ReferenceObject object) (+1)` [has Async]
- `ReferenceObject GetPrivateFolder()` [has Async]
- `Boolean CanCreateHierarchyLink(ReferenceObject parentObject, ClassObject parentClass, ReferenceObject childObject, ClassObject childClass) (+1)`
- `Boolean CanDeleteHierarchyLink(ComplexHierarchyLink link)`
- `Boolean ContainsEventRaising(EventHandler`1 eventHandler)`
- `Boolean ContainsEventRaised(EventHandler`1 eventHandler)`
- `Boolean CheckLicense(ClassObject classObject, Boolean throwOnError)`
- `List`1 SetObjectsOrder(ReferenceObject object, Int32 order) (+1)`
- `Boolean CanCreateUniqueObject(ClassObject classObject, IDictionary`2 values, ReferenceObject& existingObject) (+2)` [has Async]
- `Boolean CanCreateUniqueObjects(ICollection`1 parameters)` [has Async]
- `List`1 IsUnique(ICollection`1 objects, Boolean reload)` [has Async]
- `Filter GetAccessFilter()`
- `Void SetObjectsOwner(IEnumerable`1 objects, UserReferenceObject owner)` [has Async]
- `Void UseAsRevisions(Dictionary`2 objects, RevisionLevelObject revisionLevel, String sourceRevisionName)`
- `List`1 GetExistingRevisionNames(Guid logicalObjectGuid) (+1)`
- `ComplexHierarchyLink CreateEmptyHierarchLink(ReferenceObject childObject)`
- `Dictionary`2 LoadSimpleReferences(ServerConnection connection, Int32[] referenceIDs)`
- `Dictionary`2 LoadSimpleObjects(ServerConnection connection, Int32 referenceID, List`1 objectIDs)`
- `List`1 Find(Filter filter, Int32 maxCount, ReferenceObject parent, MacroContext formulaContext, LoadSettings loadSettings) (+16)` [has Async]
- `List`1 FindWithMaxCount(ParameterInfo parameter, ComparisonOperator op, Object value, Int32 maxCount, LoadSettings loadSettings) (+1)` [has Async]
- `ReferenceObject FindOne(ParameterInfo parameter, ComparisonOperator op, Object value) (+3)` [has Async]
- `IReferenceObjectCollection Load(ObjectIterator iterator, Filter filter, ReferenceObject rootObject, MacroContext formulaContext, RecursiveLoadDirection loadDirection)` [has Async]
- `IReferenceObjectCollection LoadWithInstances(ObjectIterator iterator, Filter filter, ReferenceObjectInstance rootObjectInstance, ReferenceObject rootObject, MacroContext formulaContext, RecursiveLoadDirection loadDirection)` [has Async]
- `Void Reload(IEnumerable`1 objects, IReadOnlyCollection`1 additionalSettings, Boolean forceLoadDeleted) (+2)` [has Async]
- `Void TryReload(IEnumerable`1 objects, IReadOnlyCollection`1 additionalSettings, Boolean forceLoadDeleted) (+2)` [has Async]
- `ReferenceObjectCollection CreateLoader(Filter filter, ReferenceObject parent, IEnumerable`1 sourceObjects, MacroContext formulaContext, Boolean ignoreLink) (+1)` [has Async]
- `ReferenceObjectCollection CreateParentsLoader(Filter filter, ReferenceObject referenceObject, MacroContext formulaContext)` [has Async]
- `PartialRecursiveCollection CreateRecursiveLoader(Filter filter, ReferenceObject parent, IEnumerable`1 sourceObjects, MacroContext formulaContext, RecursiveLoadDirection loadDirection, Boolean hierarchyLinksOnly) (+1)` [has Async]
- `PartialRecursiveCollection CreateRecursiveLoaderWithInstances(Filter filter, ReferenceObjectInstance parentInstance, IEnumerable`1 sourceObjects, MacroContext formulaContext, RecursiveLoadDirection loadDirection, Boolean hierarchyLinksOnly, ReferenceObject parent) (+1)` [has Async]
- `Void Refresh(Boolean objectsOnly) (+1)` [has Async]
- `Void ClearLoadedObjects()`
- `Void LoadLinks(List`1 rootObjects, LoadSettings settings)` [has Async]
- `List`1 GetDeletedObjects(Filter filter, Int32 count, Int32 offset, MacroContext formulaContext) (+1)` [has Async]
- `Int32 GetDeletedObjectsCount(Filter filter) (+1)` [has Async]
- `List`1 RecursiveLoad(IEnumerable`1 objects, RecursiveLoadDirection loadDirection, LoadSettings loadSettings)` [has Async]
- `ReferenceObject CreateReferenceObject(ReferenceObject parentObject, ClassObject classObject) (+3)`
- `ReferenceObject CreateRevisionsContainer(ReferenceObject parentObject, ClassObject classObject, Guid revisionsContainerGuid) (+1)`
- `ReferenceObjectCopySet CopyReferenceObject(ReferenceObject prototype, ReferenceObject parentObject, ClassObject classObject, Boolean copyChildren, IEnumerable`1 skip) (+6)`
- `ReferenceObjectCopySet CopyReferenceObjects(IEnumerable`1 sourceObjects, ReferenceObject parentObject, Boolean copyChildren, Boolean copyLinkedObjects) (+1)`
- `Boolean CanCreateReferenceObject(ReferenceObject prototype, ReferenceObject parentObject, ClassObject classObject)`
- `Void ValidateNewReferenceObject(ReferenceObject prototype, ReferenceObject parentObject, ClassObject classObject)`
- `Boolean UserHasAccessToCurrentStructureType(Boolean throwOnError)`
- `Boolean UserHasAccessToEditObjectsInCurrentStructureType(Boolean throwOnError)`
- `List`1 GetReports(ClassObject classObject) (+1)`
- `Boolean IsReportAssociatedClass(ClassObject classObject)`
- `List`1 GetReportGeneratorCommands(ClassObject classObject)`
- `Int32 CompareTo(Reference other)`

### `ReferenceAccessFilters`
**Свойства:** Reference: ReferenceInfo, IsModified: Boolean
**Методы:**
- `Filter GetFilter(UserReferenceObject userObject)`
- `Void SetFilter(UserReferenceObject userObject, Filter filter)`
- `Boolean RemoveFilter(UserReferenceObject userObject)`
- `Boolean Save()`
- `Void Clear()`
- `IEnumerator`1 GetEnumerator()`

### `ReferenceAccessor`
**Свойства:** Name: String [RU: Имя], Guid: Guid [RU: УникальныйИдентификатор], Id: Int32 [RU: Идентификатор], SignatureTypes: SignatureTypeObjList, ТипыПодписей: ТипыПодписей [RU only]

### `ReferenceAccessType`
**Свойства:** AccessTypeID: AccessTypeID, Type: AccessCommandType, Name: String, IsReference: Boolean, ChangeStructure: AccessCommand, ChangeExtendedParameters: AccessCommand, ChangeAccess: AccessCommand, Delete: AccessCommand, Export: AccessCommand, TablePaste: AccessCommand, Display: AccessCommand, ReferenceShowInCatalog: AccessCommand, ChangeWindowSettings: AccessCommand, EditCommonViews: AccessCommand, EditPersonalViews: AccessCommand, EditCommonCatalogs: AccessCommand, EditPersonalCatalogs: AccessCommand

### `ReferenceAppointment`
**Методы:**
- `Object GetCoreObject()`
- `Void Release()`
- `MacroContext GetMacroContext()`

### `ReferenceBuilder`
**Свойства:** ReferenceInfo: ReferenceInfo, Folder: ReferenceCatalogFolder, HierarchyType: ReferenceHierarchyType, Visibility: ReferenceVisibility, SupportsDesktop: Boolean, SupportsRecycleBin: Boolean, SupportsDataChangeLog: Boolean, SupportsRevisions: Boolean, RevisionNamingRule: RevisionNamingRuleObject, Configurator: Configurator, SupportsPrototypes: Boolean, SupportsStages: Boolean, SupportsExtendedParameters: Boolean, SupportsMandatoryAccess: Boolean, SupportsOwner: Boolean, SupportsObjectsInstances: Boolean, SupportsStructureTypes: Boolean, SupportsConfigurationSettings: Boolean, SupportsDesignContexts: Boolean, SupportsSubstitutesInContext: Boolean, SupportsActivityDates: Boolean, SupportsApplicability: Boolean, UniqueIndex: UniqueIndex, Scheme: Scheme, DefaultStage: SchemeStage, AuthorAccess: AccessGroup, CheckAccess: AccessRightsMode, SupportsEncryption: Boolean, IsActive: Boolean
**Методы:**
- `Void Save(Boolean createNameParameter)` [has Async]
- `Void Delete(ReferenceInfo reference)` [has Async]
- `Void MoveToAnotherFolder(ReferenceCatalogFolder folder)` [has Async]
- `Void Deactivate()` [has Async]
- `Void Activate()` [has Async]
- `Void RefreshInheritedAccesses()`
- `Void RefreshMainAccesses()`
- `Void ResetUsersSettings(Boolean clearViews)`
- `Void ResetUserWebSettings(User user, WebConfiguration configuration)`
- `Void RecreateFullTextSearchIndicies()` [has Async]

### `ReferenceCatalog`
**Свойства:** Connection: ServerConnection, RootFolder: ReferenceCatalogFolder, IsPDMInstalled: Boolean, IsDataExchangeInstalled: Boolean, IsLibraryInstalled: Boolean, IsNSIClassifierInstalled: Boolean, Root: ReferenceCatalogFolder
**Методы:**
- `Void Load()` [has Async]
- `List`1 GetReferences()`
- `List`1 GetFolders()`
- `ReferenceInfo Find(Int32 referenceId) (+3)`
- `ReferenceCatalogFolder FindFolderByName(String name)`
- `ReferenceCatalogFolder FindFolder(String fullName) (+1)`
- `Void RegisterSpecialReferenceObject(Guid parameterGroupGuid, Guid classObjectGuid, Type specialReferenceObjectType)`
- `Void RegisterSpecialReference(Guid parameterGroupGuid, SpecialReferenceFactory referenceFactory)`
- `List`1 GetSystemEventHandlers(Guid parameterGroupGuid)`
- `Boolean RegisterSystemEventHandler(ISystemEventHandlerProvider handler)`
- `Void Reload()`
- `List`1 GetAllReferences()`
- `ReferenceInfo FindReference(Int32 referenceId) (+3)`
- `Boolean IsLocked(Int32 referenceId) (+2)`
- `ReferenceBuilder CreateReferenceBuilder(ReferenceCatalogFolder folder)`
- `ReferenceCatalogFolder CreateFolder(String name, ReferenceCatalogFolder parent)`
- `Void RenameFolder(ReferenceCatalogFolder folder, String name)`
- `Void DeleteFolder(ReferenceCatalogFolder folder)`
- `Void MoveFolder(ReferenceCatalogFolder folder, ReferenceCatalogFolder newParent)`

### `ReferenceCatalogFolder`
**Свойства:** Catalog: ReferenceCatalog, Id: Int32, Guid: Guid, Parent: ReferenceCatalogFolder, Folders: ReadOnlyCollection`1, FullName: String, References: ReadOnlyCollection`1, Name: String
**Методы:**
- `ReferenceCatalogFolder CreateFolder(String name)` [has Async]
- `Void Rename(String name)` [has Async]
- `Void Delete()` [has Async]
- `Void MoveTo(ReferenceCatalogFolder newParent)` [has Async]
- `Boolean Contains(ReferenceCatalogFolder folder)`
- `Boolean ContainsReferences()`
- `Int32 CompareTo(ReferenceCatalogFolder other)`
- `Boolean IsEmpty()`

### `ReferenceCatalogFolderGroup`
**Свойства:** ChildLinksLoaded: Boolean, Text: String, FolderFullName: String, ReferenceCatalogFolder: ReferenceCatalogFolder

### `ReferenceCatalogHelper`
**Методы:**
- `String Serialize(Object value)`
- `Object DeSerialize(ServerConnection connection, String value)`
- `String SerClassObject(String reference, String classObject)`
- `String SerGroup(String reference, String group)`
- `String GetSerReference(String value)`
- `String GetSerObject(String value)`

### `ReferenceChangedCallback`
**Методы:**
- `Void Invoke(Int32 referenceId, ChangeType changeType, Int32 clientView)`
- `IAsyncResult BeginInvoke(Int32 referenceId, ChangeType changeType, Int32 clientView, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ReferenceChangedCallbackDebug`
**Методы:**
- `Void Invoke(Int32 referenceId, ChangeType changeType, Int32 clientView, String callStack)`
- `IAsyncResult BeginInvoke(Int32 referenceId, ChangeType changeType, Int32 clientView, String callStack, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `ReferenceClassArrayVariable`
**Свойства:** Type: Type, IsArray: Boolean, AllowNullValue: Boolean

### `ReferenceClassVariable`
**Свойства:** Type: Type, AllowNullValue: Boolean
**Методы:**
- `ClassObject FindClassObject(Guid referenceGuid, Guid classGuid, ServerConnection connection)`

### `ReferenceColumnData`
**Свойства:** IsEmpty: Boolean, Type: ColumnDataType

### `ReferenceComparer`
**Свойства:** Instance: ReferenceComparer
**Методы:**
- `Int32 Compare(Reference x, Reference y)`

### `ReferenceContext`
**Свойства:** ClassObject: Guid
**Методы:**
- `ReferenceContext GetOrCreate(Guid referenceGuid)`

### `ReferenceExtensions`
**Методы:**
- `Reference GetReference(ServerConnection connection, Int32 referenceId, ReferencesStorage storage, Boolean throwOnError) (+1)`
- `NomenclatureReference GetNomenclatureReference(Reference reference, Boolean throwOnError) (+1)`
- `Reference CreateReference(ServerConnection connection, String referenceName) (+3)`
- `IDisposable ClearAndHoldUseConfigurationSettings(Reference reference)`
- `IDisposable ChangeAndHoldConfigurationSettings(Reference reference, ConfigurationSettings configurationSettings, ParameterGroup linkGroup) (+2)`
- `ReferenceObjectCollection GetObjects(Reference reference, CatalogFolder folder)`
- `List`1 GetAllLoadedObjects(Reference reference)`
- `ReferenceObject FindLoadedReferenceObject(Reference reference, Guid guid)`
- `IDisposable DisableCheckByActiveDate(Reference reference)`

### `ReferenceFiles`
**Методы:**
- `Void Load(FileReferenceObject fileObject, Func`2 condition) (+2)` [has Async]
- `Dictionary`2 LoadAsStream(IEnumerable`1 files)` [has Async]
- `Dictionary`2 HasTfrFilesOnServer(ICollection`1 grbFileObjects, CancellationToken cancellationToken)`
- `Dictionary`2 LoadTfrFiles(ICollection`1 grbFileObjects, Boolean updateTfrIfExists, CancellationToken cancellationToken)`

### `ReferenceFilter`
**Свойства:** Id: Int32, Guid: Guid, Reference: ReferenceInfo, Name: String, IsPrivate: Boolean, IsAdded: Boolean, IsModified: Boolean
**Методы:**
- `List`1 GetFilters(ReferenceInfo reference)`
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `Boolean Save()`
- `Boolean Delete()`
- `Int32 CompareTo(ReferenceFilter other)`

### `ReferenceFilterObject`
**Свойства:** ShowButton: BooleanParameter, ButtonIcon: IconParameter, ButtonText: StringParameter, ButtonHint: StringParameter, Filter: Filter, IsPublic: Boolean, FilterReference: ReferenceInfo
**Методы:**
- `Boolean IsRightGroup(ParameterGroup masterGroup)`
- `Void SaveFilter()`

### `ReferenceFiltersGroupObject`
**Свойства:** FiltersGroup: FilterDataCollection

### `ReferenceGroup`
**Свойства:** ParameterGroup: ParameterGroup, HasChildren: Boolean

### `ReferenceHelper`
**Методы:**
- `ReferenceInfo Find(ServerConnection connection, String referenceName) (+2)`
- `Reference Create(ServerConnection connection, String referenceName, Boolean prototypeMode, Boolean throwOnError) (+3)`

### `ReferenceHierarchyTypeExtensions`
**Методы:**
- `String GetName(ReferenceHierarchyType type)`

### `ReferenceIndexManager`
**Методы:**
- `List`1 GetIndexes(ReferenceInfo referenceInfo)` [has Async]

### `ReferenceInfo`
**Свойства:** Connection: ServerConnection, Catalog: ReferenceCatalog, Parent: ReferenceCatalogFolder, Description: ParameterGroup, DescriptionLoaded: Boolean, Classes: ClassTree, IsStatic: Boolean, Id: Int32, HierarchyGroupId: Int32, Guid: Guid, Name: String, Icon: IconImage, IconLoaded: Boolean, Visibility: ReferenceVisibility, HierarchyType: ReferenceHierarchyType, ActivityStatus: GroupActivityStatus, SupportsDesktop: Boolean, SupportsRecycleBin: Boolean, SupportsNomenclature: Boolean, HasHierarchy: Boolean, SupportsObjectsInstances: Boolean, IsObjectsInstancesImpl: Boolean, SupportsStructureTypes: Boolean
**Методы:**
- `ParameterGroup RefreshDescription()` [has Async]
- `Reference CreateReference(Boolean prototypeMode) (+1)` [has Async]
- `Void RefreshStaticReference()`
- `Int32 CompareTo(ReferenceInfo other)`
- `LicenseFunction GetLicense(ClassObject classObject)`
- `Boolean HasTypesLicense()`
- `LicenseFunction GetStructureEditLicense()`

### `ReferenceInfoHelper`
**Методы:**
- `Boolean CheckReferenceIsDeactivating(ReferenceInfo referenceInfo) (+1)`
- `Boolean CheckDeactivationWasCancelled(ReferenceInfo referenceInfo) (+1)`
- `Void CancelDeactivation(ReferenceInfo referenceInfo) (+1)`
- `Void AddActiveTask(ReferenceInfo referenceInfo, Task task) (+1)`

### `ReferenceInfoRepositoryItemXMLData`
**Свойства:** ShowHiddenReferences: Boolean, ShowInnactiveReferences: Boolean, ShowHierarchyGroups: Boolean, ShowObjectInstancesGroups: Boolean

### `ReferenceLink`
**Свойства:** Text: String, ReferenceGuid: Guid, Reference: ReferenceInfo, Filter: Filter, ViewType: ReferenceViewType, CanContainChildren: Boolean, HideReferenceTextAndIcon: Boolean

### `ReferenceLinkAdditionalSettings`
**Свойства:** Data: ReferenceLinkAdditionalSettingsData, IsValid: Boolean, IsLoaded: Boolean, LinkGroup: ParameterGroup, LinkClass: ClassObject
**Методы:**
- `ReferenceLinkAdditionalSettings Create(ParameterGroup linkGroup, ClassObject linkClass)`
- `Void Reload()`
- `Boolean Save()`
- `Boolean Remove()`

### `ReferenceLinkAdditionalSettingsData`
**Свойства:** DefaultParentObjectGuid: Guid, DefaultParentObjectName: String, ShowSelectObjectDialog: Boolean, PathIsMacro: Boolean, Macros: String, ForbidSelectionFromOtherFolders: Boolean
**Методы:**
- `String Serialize()`
- `Void Deserialize(String data)`

### `ReferenceObject`
**Свойства:** BaseObject: StateGuidDomainObject, Reference: Reference, Id: Int32, Guid: Guid, ParameterValues: ParameterCollection, SystemFields: ReferenceObjectSystemFields, HasChildren: Boolean, IsHasChildrenLoaded: Boolean, HasSubfolders: Boolean, Parent: ReferenceObject, IsParentLoaded: Boolean, NewParent: ReferenceObject, Parents: ReferenceObjectCollection, IsParentsLoaded: Boolean, Children: ReferenceObjectCollection, IsChildrenLoaded: Boolean, Class: ClassObject, IsPrivateFolder: Boolean, IsInPrivateFolder: Boolean, CanEdit: Boolean, CanDelete: Boolean, IsActualVersion: Boolean, AttachToMasterObject: Boolean, IsAdded: Boolean, IsNew: Boolean, IsPartial: Boolean, IsDeleted: Boolean, IsModified: Boolean, IsChanged: Boolean, IsPrototype: Boolean, PacketSet: DesktopObjectPacketSet`1, SaveSet: ReferenceObjectSaveSet, CanUnlock: Boolean, Changing: Boolean, StandAloneChanging: Boolean, ChangingObject: ReferenceObject, StandAloneCopies: ReadOnlyCollection`1, IsCopy: Boolean, EditableObject: ReferenceObject, Prototype: ReferenceObject, ChangesCounter: Int32, IsNotActual: Boolean, Master: DesktopObject, MasterObject: ReferenceObject, MasterHierarchyLink: ComplexHierarchyLink, IsMaster: Boolean, Versions: ReferenceObjectCollection, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, CanCheckOut: Boolean, CanCheckIn: Boolean, CanUndoCheckOut: Boolean, IsInRecycleBin: Boolean, LockState: ReferenceObjectLockState, CanContainChildren: Boolean, SupportMultiAttachment: Boolean, Signatures: SignatureCollection, ObjectStages: ObjectStageInfo
**Методы:**
- `Boolean MoveUp()`
- `Boolean MoveDown()`
- `Boolean Swap(ReferenceObject objectToSwap)`
- `Void IncreaseSelectionRank(String context)`
- `List`1 GetAllLinkedFiles()`
- `Void Load(IReadOnlyCollection`1 parameters, IReadOnlyCollection`1 toOneLinks) (+2)` [has Async]
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`
- `IReadOnlyCollection`1 GetLinkedComplexLinks(Guid linkGuid) (+1)` [has Async]
- `Boolean TryLinkedComplexLinks(Guid linkGuid, IReadOnlyCollection`1& links) (+1)` [has Async]
- `ReferenceObject CreateRevision(RevisionLevelObject revisionLevel, ReferenceObject parent, Boolean recursive, Boolean copyApplicability)`
- `Boolean UseAsRevision(Guid logicalObjectGuid, Boolean throwOnError)`
- `Boolean UseAsNewLogicalObject(Boolean throwOnError)`
- `List`1 GetExistingRevisionNames()`
- `List`1 GetRevisions()`
- `ReadOnlyCollection`1 GetSelectedRevisions()` [has Async]
- `Boolean IsSelectRevisionFailed()`
- `Filter GetRevisionContainerFilter()` [has Async]
- `Boolean CopySignaturesFromRevision(ReferenceObject sourceObject, Boolean throwOnError)`
- `IReadOnlyCollection`1 GetRemarks()`
- `ReferenceObject CreateCopy(ClassObject newClass, OneToManyTable destLink, IEnumerable`1 skip, CopyReferenceObjectsContext context, Boolean loadLinks, Boolean forRevision, Boolean copyLinks) (+4)`
- `ReferenceObject CreateFullCopy(IEnumerable`1 linkIds, ClassObject classObject, ReferenceObject parentObject)`
- `ReferenceObject CopyAllTo(Reference reference)`
- `Void Refresh(ReferenceObject source)`
- `Boolean CanCopy(ParameterInfo parameter) (+1)`
- `Boolean BelongsToConfigurationSettings()`
- `Boolean HasLinkedObjects(ICollection`1 relations, Boolean loadDeleted) (+2)`
- `ParameterGroup FindRelation(Guid groupGuid)`
- `Boolean ContainsRelation(Int32 groupId)`
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, ComplexHierarchyLink hierarchyLink, ReferenceObjectInstance objectInstance, Boolean throwOnError) (+8)`
- `Boolean IsLoaded(ReferencePath path, ComplexHierarchyLink hierarchyLink) (+1)`
- `Boolean Match(Filter filter)`
- `Stack`1 GetPath(ReferenceObject rootObject) (+1)` [has Async]
- `Void Reload(LoadSettings loadSettings) (+2)` [has Async]
- `Boolean TryReload()` [has Async]
- `Boolean IsAvailable()`
- `ComplexHierarchyLink GetParentLink(ReferenceObject parentObject)` [has Async]
- `ICollection`1 GetParentLinks(ReferenceObject parentObject)`
- `ComplexHierarchyLink GetChildLink(ReferenceObject childObject)` [has Async]
- `ICollection`1 GetChildLinks(ReferenceObject childObject)`
- `ComplexHierarchyLink CreateParentLink(ReferenceObject parentObject)`
- `ComplexHierarchyLink CreateChildLink(ReferenceObject childObject)`
- `ComplexHierarchyLinkInstanceData CreateChildLinkWithInstancesData(ReferenceObject childObject, ReferenceObjectInstance sourceStructureObjectInstance, ReferenceObjectInstance parentObjectInstance)`
- `ComplexHierarchyLinkInstanceData CreateChildLinkWithBaseInstancesData(ReferenceObject childObject, ReferenceObjectInstance baseInstance, ReferenceObjectInstance parentObjectInstance)`
- `Boolean DeleteLink(ComplexHierarchyLink link)`
- `Boolean CanCreateChildObject(ClassObject childClass)`
- `Boolean CanCreateChildLink(ReferenceObject childReferenceObject)`
- `Boolean CanCreateParentLink(ReferenceObject parentReferenceObject)`
- `Boolean SetSignature(User user, SignatureType signatureType, String resolution, Boolean throwOnError, X509Certificate2 certificate) (+1)`
- `List`1 GetSignatures(Int32 objectVersion)`
- `Byte[] GetSigningReferenceObjectData()`
- `DigitalSignatureContent GetDigitalSignatureContent()`
- `Void OnParameterChanged(Parameter p)`
- `Boolean CanChangeParameter(Parameter p, Object newValue)`
- `Boolean IsUnique(ReferenceObject& existingObject)`
- `Boolean SetParent(ReferenceObject parentObject)`
- `Boolean CanSetParent(ReferenceObject parentObject)`
- `Boolean ValidateParentObject(ReferenceObject parentObject, ClassObject classObject, Boolean throwOnError)`
- `Void SetOwnerUser(UserReferenceObject owner)` [has Async]
- `Boolean CheckIsObjectVersionActual()`
- `Void BeginChanges(Boolean reload) (+2)` [has Async]
- `Boolean TryBeginChanges(ReferenceObject& actualObject)`
- `ReferenceObject BeginStandAloneChanges(ComplexHierarchyLink hierarchyLink) (+1)`
- `Boolean TryBeginStandAloneChanges(ComplexHierarchyLink hierarchyLink, ReferenceObject& referenceObject)`
- `Boolean ApplyChanges()` [has Async]
- `Boolean EndChanges()` [has Async]
- `Void CreateSaveSet()`
- `Void CancelChanges()` [has Async]
- `Void Unlock()` [has Async]
- `Void Delete()` [has Async]

### `ReferenceObjectArrayVariable`
**Свойства:** Type: Type, IsArray: Boolean

### `ReferenceObjectCollection`1`
**Свойства:** AsList: IList`1, Item: T
**Методы:**
- `Int32 IndexOf(T item)`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `ReferenceObjectCollectionExtensions`
**Методы:**
- `HashSet`1 GetLoadedObjects(IReferenceObjectCollection objectCollection, Boolean includeParent)`
- `Void FillEmptyParameters(IEnumerable`1 objects)`

### `ReferenceObjectComparer`
**Методы:**
- `Int32 Compare(ReferenceObject x, ReferenceObject y)`

### `ReferenceObjectCopySet`
**Свойства:** Context: CopyReferenceObjectsContext
**Методы:**
- `ReferenceObject GetNewObject(ReferenceObject source)`
- `Boolean EndChanges()` [has Async]

### `ReferenceObjectEntrance`
**Свойства:** Owner: ReferenceObjectEntrancesTree, Object: ReferenceObject, DirectEntrancesCount: Nullable`1, EntrancesCount: Double, Children: IEnumerable`1
**Методы:**
- `IEnumerable`1 GetDirectEntrances()`

### `ReferenceObjectEntrancesTree`
**Свойства:** MainObject: ReferenceObject, AllObjects: IEnumerable`1, RootObjects: IEnumerable`1
**Методы:**
- `Void Load()`
- `Void Reload()`

### `ReferenceObjectExtensions`
**Методы:**
- `Boolean IsLinkedToNomenclature(ReferenceObject referenceObject)`
- `NomenclatureObject GetLinkedNomenclatureObject(ReferenceObject referenceObject)` [has Async]
- `Dictionary`2 GetLinkedNomenclatureObjects(IEnumerable`1 referenceObjects)` [has Async]
- `Void Modify(TObject referenceObject, Action`1 action, ReferenceObjectSaveSet saveSet, Boolean cancelOnError, Boolean reload, Boolean applyChanges) (+2)` [has Async]
- `Boolean TryActualBeginChanges(TReferenceObject& referenceObject, String& message, ClassObject classObject, Boolean unlock) (+1)` [has Async]
- `Void ModifyActual(TReferenceObject& referenceObject, Action`1 action, Boolean endChanges)`
- `Void TryEndChanges(TReferenceObject referenceObject, Action`1 action)`
- `Boolean TryGetActual(TReferenceObject& referenceObject)`
- `Void RemoveNotActualParentLinks(ReferenceObject referenceObject)`
- `List`1 GetChangedHierarchyLinks(IEnumerable`1 objects)`
- `ObjectValue GetObjectValue(DesktopObject obj, ReferencePath path, ComplexHierarchyLink parentLink, Boolean throwOnError)`
- `String GetPropertyHyperlink(ReferenceObject obj, String serverAddress)` [has Async]
- `String GetHyperlink(ReferenceObject obj, String serverAddress)` [has Async]
- `String GetFileHyperlink(FileObject file, String serverAddress)` [has Async]

### `ReferenceObjectExtensions`
**Методы:**
- `IEnumerable`1 GetObjectInstances(ReferenceObject referenceObject, Boolean loadParents)` [has Async]
- `IEnumerable`1 GetObjectInstancesWithoutConfiguration(ReferenceObject referenceObject)` [has Async]
- `ReferenceObject GetReferenceObject(ReferenceObjectInstance referenceObject, Reference reference)` [has Async]

### `ReferenceObjectExtensions`
**Методы:**
- `Boolean IsSubstituteInActiveDesignContext(ReferenceObject referenceObject)`
- `Boolean IsSubstituteInDesignContext(ReferenceObject referenceObject, DesignContextObject designContext)`
- `DesignContextChangeStatus GetDesignContextStatus(ReferenceObject referenceObject)`

### `ReferenceObjectInstance`
**Свойства:** ReferenceObject: ReferenceObject, LinkedComplexLink: ComplexHierarchyLink, ComplexHierarchyLink: ComplexHierarchyLink, SourceStructureInstances: IEnumerable`1, AltRepGroupGuidParameter: Parameter
**Методы:**
- `Int32 ReplaceRepresentation(Int32 sourceNewAltRepId)` [has Async]
- `IEnumerable`1 GetTargetStructureInstances(StructureTypesReferenceObject targetStructure)` [has Async]
- `IEnumerable`1 GetTargetStructuresInstances()` [has Async]

### `ReferenceObjectLinks`
**Свойства:** Owner: DesktopObject, IsOneToOneLoaded: Boolean, ToOne: OneToOneLinkManager, ToOneToComplexHierarchy: OneToOneLinkToComplexHierarchyManager, SwappedToOne: OneToOneLinkManager, IsOneToManyLoaded: Boolean, ToMany: OneToManyRelationManager, ToManyToComplexHierarchy: OneToManyLinkToComplexHierarchyManager, SwappedToMany: OneToManyRelationManager, AnyReference: AnyReferenceLinkManager, SearchQuery: SearchQueryLinkManager, OneToOne: OneToOneLinkManager, OneToMany: OneToManyRelationManager
**Методы:**
- `OneToManyRelation FindToManyRelation(ParameterGroup group) (+1)`
- `OneToOneLink FindToOneLink(ParameterGroup group) (+1)`
- `OneToManyLinkToComplexHierarchy FindToManyToComplexHierarchyLink(ParameterGroup group) (+1)`
- `OneToOneLinkToComplexHierarchy FindToOneToComplexHierarchyLink(ParameterGroup group) (+1)`
- `SearchQueryLink FindSearchQueryLink(ParameterGroup group) (+1)`
- `Void Clear(Boolean full) (+1)`
- `Void Fill(LoadSettings settings, Boolean loadOnlyUnloadedRelations)` [has Async]

### `ReferenceObjectLinksExtensions`
**Методы:**
- `ReferenceObject GetStorageLinkedObject(DesktopObject desktopObject, Guid linkGuid) (+5)` [has Async]
- `Boolean TryGetStorageLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject& linkedObject) (+5)`
- `ICollection`1 GetStorageLinkedObjects(DesktopObject desktopObject, Guid linkGuid) (+3)` [has Async]
- `Boolean TryGetStorageLinkedObjects(DesktopObject desktopObject, Guid linkGuid, ICollection`1& objects) (+3)`
- `ReferenceObject SetStorageLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject newLinkedObject, Boolean appendInStorage) (+2)`
- `ReferenceObject AddStorageLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject newLinkedObject, Boolean appendInStorage) (+3)`
- `ICollection`1 AddStorageLinkedObjects(DesktopObject desktopObject, Guid linkGuid, ICollection`1 newLinkedObjects, Boolean appendInStorage) (+3)`
- `Boolean RemoveStorageLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject linkedObject) (+1)`
- `Void RemoveAllStorageLinkedObjects(DesktopObject desktopObject, Guid linkGuid) (+3)`
- `Void SetStaticReferences(LoadSettings settings, ICollection`1 ignoreLinks, StaticReferenceLoadSettings loadSettings) (+1)`

### `ReferenceObjectLockStateExtensions`
**Методы:**
- `String GetName(ReferenceObjectLockState state)`

### `ReferenceObjectParameters`
**Свойства:** Object: ReferenceObject

### `ReferenceObjectReminder`
**Свойства:** Object: Object

### `ReferenceObjectSaveSet`
**Свойства:** Changing: Boolean, Owner: ReferenceObject, ObjectsToDelete: ReadOnlyCollection`1, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Void AddRange(IEnumerable`1 collection)` [has Async]
- `Boolean Contains(ReferenceObject item)`
- `ReferenceObject Find(Int32 referenceId, Int32 objectId)`
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges(ReferenceObject referenceObject) (+2)` [has Async]
- `Void AddObjectToDelete(ReferenceObject referenceObject)`
- `Void AddObjectsToDelete(IEnumerable`1 referenceObjects)`
- `Void Add(ReferenceObject item)` [has Async]
- `Void CopyTo(ReferenceObject[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `ReferenceObjectSaveSetExtensions`
**Методы:**
- `T RunWithSaveSet(Func`2 operation, CancellationToken token) (+3)` [has Async]

### `ReferenceObjectSetAccessManager`
**Свойства:** Objects: IReadOnlyCollection`1
**Методы:**
- `Void SetInherit(Boolean inherit, Boolean copyInheritAccess)`
- `ReferenceObjectSetAccessManager GetReferenceObjectsAccess(IEnumerable`1 referenceObjects, AccessRightsLoadOptions options)` [has Async]

### `ReferenceObjectSystemFields`
**Свойства:** Id: Int32, Guid: Guid, AuthorName: String, AuthorId: Int32, Author: User, OwnerId: Int32, Owner: UserReferenceObject, OnBehalfOfId: Int32, OnBehalfOf: UserReferenceObject, CredentialId: Int32, Credential: CredentialsReferenceObject, CreationDate: DateTime, EditorName: String, EditorId: Int32, Editor: User, EditDate: DateTime, StageEditDate: DateTime, Version: Int32, Deleted: Boolean, ClientViewId: Int32, ClientView: ClientView, Order: Nullable`1, StageId: Int32, Stage: SchemeStage, IsLinkedToNomenclature: Boolean, LogicalObjectGuid: Guid, RevisionName: String, LastRevisionName: String, SourceRevisionName: String, IsActualRevision: Boolean, StartDate: Nullable`1, EndDate: Nullable`1, DesignContextId: Int32, OriginalId: Int32, DeletedInDesignContext: Boolean, ConflictWithOriginal: ConflictWithOriginal, MasterServerId: Int32, MasterServer: ReferenceObject, IsRevisionsContainer: Boolean, StructureTypeId: Int32, StructureType: StructureTypesReferenceObject, InstanceGroupGuid: Guid, InstanceMappingType: InstancesMappingType, InstanceSequenceNumbers: String, IsStandaloneProduct: Boolean

### `ReferenceObjectTerm`
**Свойства:** Path: ReferencePath, ParameterName: String, Operator: ComparisonOperator, AsReferenceObjectTerm: ReferenceObjectTerm, SkipUsingServerTermValue: Boolean
**Методы:**
- `Void Clear()`
- `Void ReplaceVariablesByValues()`
- `IReadOnlyCollection`1 GetAvailableOperators()`

### `ReferenceObjectValue`
**Свойства:** IsObject: Boolean, Object: ReferenceObject, Link: ComplexHierarchyLink

### `ReferenceObjectVariable`
**Свойства:** Type: Type

### `ReferenceObjectWithInstance`
**Свойства:** ReferenceObject: ReferenceObject, ObjectInstance: ReferenceObjectInstance

### `ReferenceObjectWithLink`
**Свойства:** Link: ComplexHierarchyLink

### `ReferenceObjectWithLink`
**Свойства:** ReferenceObject: ReferenceObject, Link: ComplexHierarchyLink, Signature: Signature

### `ReferencePath`
**Свойства:** MasterGroup: ParameterGroup, CurrentItem: PathItem, Item: PathItem, Count: Int32
**Методы:**
- `Boolean AddGroup(ParameterGroup group, Boolean throwOnError) (+1)`
- `Boolean AddGroupAt(ParameterGroup group, Int32 index, Boolean throwOnError) (+1)`
- `Boolean AddSwappedLink(ParameterGroup linkGroup, Boolean throwOnError) (+1)`
- `Boolean AddChildObjects(Boolean throwOnError) (+1)`
- `Boolean AddAllChildObjects(Boolean throwOnError) (+1)`
- `Boolean AddObjectRemarks(Boolean throwOnError)`
- `Boolean AddRevisions(Boolean throwOnError)`
- `Boolean AddBaseRepresentationObject(Boolean throwOnError)`
- `Boolean AddStructureTypes(Boolean throwOnError)`
- `Boolean AddStructureType(Boolean throwOnError)`
- `Boolean AddApplicability(Boolean throwOnError)`
- `Boolean AddStartProduct(Boolean throwOnError)`
- `Boolean AddEndProduct(Boolean throwOnError)`
- `Boolean AddAuthor(Boolean throwOnError)`
- `Boolean AddEditor(Boolean throwOnError)`
- `Boolean AddOwner(Boolean throwOnError)`
- `Boolean AddOnBehalfOf(Boolean throwOnError)`
- `Boolean AddCredential(Boolean throwOnError)`
- `Boolean AddMasterServer(Boolean throwOnError)`
- `Boolean AddLoadOptions(Boolean throwOnError)`
- `Boolean AddLoadOptionsParameter(LoadOptionsParameter parameter, Boolean throwOnError)`
- `Boolean AddConfigurationGroup(Boolean throwOnError)`
- `Boolean AddConfigurationParameter(ConfigurationParameter parameter, Boolean throwOnError)`
- `Boolean AddParentComplexHierarchyLinks(Boolean throwOnError) (+1)`
- `Boolean AddChildrenComplexHierarchyLinks(Boolean throwOnError) (+1)`
- `Boolean AddAllParentObjects(Boolean throwOnError) (+1)`
- `Boolean AddParameter(ParameterInfo parameter, Boolean throwOnError) (+1)`
- `Boolean AddSignature(SignatureType type, Boolean throwOnError) (+2)`
- `Boolean AddSignatureParameter(SignatureParameter parameter, Boolean throwOnError)`
- `Boolean AddFilePreviewImage(Int32 pageIndex, Boolean throwOnError)`
- `Boolean AddFileContent(Boolean throwOnError)`
- `Boolean AddNomenclatureObject(Boolean throwOnError)`
- `Boolean AddLinkedObject(Boolean throwOnError)`
- `Boolean AddMasterObject(Boolean throwOnError)`
- `Boolean AddParentObject(Boolean throwOnError)`
- `Boolean AddRootObject(Boolean thrownOnError)`
- `Boolean AddObjectStages(Boolean throwOnError)`
- `Boolean AddObjectStageParameter(ObjectStageParameter parameter, Boolean throwOnError)`
- `Boolean AddObjectInstancePathItem(Boolean throwOnError)`
- `Boolean AddCharacteristics(Boolean throwOnError)`
- `Boolean AddNamePathItem(Boolean throwOnError)`
- `Void RemoveLast()`
- `Void RemoveRange(Int32 index, Int32 count)`
- `Void SetPathToItem(PathItem item)`
- `ReferencePath CreatePathToItem(PathItem item)`
- `ReferencePath GetSubpath(ParameterGroup group)`
- `ReferencePath GetRelativePath(ReferencePath initialPath, Boolean throwOnError)`
- `Boolean IsOneToMany()`
- `Boolean ContainsInLoadSettings(LoadSettings loadSettings)`
- `LoadSettings AddToLoadSettings(LoadSettings loadSettings)`
- `String Serialize(ObjectSerializationMode mode, Boolean includeRootItem)`
- `Boolean IsSame(ReferencePath other)`
- `Int32 IndexOf(PathItem item)`
- `Void Add(PathItem item)`
- `Boolean TryAdd(PathItem item)`
- `Void Clear()`
- `Boolean Contains(PathItem item)`
- `Void CopyTo(PathItem[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`
- `ReferencePath Parse(String str, ServerConnection connection) (+1)`
- `Boolean TryParse(String str, ServerConnection connection, ReferencePath& path) (+1)`
- `ReferencePath CreateToReferenceGroup(ParameterGroup group) (+1)`

### `ReferencePathCache`
**Свойства:** Connection: ServerConnection
**Методы:**
- `Boolean TryParse(String str, ParameterGroup masterGroup, ReferencePath& path) (+1)`
- `Boolean TryParseAny(String str, ParameterGroup masterGroup, ReferencePath& path) (+1)`
- `Void Reset()`

### `ReferencePathElement`
**Свойства:** ReferenceGuid: Guid, PrototypeMode: Boolean
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean IsEqual(PathElement pathElement)`

### `ReferencePathExtensions`
**Методы:**
- `Boolean IsEmptyPath(ReferencePath path, Boolean skipParameterGroups) (+1)`
- `Boolean TryAddCopy(ReferencePath path, PathItem item)`
- `ReferencePath[] SplitPath(ReferencePath path, Func`2 predicate)`
- `ReferencePath[] TrySplitPath(ReferencePath path, Func`2 predicate) (+1)`
- `Int32 GetPathItemIndex(ReferencePath path, Func`2 predicate)`
- `ReferencePath ConcatPath(ReferencePath first, ReferencePath second)`
- `ReferencePath ReversePath(ReferencePath path)`
- `ParameterGroup GetOutputGroup(ReferencePath path)`
- `ReferencePath SubPath(ReferencePath source, Int32 start, Int32 count) (+1)`
- `ReferencePath TrimEndParameterGroup(ReferencePath path)`
- `ReferencePath MergeRepetitiveHierarchy(ReferencePath path)`
- `Boolean IsHierarchyOneToMany(ReferencePath path)`

### `ReferencePathExtensions`
**Методы:**
- `String GetGuidStringToPathItem(GroupPathItem linkPathItem) (+1)`

### `ReferenceRestrictiveListClassGroupSettings`
**Свойства:** ReferencesUseType: ItemListUseType, Except: List`1
**Методы:**
- `Void Deserialize(String data)`
- `String Serialize()`

### `ReferencesStorage`
**Свойства:** Guid: Guid, Connection: ServerConnection, Settings: ReferencesStorageSettings, IgnoreRefreshReferences: HashSet`1, IsDisposed: Boolean, Item: Object
**Методы:**
- `Reference Get(Int32 referenceId, Boolean throwOnError) (+4)` [has Async]
- `TReferenceObject Append(TReferenceObject referenceObject, Boolean throwOnError, Boolean skipChangingObjectCheck) (+1)`
- `IReadOnlyCollection`1 AppendReadOnly(IReadOnlyCollection`1 referenceObjects, Boolean throwOnError)`
- `Reference Find(Int32 referenceId) (+2)`
- `Void Refresh()`
- `Void ClearLoadedObjects()`
- `Void Clear(Int32 referenceId) (+3)`
- `Boolean ChangeSettings(ReferencesStorageSettings settings)`

### `ReferencesStorageExtension`
**Методы:**
- `ReferencesStorage GetOrCreateStorage(Reference reference)`

### `ReferencesStorageExtensions`
**Методы:**
- `ReferenceObject GetLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferencesStorage storage, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData) (+2)`
- `Boolean TryGetLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject& linkedObject, ReferencesStorage storage, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData) (+1)`
- `List`1 GetLinkedObjects(DesktopObject desktopObject, Guid linkGuid, ReferencesStorage storage, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData) (+1)`
- `Boolean TryGetLinkedObjects(DesktopObject desktopObject, Guid linkGuid, List`1& objects, ReferencesStorage storage, StaticReferenceLoadSettings loadSettings, Boolean onlyLoadedData)`
- `ReferenceObject SetLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject newLinkedObject, ReferencesStorage storage, Boolean appendInStorage) (+2)`
- `ReferenceObject AddLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject newLinkedObject, ReferencesStorage storage, Boolean appendInStorage) (+5)`
- `List`1 AddLinkedObjectReadOnly(DesktopObject desktopObject, ParameterGroup linkGroup, IReadOnlyCollection`1 newLinkedObjects, ReferencesStorage storage, Boolean appendInStorage)`
- `List`1 AddLinkedObjects(OneToManyLink link, ICollection`1 newLinkedObjects, ReferencesStorage storage, Boolean appendInStorage) (+1)`
- `List`1 AddLinkedObjectsReadOnly(OneToManyLink link, IReadOnlyCollection`1 newLinkedObjects, ReferencesStorage storage, Boolean appendInStorage) (+1)`
- `Boolean RemoveLinkedObject(DesktopObject desktopObject, Guid linkGuid, ReferenceObject linkedObject, ReferencesStorage storage) (+1)`
- `Void RemoveAllLinkedObjects(DesktopObject desktopObject, Guid linkGuid, ReferencesStorage storage) (+3)`
- `Void SetStaticReferences(LoadSettings settings, ReferencesStorage storage, ICollection`1 ignoreLinks, Nullable`1 loadSettings, Boolean useRootConfigurationSettings) (+1)`
- `Boolean ContainsStaticReferenceInAllRelations(LoadSettings settings)`
- `ReferencesStorage FindStorageInReference(Reference reference)`
- `TReference GetIndependentReference(TReference reference)`

### `ReferencesStorageSettings`
**Свойства:** Bind: Boolean, CanRefreshReference: Boolean, CanRefreshStaticReference: Boolean, CanRefreshReferenceCatalog: Boolean, CheckHierarchyWhenChanging: Boolean, OnReferenceAppending: Action`1, InitAllParametersWhenCreate: Boolean, CanCreateNewInstanceForStaticReference: Boolean

### `ReferenceStageArrayVariable`
**Свойства:** Type: Type, IsArray: Boolean

### `ReferenceStageVariable`
**Свойства:** Type: Type

### `ReferenceTrigger`
**Свойства:** Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `ReferenceUserArrayVariable`
**Свойства:** ReferenceGuid: Guid, Type: Type

### `ReferenceUserVariable`
**Свойства:** ReferenceGuid: Guid, Type: Type

### `ReferenceVariable`
**Свойства:** AllowNullValue: Boolean, IsNull: Boolean, ReferenceGuid: Guid
**Методы:**
- `Void SetDefaultValue()`

### `ReferenceVariableManager`
**Свойства:** ReferenceVariableTypeCollection: IReadOnlyList`1, SupportedTypes: HashSet`1
**Методы:**
- `Type GetVariableType(Type parameterType, Boolean isArray)`

### `ReferenceVisibilityExtensions`
**Методы:**
- `String GetName(ReferenceVisibility visibility)`

### `ReferenceWithFilterObject`
**Свойства:** ReferenceInfo: ReferenceInfo, ReferenceGuid: Guid, Filter: Filter

### `RefObj`
**Методы:**
- `RefObj CreateInstance(ReferenceObject object, MacroContext context, ComplexHierarchyLink hierarchyLink) (+1)`

### `RefObjInstance`
**Методы:**
- `RefObjInstance CreateInstance(ReferenceObjectInstance object, MacroContext context)`

### `RefObjList`
**Методы:**
- `RefObjList CreateInstance(IEnumerable`1 objects, MacroContext context)`
- `RefObjList Match(String filter)`
- `RefObjList SelectTopLevelObjectsFromList()`

### `RegisterPathType`
**Свойства:** Key: String, ParseFunc: Func`2

### `RegularTimeTrigger`
**Свойства:** Interval: TimeSpan, Ticks: Int64, Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `RelationExtensions`
**Методы:**
- `String GetRelationObjectsVisualization(RelationTree relationTree, Guid[] objectParameters) (+1)`
- `Void AddParentsRecursiveLoad(RelationLoadSettings loadSettings)`
- `Void AddChildrenRecursiveLoad(RelationLoadSettings loadSettings)`
- `Void AddParentOneLevelLoad(RelationLoadSettings loadSettings)`
- `Void AddChildrenOneLevelLoad(RelationLoadSettings loadSettings)`
- `Void AddRecursiveLoad(RelationLoadSettings loadSettings, RecursiveLoadDirection loadDirection)`
- `Void AddNonRecursiveLoad(RelationLoadSettings loadSettings, RecursiveLoadDirection loadDirection)`
- `String GetVisualization(LoadSettings loadSettings)`
- `IEnumerable`1 GetAllObjects(ReferenceObject mainReferenceObject, ParameterGroup linkGroup)` [has Async]
- `String GetLoadedObjectLinksVisualization(ReferenceObject referenceObject, ReferencesStorage storage) (+1)`

### `RelationLoadSettings`
**Свойства:** Owner: LoadSettings, Relation: ParameterGroup, Load: Boolean, LoadHierarchy: Boolean, ConfigurationSettings: ConfigurationSettings, LoadHasChildren: Boolean, StaticReference: Reference, StaticReferenceSettings: StaticReferenceLoadSettings, Filter: Filter, RecursiveLoadHierarchy: RecursiveLoadDirection
**Методы:**
- `Void TakeStaticReference()`

### `RelationManager`1`
**Свойства:** Owner: ReferenceObject, OwnerHierarchyLink: ComplexHierarchyLink, LinkGroups: ParameterGroupCollection, IsModified: Boolean, Item: T, Item: T, Item: T
**Методы:**
- `T Find(ParameterGroup linkGroup) (+2)`
- `Void ReloadAll()`
- `IEnumerator`1 GetEnumerator()`

### `RelationRule`
**Свойства:** Guid: Guid
**Методы:**
- `Void Add(ComparisonRuleBase comparisonRule)`
- `Void Remove(ComparisonRuleBase comparisonRule)`
- `IObjectsComparisonNode Run(IObjectNode left, IObjectNode right)`
- `ParameterGroup FindParameterGroup(ParameterGroup mainGroup)`

### `RelationTableFormulaMacro`
**Свойства:** CodeOffset: Int32

### `RelationTableMacroContext`
**Свойства:** Column: ReferenceObject, Row: ReferenceObject

### `RelationTableMacroProvider`
**Свойства:** Context: RelationTableMacroContext, ColumnObject: RefObj, RowObject: RefObj

### `RelationTree`
**Свойства:** Mode: LoadingMode, RootObject: ReferenceObject, RootObjects: ReadOnlyCollection`1, RootHierarchyLink: ComplexHierarchyLink, RootHierarchyLinks: ReadOnlyCollection`1, Relations: ReadOnlyCollection`1, SetObjectsInLinks: Boolean, LoadOnlyUnloadedRelations: Boolean, FilterContext: MacroContext
**Методы:**
- `ReadOnlyCollection`1 Fill(IEnumerable`1 rootObjects, LoadSettings settings, Boolean setObjectsInLinks, Boolean loadOnlyUnloadedRelations, MacroContext filterContext) (+2)` [has Async]
- `ReadOnlyCollection`1 Load(DesktopObject rootObject, LoadSettings settings, Boolean setObjectsInLinks, Boolean loadOnlyUnloadedRelations, RecursiveLoadDirection loadDirection, MacroContext filterContext) (+2)` [has Async]
- `Void LoadParameters(IEnumerable`1 rootObjects, IReadOnlyCollection`1 parameterIds) (+2)` [has Async]

### `ReloadLicenseKeyResult`
**Свойства:** Success: Boolean, Message: String

### `RemarkContext`
**Свойства:** ReferenceGuid: Guid, ReferenceObjectGuid: Guid, ReferenceObjectVersion: Int32, XmlData: String, BinaryData: Byte[]

### `RemarkReferenceObject`
**Свойства:** Text: StringParameter, Status: Int32Parameter, Importance: Int32Parameter, ClosingDate: DateTimeParameter, ClosingAuthor: StringParameter, ClosingComment: StringParameter, Class: RemarkType, Dependencies: ReferenceObjectCollection, StatusType: RemarkStatus
**Методы:**
- `Int32 GetReferenceObjectVersion(Guid referenceObject)`
- `ReferenceObject AddDependency(ReferenceObject newLinkedObject)`
- `Boolean RemoveDependency(ReferenceObject linkedObject)`
- `ICollection`1 FindDependencies(ReferenceObject referenceObject)`

### `RemarksReference`
**Свойства:** Classes: RemarkTypes, Context: RemarkContext
**Методы:**
- `List`1 FindRemarks(ReferenceObject referenceObject, Filter filter) (+1)` [has Async]
- `IReadOnlyCollection`1 FindRequestRemarkObjects(ReferenceObject referenceObject)`
- `RemarkReferenceObject AddPdfRemark(Guid reference, Guid referenceObject, String text, String xmlData, RequestRemarkObject requestRemark) (+1)`
- `RemarkReferenceObject AddImageRemark(Guid reference, Guid referenceObject, String text, String xmlData, RequestRemarkObject requestRemark) (+1)`
- `RemarkReferenceObject AddCadRemark(Guid reference, Guid referenceObject, String text, Byte[] binaryData, RequestRemarkObject requestRemark) (+1)`
- `RemarkReferenceObject AddTextRemark(Guid reference, Guid referenceObject, String text, RequestRemarkObject requestRemark) (+1)`
- `RemarkReferenceObject AddRequestRemark(Guid reference, Guid referenceObject, String text, RequestRemarkObject requestRemark) (+1)`

### `RemarkType`
**Свойства:** Classes: RemarkTypes, IsPdfRemark: Boolean, IsTextRemark: Boolean, IsCadRemark: Boolean, IsRequestRemark: Boolean, IsImageRemark: Boolean

### `RemarkTypes`
**Свойства:** PdfRemark: RemarkType, TextRemark: RemarkType, CadRemark: RemarkType, RequestRemark: RemarkType, ImageRemark: RemarkType

### `Reminder`
**Свойства:** Connection: ServerConnection, Id: Int32, IsNew: Boolean, Date: DateTime, Text: String, Object: Object
**Методы:**
- `Void Save()`
- `Boolean Delete()` [has Async]

### `ReminderAppointment`
**Методы:**
- `Object GetCoreObject()`
- `Void Release()`
- `Boolean IsEqual(Reminder reminder)`

### `ReminderManager`
**Свойства:** Reminders: List`1, RemindersToShow: List`1
**Методы:**
- `ReferenceObjectReminder GetReminder(ReferenceObject refObj) (+1)`
- `Void WaitRemindThread(Object state)`

### `RemoveFromCollectionActivity`1`
**Свойства:** Values: InArgument`1, Item: InArgument`1, IsIndex: InArgument`1, Index: InArgument`1

### `ReplaceActionReferenceObject`
**Свойства:** NewObject: NomenclatureReferenceObject

### `ReplaceFileEditActionReferenceObject`
**Свойства:** IsAutomatic: Boolean, DestinationFile: FileObject, SourceFile: FileObject

### `Report`
**Свойства:** ReportFileName: StringParameter, OutputFileFormat: StringParameter, ReportResultProcessingFormula: StringParameter, DefaultFolder: FolderObject, AutoAttachLink: GuidParameter, MethodExtraLoading: StringParameter, UserDialog: UserDialogObject, MacroExtraLoading: CodeMacro, HasTemplateProperties: Boolean, TemplateProperties: ByteArrayParameter, AllowCustomizeDesign: Boolean
**Методы:**
- `Void EditTemplateProperties(IWin32Window owner)`
- `Void CustomizeDesign(IntPtr owner)`
- `Boolean ValidateMacroExtraLoading(Macro macro, String method, Boolean throwOnError)`
- `Boolean ValidateLicense(Boolean throwOnError)`
- `ReportGenerationContext Generate(ReferenceObject obj, ComplexHierarchyLink link, ReferenceObject resultFileOwner, ParameterGroup fileLink) (+5)`
- `Void InitializeContext(ReportGenerationContext context, Boolean generating)`

### `ReportAccessor`
**Свойства:** OpenFile: Boolean [RU: ОткрытьФайл], OpenFileInTab: Boolean [RU: ОткрытьФайл], ReportFolderPath: String [RU: ПутьКПапке], ReportFileName: String [RU: ПутьКПапке], UserDialog: UserDialogObj, ПользовательскийДиалог: ПользовательскийДиалог [RU only]
**Методы:**
- `ReportResult Generate(RefObj refObj) (+2)` [RU: Сформировать]
- `Object GetRealValue()` [RU: Сформировать]

### `ReportConfigurationSettingsData`
**Свойства:** TypicalConfiguration: Guid, Product: Guid, DesignContext: Guid, ApplyStructureType: Boolean, ActiveStructureTypeGuid: Guid, ActiveStructureTypes: List`1, DisplayStructureTypes: List`1, ShowBaseStructure: Boolean, StatusesDate: String, ShowEmptyCategories: Boolean, ShowAllCategories: Boolean, ShowDeletedInDesignContextLinks: Boolean, ApplyProductFilter: Boolean, ApplyCategoriesFilter: Boolean, ApplyTerms: Boolean, ApplyDate: Boolean, ApplyDesignContext: Boolean, ApplyOptionValues: Boolean, ApplyProductDesignNumber: Boolean, ApplyProductMilestoneNumber: Boolean, ProductCategories: List`1, SelectRevisionsTermsObject: Guid, SelectRevisionsTerms: FilterDataCollection, ProductMilestoneNumber: Nullable`1, ProductDesignNumber: Nullable`1, SerialNumberGuid: Guid, OptionValues: List`1, CustomCriteriaValueData: CustomCriteriaValueData
**Методы:**
- `String Serialize(ServerConnection connection, ConfigurationSettings configurationSettings)`
- `ConfigurationSettings Deserialize(ServerConnection connection, String contextData)`

### `ReportFormulaMacro`
**Свойства:** CodeOffset: Int32

### `ReportGenerationContext`
**Свойства:** PathToParameterGroup: String, IsPreview: Boolean, IsPreviewSaving: Boolean, ReportId: Int32, RootObjectId: Int32, ParameterGroup: ParameterGroup, Reference: Reference, Objects: List`1, UserDialogTypeGuid: Guid, UserDialog: UserDialogObject, ContentFilter: Filter, ReportFolderPath: String, ReportFileName: String, ReportGenerationCode: String, DebugMode: Boolean, ReportGenerationCodeReferences: String, GenerationErrors: String, SetOfReportFilePaths: List`1, RequiredParametersExceptionCallback: Func`2, OverwriteReportFile: Nullable`1, OpenFile: Nullable`1, MacroContext: ReportMacroContext, ReferenceId: Int32, ObjectsInfo: List`1, ObjectPositions: List`1, RefreshPositons: Boolean, ContentType: ReportContentType, UpdateOutputDocument: Boolean, AuthorInfo: IAuthorInfo, ReportFilePath: String, TemplateFilePath: String, DefaultFolderObject: FolderObject, ReportFileObject: FileReferenceObject, DefaultFolder: String, UserName: String, Password: String, Server: String, WindowsAuthentication: Boolean, ConnectionParametersData: String, TemplateProperties: Byte[], ProductStructureId: Int32, GeneratorProgramFilePath: String, ReportDataSetReader: IReportDataSetReader, SetOfReportsParameters: List`1, TotalPages: Int32, PagesNumerationInfo: PageNumerationInfoCollection, MacroExtraLoading: ValueTuple`2
**Методы:**
- `Dictionary`2 GetLinksWithNewPositions()`
- `Void CopyTemplateFile()`
- `Void CopyFrom(IReportGenerationContext context)`
- `Byte[] Serialize(IReportGenerationContext context)`
- `IReportGenerationContext Deserialize(Byte[] contextData)`

### `ReportGenerationContextFactory`
**Методы:**
- `ReportGenerationContext CreateContext(ReferenceObject referenceObject, ComplexHierarchyLink link, ReportContentType contentType) (+4)`

### `ReportGenerationContextWithConfigurationSettings`
**Свойства:** ConfigurationSettingsInfo: String, Reference: Reference
**Методы:**
- `Void CopyFrom(IReportGenerationContext context)`

### `ReportGenerationResult`
**Свойства:** ReportFilePath: String, GenerationErrors: String, ReportFileObject: FileReferenceObject

### `ReportGenerationResultFormulaCreator`
**Методы:**
- `FormulaMacro CreateFormula(String formula)`

### `ReportGenerationResultFormulaMacro`
**Свойства:** IsReturnValue: Boolean, CodeOffset: Int32

### `ReportGenerationResultMacroContext`
**Свойства:** ReportGenerationResult: ReportGenerationResult

### `ReportGenerationResultMacroProvider`
**Свойства:** Context: ReportGenerationResultMacroContext, ReportResult: ReportResult, РезультатОтчёта: РезультатОтчёта [RU only]

### `ReportGenerator`
**Свойства:** Name: StringParameter, ModuleName: StringParameter, GeneratorClassName: StringParameter, SupportsTemplateProperties: BooleanParameter, CustomizableDesign: BooleanParameter, StandAlone: BooleanParameter, RefreshPositions: BooleanParameter, OperationTimeout: Int32Parameter
**Методы:**
- `IEnumerable`1 GetCommands()`
- `IReportGenerator CreateGenerator(Boolean forGeneration)`

### `ReportGeneratorCommand`
**Свойства:** Name: StringParameter, Identifier: StringParameter, Icon: IconParameter

### `ReportGeneratorProxy`
**Свойства:** DefaultReportFileExtension: String
**Методы:**
- `Void Generate(IReportGenerationContext context)`
- `Boolean EditTemplateProperties(Byte[]& data, IReportGenerationContext context, IWin32Window owner)`

### `ReportKitDocument`
**Свойства:** Name: StringParameter, Report: OutputDocument
**Методы:**
- `Filter GetFilter()`

### `ReportMacro`
**Свойства:** CodeOffset: Int32

### `ReportMacroContext`
**Свойства:** Signature: Signature, ObjectsIds: Int32[], ReferenceId: Int32, ReportId: Int32, ContentType: ReportContentType, ReportFilePath: String, TemplateFilePath: String, AuthorFullName: String, AuthorFirstName: String, AuthorLastName: String, AuthorPatronymic: String, AuthorShortName: String, UserName: String, Server: String, WindowsAuthentication: Boolean, RefreshPositons: Boolean, UserDialog: UserDialogObject
**Методы:**
- `Object GetValue(Int32 objectId, String parameter)`
- `String GetString(Int32 objectId, String parameter)`
- `List`1 GetKitParameters()`

### `ReportMacroParameterAccessor`
**Свойства:** Item: DynamicType

### `ReportMacroProvider`
**Свойства:** Context: ReportMacroContext, CurrentSignature: SignatureObj, KitParameter: ReportMacroParameterAccessor [RU: ПараметрКомплекта], ТекущаяПодпись: Подпись [RU only]

### `ReportMacroProviderAccessorExtensions`
**Методы:**
- `SignatureAccessor GetCurrentSignature(ReportMacroProvider macroProvider)`

### `ReportPreviewContext`
**Свойства:** IsPreview: Boolean, FilePath: String, Parameters: String, ShowToolsButtons: Boolean, LinkedObjectId: Int32, LinkedReferenceId: Int32, AsyncModeSupported: Boolean, LinkedObjectGuid: Guid, EnablePrint: Boolean, ConfigurationSettings: String, CustomFilePreviewerGuid: Guid, DefaultFilePreviewerGuid: Guid, ObjectContext: String, LastModificationTime: DateTime, CanEditDocument: Boolean, FileExtension: String, HierarchyLink: Guid
**Методы:**
- `Void GenerateFile()`
- `Boolean IsChanged(IFilePreviewContext filePreviewContext)`

### `ReportPreviewContextWithConfigurationSettings`
**Свойства:** ConfigurationSettingsInfo: String, Reference: Reference
**Методы:**
- `Void CopyFrom(IReportGenerationContext context)`

### `ReportReference`
**Методы:**
- `OutputDocument FindByTemplate(FileObject template)`

### `ReportReferenceAccessor`
**Методы:**
- `ReportRef Find(String name, String referenceName)` [RU: Найти]
- `Object GetRealValue()`

### `ReportResultAccessor`
**Свойства:** ReportFilePath: String [RU: ПутьКФайлу], ReportFile: RefObj, HasErrors: Boolean [RU: СодержитОшибки], ErrorsDescription: String [RU: ПутьКФайлу], ФайлОтчёта: Объект [RU only]
**Методы:**
- `Object GetRealValue()`

### `ReportType`
**Свойства:** Classes: ReportTypes, IsReport: Boolean, IsSetOfReports: Boolean

### `RepositoryBaseEditItemXMLData`
**Свойства:** ReferenceGuid: Guid, Filter: Filter

### `RepositoryBooleanListItemXMLData`
**Свойства:** Yes: String, No: String

### `RepositoryExtendedHtmlEditXMLData`
**Свойства:** UseInteractiveLinks: Boolean

### `RepositoryExtendedRtfEditXMLData`
**Свойства:** UseInteractiveLinks: Boolean

### `RepositoryGuidEditItemXMLData`
**Свойства:** PathToParameterContainingReferenceId: String, PrototypeMode: Boolean, PathToParameterContainingClassId: String

### `RepositoryItemExpressionEditXMLData`
**Свойства:** LinkGuid: String, ParameterNameGuid: String, ParameterDescriptionGuid: String

### `RepositoryItemListFromLinkEditXMLData`
**Свойства:** LinkGuid: String, LinkObjectsGuid: String, ParameterNameGuid: String, ParameterValueGuid: String, IsEditable: Boolean

### `RepositoryItemTimeSpanEditXMLData`
**Свойства:** ShowDays: Boolean, ShowHours: Boolean, ShowMinutes: Boolean, ShowSeconds: Boolean, AllowNegative: Boolean

### `RepositoryItemUniversalPathEditXMLData`
**Свойства:** AllowUserChangeInputType: Boolean, InputType: String

### `RepositoryRichTextEditXMLData`
**Свойства:** LineSpacingInterval: Nullable`1

### `RepositoryRtfEditXMLData`
**Свойства:** LineSpacingInterval: Nullable`1

### `RepositoryTextWithHintsEditXMLData`
**Свойства:** HintsMode: Boolean

### `RequestErrorHandler`
**Методы:**
- `Boolean Invoke(IRequestResultError error)`
- `IAsyncResult BeginInvoke(IRequestResultError error, AsyncCallback callback, Object object)`
- `Boolean EndInvoke(IAsyncResult result)`

### `RequestRemarkObject`
**Свойства:** Performers: ReferenceObjectCollection
**Методы:**
- `ReferenceObject AddPerformer(ReferenceObject newLinkedObject)`
- `Boolean RemovePerformer(ReferenceObject linkedObject)`

### `RequestResult`
**Свойства:** Error: InternalErrorData
**Методы:**
- `Void SetError(Exception exception)`
- `Boolean IsNullOrFaulted(RequestResult result)`

### `RequestResult`1`
**Свойства:** Value: T

### `RequirementsDictionaryReferenceObject`
**Свойства:** Class: TechnicalRequirementsDictionaryType, Name: StringParameter, Text: StringParameter, Number: Int32Parameter, TechnicalCADData: ByteArrayParameter

### `ResolutionMailData`
**Свойства:** CheckStatus: Int32, ResponsibleGuid: Guid, Responsible: User, Comment: String

### `ResolutionTaskAccessor`
**Свойства:** Responsible: UserRefObj, Comment: String [RU: Комментарий], Ответственный: Пользователь [RU only]

### `ResolutionTaskObj`
**Методы:**
- `ResolutionTaskObj CreateInstance(MailResolution mailTask, MacroContext context)`

### `ResourceLinkComputingParameter`
**Методы:**
- `Void ForceSetValue(Object value)`

### `ResourceLinkReference`
**Свойства:** Classes: ResourceLinkTypes

### `ResourceLinkReferenceObject`
**Свойства:** Resource: ResourceReferenceObject, Quantity: Double, Value: Double, SpendingValueType: Int32, BaseTask: BaseTaskObject
**Методы:**
- `Void UpdateValue()`

### `ResourceLinkType`
**Свойства:** Classes: ResourceLinkTypes, IsBaseResource: Boolean, IsLabourResource: Boolean, IsMaterialResource: Boolean, IsSpendingResource: Boolean

### `ResourceReference`
**Свойства:** Classes: ResourceTypes

### `ResourceReferenceObject`
**Свойства:** Name: String

### `ResourceType`
**Свойства:** Classes: ResourceTypes, IsBaseResource: Boolean, IsLabourResource: Boolean, IsMaterialResource: Boolean, IsSpending: Boolean

### `ResponsibleMailResolutionField`
**Методы:**
- `List`1 GetComparisonOperators()`

### `RestRequest`
**Свойства:** Id: String, Data: String, Format: String

### `RestRequestData`
**Свойства:** Id: String, Data: String, Format: String

### `RestResponse`
**Свойства:** Data: String, Format: String, ResponseStatus: RestResponseStatus

### `RestResponseData`
**Свойства:** Data: String, Format: String, ResponseStatus: RestResponseStatus

### `RevisionLevelObject`
**Свойства:** RegexTemplate: String, Class: RevisionLevelsType, Name: StringParameter, FirstValue: StringParameter, Format: StringParameter, Icon: IconParameter
**Методы:**
- `String GetNextValue(String previousValue)`
- `Int32 Compare(String x, String y)`
- `Boolean CanChangeParameter(Parameter p, Object newValue)`

### `RevisionLevelsReference`
**Свойства:** Classes: RevisionLevelsTypes

### `RevisionLevelsType`
**Свойства:** Classes: RevisionLevelsTypes, IsAlphabeticRevisionLevel: Boolean, IsNumericRevisionLevel: Boolean

### `RevisionLevelsTypes`
**Свойства:** AlphabeticRevisionLevel: RevisionLevelsType, NumericRevisionLevel: RevisionLevelsType

### `RevisionNamingRuleObject`
**Свойства:** Class: RevisionNamingRulesType, Name: StringParameter, Template: StringParameter, FirstRevisionName: StringParameter, RevisionLevels: ReferenceObjectCollection`1
**Методы:**
- `String GetFirstRevisionName()`
- `String GetNewRevisionName(List`1 existingRevisionNames, String baseRevisionName, RevisionLevelObject forLevel)`
- `String GetLastRevisionName(List`1 existingNames)`
- `List`1 SortRevisionNames(List`1 revisionNames)`
- `Void RenameExistingRevisions(RevisionNamingRuleObject oldRule, Int32 referenceId, Int32 classObjectId)` [has Async]
- `RevisionLevelObject CreateRevisionLevel(Guid listObjectClass) (+1)`

### `RevisionNamingRulesReference`
**Свойства:** DefaultRevisionNamingRule: RevisionNamingRuleObject, Classes: RevisionNamingRulesTypes

### `RevisionNamingRulesType`
**Свойства:** Classes: RevisionNamingRulesTypes, IsRule: Boolean

### `RevisionNamingRulesTypes`
**Свойства:** Rule: RevisionNamingRulesType

### `RevisionsPathItem`
**Свойства:** Name: String, Icon: IconImage, Type: PathItemType, SupportSearchType: SupportSearchTypes

### `RootObjectPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `SaveFileDialog`
**Свойства:** Caption: String, InitialDirectory: String, FilterIndex: Int32, Filter: String, FileNames: String[], FileName: String, ValidateNames: Boolean, AddExtension: Boolean, DefaultExt: String, CreatePrompt: Boolean, OverwritePrompt: Boolean
**Методы:**
- `Stream OpenFile()`
- `Boolean Show()`

### `SaveSetEditSession`
**Методы:**
- `Void Add(ReferenceObject referenceObject)`
- `Boolean EndChanges()`
- `Void CancelChanges()`

### `Scheme`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, Name: String, Comment: String, Stages: ReadOnlyCollection`1, Changing: Boolean
**Методы:**
- `SchemeStage AddStage(Stage stage)`
- `Void BeginChanges()`
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges()`
- `Boolean Delete()` [has Async]
- `List`1 GetSchemes(ServerConnection connection) (+1)` [has Async]

### `SchemeStage`
**Свойства:** Id: Int32, Guid: Guid, Scheme: Scheme, Stage: Stage, IsAdded: Boolean, IsDeleted: Boolean, Transitions: ReadOnlyCollection`1
**Методы:**
- `List`1 GetNextStages()`
- `SchemeStageTransition AddTransition(SchemeStage stage, Boolean isAutomatic, Boolean isManual)`
- `Void Delete()`
- `IEnumerator`1 GetEnumerator()`

### `SchemeStageTransition`
**Свойства:** FromStage: SchemeStage, ToStage: SchemeStage, IsAutomatic: Boolean, IsManual: Boolean, IsAdded: Boolean, IsDeleted: Boolean
**Методы:**
- `Void Delete()`

### `SearchAssignmentFolderReferenceObject`
**Свойства:** Objects: ReferenceObjectCollection, Filter: StringParameter, ParamSearchFolder: StringParameter, IsCreatedByParameter: BooleanParameter, IsAutoCreated: Boolean
**Методы:**
- `Filter GetSearchFilter()`

### `SearchFolder`
**Свойства:** AsSearchFolder: SearchFolder, ParameterSearchFolder: String, IsCreatedByParameter: Boolean
**Методы:**
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `Filter GetSearchFilter()`

### `SearchQuery`
**Свойства:** Id: Int32, Guid: Guid, Folder: SearchQueryFolder, Name: String, IsPrivate: Boolean, IsAdded: Boolean, IsModified: Boolean
**Методы:**
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `ReferencePathCollection GetOutput()`
- `Void SetOutput(ReferencePathCollection output)`
- `Boolean Save()`
- `Boolean Delete()`
- `Int32 CompareTo(SearchQuery other)`

### `SearchQueryFolder`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, IsPrivate: Boolean, ParentFolder: SearchQueryFolder, Folders: ReadOnlyCollection`1, Queries: ReadOnlyCollection`1, Name: String, IsAdded: Boolean, IsModified: Boolean
**Методы:**
- `List`1 GetRootFolders(ServerConnection connection)`
- `Boolean Save()`
- `Boolean Delete()`

### `SearchQueryLink`
**Свойства:** Filter: Filter, PathToFilter: ReferencePath, Objects: ReferenceObjectCollection, IsSearchQueryLink: Boolean, LinkReference: Reference, IsLinkedReferenceInitialized: Boolean, IsEmptyLinkedObjects: Boolean, IsModified: Boolean, IsLoaded: Boolean, State: LoadState, CountLoaded: Int32, IsLinkedObjectIdsLoaded: Boolean, IsEmptyLinkedObjectsId: Boolean
**Методы:**
- `IEnumerable`1 GetLinkedObjects()` [has Async]
- `Boolean IsObjectAdded(ReferenceObject object)`
- `Boolean IsObjectRemoved(ReferenceObject object)`

### `SearchQueryLinkManager`
**Свойства:** LinkGroups: ParameterGroupCollection

### `SearchQueryObject`
**Свойства:** ResultParameters: ReferencePathCollection, Filter: Filter, MainReference: ReferenceInfo

### `SearchQueryReference`
**Свойства:** PrivateFolder: SearchQueryFolderObject, CommonFolder: SearchQueryFolderObject, Classes: SearchQueryTypes, IsAvailable: Boolean
**Методы:**
- `List`1 FindReferenceFilters(Guid referenceId) (+2)` [has Async]
- `SearchQueryReferenceObject Find(String name)` [has Async]

### `SearchQueryReferenceObject`
**Свойства:** Class: SearchQueryType, Caption: StringParameter

### `SearchQueryType`
**Свойства:** Classes: SearchQueryTypes, IsQuery: Boolean, IsFilter: Boolean, IsFolder: Boolean, IsFiltersGroup: Boolean

### `SearchQueryTypes`
**Свойства:** Instance: SearchQueryTypes, Folder: SearchQueryType, Query: SearchQueryType, Filter: SearchQueryType, FiltersGroup: SearchQueryType

### `SearchRule`
**Свойства:** Owner: TermGroupItem, Value: Object

### `SearchTerm`
**Свойства:** Parameter: String, Operator: String, Value: String
**Методы:**
- `Filter ToFilter(ReferenceInfo reference)`
- `IEnumerable`1 Parse(String value)`

### `SearchTermList`1`
**Свойства:** Item: T, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Boolean Remove(T item)`
- `Void RemoveAt(Int32 index)`
- `Filter ToFilter(ReferenceInfo reference)`

### `SearchTerms`
**Методы:**
- `SearchTerms CreateInstance(IEnumerable`1 terms)`

### `SecondaryRepresentationReferenceObject`
**Свойства:** LOD: Int32Parameter, FileExportParameters: ConversionFormatReferenceObject, AutoGenerationRepresentation: BooleanParameter, Disable: BooleanParameter, ConversionModule: FileConversionModuleReferenceObject

### `SecondaryRepresentationTaskReferenceObject`
**Свойства:** SecondaryRepresentationTemplate: GuidParameter

### `SelectCatalogFolderGuidControlXMLData`
**Свойства:** ReferenceGuid: String, CatalogGuid: String
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `SelectClassObjectsDialogAccessor`1`
**Свойства:** Caption: String, SelectedClasses: T[], AllowedClasses: T[], SelectAbstractClasses: Boolean, CheckboxesAutoSelection: Boolean, CheckboxSelection: Boolean
**Методы:**
- `Boolean Show()`

### `SelectFromListFieldInputDialog`
**Свойства:** TypeName: String, DefaultValue: InArgument`1, Values: InArgument`1

### `SelectFromReferenceFieldInputDialog`
**Свойства:** TypeName: String, Reference: InArgument`1, Parameter: InArgument`1, DefaultValue: InArgument`1, Filter: InArgument`1, Code: InArgument`1

### `SelectListObjectsDialog`
**Методы:**
- `Void AddColumn(String name, Func`2 calculateValue)`

### `SelectListObjectsDialogAccessor`2`
**Свойства:** Caption: String, AllowOrderResult: Boolean, ShowSearchPanel: Boolean, HideDefaultColumns: Boolean, MirrorDialog: Boolean, ListObjects: TList, SelectedObjects: TList
**Методы:**
- `Boolean Show()`
- `Void AddColumn(String name, Func`2 calculateValue)`

### `SelectObjectCommand`
**Свойства:** Objects: List`1
**Методы:**
- `Void Accept(ICommandVisitor visitor)`

### `SelectObjectDialogAccessor`4`
**Свойства:** MultipleSelect: Boolean, Filter: String, CheckboxSelection: Boolean, CheckboxesAutoSelection: Boolean, SelectedHierarchyLinks: HList, FocusedObject: T, SelectedObjects: TList, FocusedHierarchyLink: H, RootObject: T, Caption: String, View: String, Catalog: String, CatalogFolder: String, ShowToolbar: Boolean, PrototypeMode: Boolean, IsReadOnly: Boolean
**Методы:**
- `Boolean Show()`

### `SelectObjectsDialogAccessor`2`
**Свойства:** SelectedObjects: TList, Caption: String
**Методы:**
- `Boolean Show()`

### `SelectRevisionsFilterCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `SendMailItemActivityBase`
**Свойства:** To: Collection`1, Subject: Activity`1, Text: Activity`1, Template: InArgument`1, Attachments: Collection`1, CopyToExternalEMail: InArgument`1

### `SendMessageTaskAction`
**Свойства:** MessageRecipients: List`1, Administrators: List`1, MessageTemplateId: Guid, AttachObject: Boolean, Name: String
**Методы:**
- `TaskActionResult Execute(MacroContext context)`

### `SequenceActivityBase`
**Свойства:** Variables: Collection`1, Activities: Collection`1

### `SequenceResultActivityBase`
**Свойства:** Activities: Collection`1

### `SequenceResultActivityReturnBase`
**Свойства:** Activities: Collection`1

### `SerialNumberCriteria`
**Методы:**
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `SeriesSettings`
**Свойства:** Guid: Guid, Name: String, Reference: Guid, FilterString: String, IsActive: Boolean, SeriesType: String, GroupName: String, LineThickness: Int32, ComputationType: SeriesComputationType, ComputationFormula: String, UniversalPathString: String, Color: Color, ModelType: String, MarkerModelType: Marker2DModelType, MarkerModelSize: Int32, MarkerModelVisibility: Boolean, MarkerModel2Type: Marker2DModelType, MarkerModel2Size: Int32, MarkerModel2Visibility: Boolean, IsLabelVisible: Boolean, IsLabelConnectorVisible: Boolean, LabelPointView: LabelViewMode, LabelViewPatternString: String, LabelPosition: LabelPositionMode, LabelKind: LabelKindMode, LabelAngle: Double, PaneId: Guid, ShowInLegend: Boolean, LegendName: String, LegendTextPattern: String, UseSummaryGrouping: Boolean, SummaryGroupingStep: Double, SummaryGroupingOffset: Double, AlignSummaryGrouping: Boolean, WindowSummaryGroupingByCount: Boolean, IsSummaryAgregationFormulaReturnPoints: Boolean, AgregationParameters: ObservableCollection`1, SummaryGroupingMode: SummaryAggregationGroupingMode, SummaryGroupingAlignMode: SummaryAggregationGroupingAlignMode, SummaryGroupingFormula: String, IntegrationEnabled: Boolean, PointIntegrationType: PointIntegrationType, Parameters: ObservableCollection`1, HoleRadiusPercent: Double, NestedDonutWeight: Double, NestedDonutInnerIndent: Double, TotalLabelPattern: String, ShowTitle: Boolean

### `SeriesViewParameters`
**Свойства:** Id: Guid, LegendText: String, Color: Nullable`1

### `ServerConnection`
**Свойства:** IsWebServer: Boolean, ConnectionParameters: ConnectionParameters, ClientView: ClientView, CachingFileServer: CachingFileServerObject, WorkingFolder: String, IsConnected: Boolean, IsDemo: Boolean, LdapUrl: String, IsAdministrator: Boolean, IsSystem: Boolean, Version: Version, EvaluationTime: Nullable`1, UpdateVersion: Version, UpdateRequestRequired: Boolean, Callback: IModelCallback, ServerName: String, InstanceName: String, CurrentConfiguration: BaseConfiguration, DefaultConfiguration: ClientConfiguration, FullTextSearchEnabled: Boolean, SupportCertificates: Boolean, FilePreviewers: FilePreviewers, ViewerService: ViewerService, ToolsManager: CommonToolsManager, Mail: MailService, ServerTaskManager: ServerTaskManager, BytesSent: Int64, BytesReceived: Int64, UnzippedBytesSent: Int64, UnzippedBytesReceived: Int64, SentPercentsZipped: Double, ReceivedPercentsZipped: Double, ReferenceCatalog: ReferenceCatalog, IsReferenceCatalogLoaded: Boolean, References: SystemReferences, EventWatcher: EventWatcher, SaveSettingsOnClose: Boolean, Stages: List`1, Schemes: List`1, SignatureTypes: List`1, AccessGroups: List`1, Logging: LogManager, SettingsManager: SettingsManager, ClientViews: List`1, Licenses: LicenseManager, ReferencesStorageCollection: ReferencesStorageCollection, IsCertificateItemsEmpty: Boolean, ExtendedParameters: ExtendedParametersManager, ConfigurationSettings: ConfigurationSettings, OmitHasChildrenCheck: Boolean
**Методы:**
- `Boolean HasLicense(LicenseFunction function)`
- `IList`1 GetCertificatesInfo()`
- `Void CloseCertificate(Certificate certificate) (+1)` [has Async]
- `Void CloseCertificates()` [has Async]
- `Void SendCertificates()` [has Async]
- `Void RefreshStages()`
- `Void RefreshSchemes()`
- `Void RefreshSignatureTypes()`
- `Void RefreshAccessGroups()`
- `Void RefreshClientViews()`
- `CertificateSessionItem GetOpenedCertificate(Guid certificateGuid)`
- `Boolean IsCertificateOpened(Guid certificateGuid, Boolean checkExpiration)`
- `String GetCertificateKeyName(Guid certificateGuid)`
- `Void ClearCertificateItems()`
- `Void AddCertificateItem(CertificateSessionItem item)`
- `Void SetRequestLogger(ILogger logger)`
- `Void SetWebServerMode(String actualFileFolder, String workingFileFolder)`
- `Void SubscribeAccessChanges()` [has Async]
- `ServerConnection Open(String userName, MD5HashString password, String server, Nullable`1 configurationGuid, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+6)` [has Async]
- `Boolean Prepare(Boolean reregister, Nullable`1 configuration, LoadingCallback loadingCallback)`
- `ServerConnection OpenWithToken(String server, String accessToken, Nullable`1 configurationGuid, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+1)` [has Async]
- `ServerConnection OpenWithOidcToken(String server, String oidcToken, Guid oidcProvider, Nullable`1 configurationGuid, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+1)` [has Async]
- `AuthToken GenerateToken(String userName, MD5HashString password, String server, String clientId, Nullable`1 configurationGuid, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+3)` [has Async]
- `AuthToken RefreshToken(String server, String refreshToken, String clientId, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+2)` [has Async]
- `List`1 GetConfigurations(String userName, MD5HashString password, String server, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, ConfigurationType configurationType) (+4)` [has Async]
- `List`1 GetOpenIdProviders(String server, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression) (+1)` [has Async]
- `Void Close()` [has Async]
- `Boolean SetConnectionParameters()`
- `Boolean RunUpdate(ConcurrencyException exception, Object ownerWindow)`
- `String GetLocalStorageFolderPath(String folderName)`
- `String GetWorkingFolder(DesignContextObject designContextObject)` [has Async]
- `String GetDefaultSystemWorkingFolderPath()`
- `Void SetWorkingFolder(String path)` [has Async]
- `List`1 GetActiveConnections()` [has Async]
- `Void CloseUserConnection(IEnumerable`1 connections)` [has Async]
- `List`1 GetAvailableLicenses()` [has Async]
- `LicenseKeyInfo GetLicenseKeyInfo()` [has Async]
- `List`1 GetClientConfigurations()` [has Async]
- `List`1 GetWebConfigurations()` [has Async]
- `Boolean ExportConfigurations(Stream stream, IEnumerable`1 configurations)` [has Async]
- `List`1 ImportConfigurations(Stream stream)` [has Async]

### `ServerConnectionDictionary`1`
**Свойства:** Keys: ICollection`1, Values: ICollection`1, Item: T, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `T Get(ServerConnection connection)`
- `T GetOrAdd(ServerConnection connection, Func`1 valueFactory)`
- `Void Add(ServerConnection connection, T value)`
- `Boolean ContainsKey(ServerConnection connection)`
- `Boolean Remove(ServerConnection connection)`
- `Boolean TryGetValue(ServerConnection connection, T& value)`
- `Void Clear()`
- `IEnumerator`1 GetEnumerator()`

### `ServerConnectionExtensions`
**Методы:**
- `Reference CreateReference(ServerConnection connection, Int32 referenceId, Boolean prototypeMode) (+5)` [has Async]
- `Void ClearWorkingFolder(ServerConnection connection)` [has Async]

### `ServerDiscovery`
**Методы:**
- `ServiceSpecification Find(String serverAddress, Boolean udpDiscovery, TimeSpan searchTime)` [has Async]
- `Int32 GetServerVersion(ServiceSpecification service)`

### `ServerEventHandlerCondition`
**Свойства:** Parameter: ParameterInfo, LinkGroup: ParameterGroup, Condition: Int32, Value: Object

### `ServerGateway`
**Свойства:** Connection: ServerConnection, ConnectionParameters: ConnectionParameters, IsConnected: Boolean, IsDemo: Boolean, Version: Version, EvaluationTime: Nullable`1, Callback: IModelCallback, ServerName: String, CurrentConfiguration: BaseConfiguration, Mail: MailService, BytesSent: Int64, BytesReceived: Int64, UnzippedBytesSent: Int64, UnzippedBytesReceived: Int64, SentPercentsZipped: Double, ReceivedPercentsZipped: Double
**Методы:**
- `Void Connect(String userName, MD5HashString password, String server, Nullable`1 configurationGuid, CommunicationMode communication, DataSerializerAlgorithm dataSerializer, CompressionAlgorithm compression, IWebProxy proxy) (+7)`
- `Void Disconnect()`
- `List`1 GetActiveConnections()`
- `List`1 GetAvailableLicenses()`
- `LicenseKeyInfo GetLicenseKeyInfo()`
- `List`1 GetClientConfigurations()`
- `List`1 GetWebConfigurations()`
- `List`1 GetConfigurations()`
- `Boolean ExportConfigurations(Stream stream, IEnumerable`1 configurations) (+1)`
- `List`1 ImportConfigurations(Stream stream)`

### `ServerTask`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, Name: String, Comment: String, Enabled: Boolean, User: User, Trigger: Trigger, Action: TaskAction, LastSuccessExecuteTime: DateTime, LastExecuteTime: DateTime, NextExecuteTime: DateTime, LastExecuteResult: String, ExecuteCount: Int32, IsAdded: Boolean, IsModified: Boolean, IsDeleted: Boolean, IsChanged: Boolean, Changing: Boolean
**Методы:**
- `Void BeginChanges()`
- `Void CancelChanges()`
- `Boolean Save()` [has Async]
- `Boolean Delete()` [has Async]

### `ServerTaskManager`
**Свойства:** Connection: ServerConnection
**Методы:**
- `ServerTask GetTask(Int32 id) (+1)` [has Async]
- `List`1 GetTasks()` [has Async]
- `ServerTask CreateTask()`
- `Boolean DeleteTasks(ICollection`1 tasks)` [has Async]
- `ServerEventHandler GetEventHandler(Guid handlerId)` [has Async]
- `List`1 GetEventHandlers(Boolean reload)` [has Async]
- `ServerEventHandler CreateEventHandler()`
- `Boolean SaveEventHandler(ServerEventHandler eventHandler)` [has Async]
- `Boolean DeleteEventHandler(ServerEventHandler eventHandler)` [has Async]
- `Void ImportEventHandlers(Stream stream)` [has Async]
- `Void ExportEventHandlers(Stream stream, IEnumerable`1 handlers)` [has Async]
- `List`1 GetRaisedServerEvents(DateTime dateTime)` [has Async]
- `List`1 GetNewOnsetDateRaisedEvents()` [has Async]

### `ServerTaskServiceData`
**Свойства:** LoadedTasksFunc: Func`1, FindTaskByIdFunc: Func`2, FindTaskByGuidFunc: Func`2, GetIsSoppedFunc: Func`1, UpdateTaskFunc: Action`2, LoggingProcessTasks: Boolean
**Методы:**
- `Void RaiseTaskChanged(ServerTask task)`
- `Void RaiseTaskDeleted(Int32[] idCollection, Guid[] guidCollection)`
- `Void RaiseStopping()`

### `ServiceCallbackOwnerInfo`
**Свойства:** OwnerId: Int32, Type: FilePreviewType, Owner: IViewerServiceOwner, ConnectionParameters: String, Async: Boolean, IsInstalledProgram: Boolean, Context: String

### `SetOfReports`
**Свойства:** CanExecute: Boolean
**Методы:**
- `Boolean ValidateLicense(Boolean throwOnError)`
- `Void Generate(ReportGenerationContext context)`
- `Void InitializeContext(ReportGenerationContext context, Boolean generating)`
- `IEnumerable`1 GetReportParameters()`

### `SetOfReportsParameter`
**Свойства:** Name: StringParameter, Type: StringParameter, IsConstant: BooleanParameter, Value: StringParameter
**Методы:**
- `SetOfReportsParameter CreateContextParameter()`

### `SettingsContainer`1`
**Свойства:** ExplicitLoading: Boolean, Connection: ServerConnection, Application: String, Interface: String, Context: String, ParameterGroupId: Int32, ObjectId: Int32, FolderGuid: Guid, SupportsViews: Boolean, SharingType: SettingsSharingType, IsCommon: Boolean, IsLoaded: Boolean, IsNew: Boolean, Exists: Boolean, Data: TSettingsData, CurrentApplicationName: String, IsLocked: Boolean, Views: ReadOnlyCollection`1, CurrentView: SettingsView`1, DefaultView: SettingsView`1
**Методы:**
- `Void Lock()`
- `Void Unlock()`
- `Boolean Load()` [has Async]
- `Void Clear()`
- `Void ReloadViews()`
- `Void Reset()`
- `Boolean Reload(Boolean reloadViews)` [has Async]
- `Void Save()` [has Async]
- `Boolean Remove()`
- `SettingsView`1 CreateView(String name, SettingsViewType type, Boolean inSettingsContext, Boolean copySettings, ConfigurationUseType configurationUseType, List`1 configurations, SettingsViewAccessType accessType, List`1 users, Boolean showOpenAsCommand, String comment)`
- `Void UpdateView(SettingsView`1 view, String name, SettingsViewType type, Boolean inSettingsContext, Boolean copySettings, ConfigurationUseType configurationUseType, List`1 configurations, SettingsViewAccessType accessType, List`1 users, Boolean showOpenAsCommand, String comment)`
- `Boolean DeleteView(SettingsView`1 view)`
- `Void ApplyView(SettingsView`1 view) (+1)`
- `ICollection`1 GetSharedViews(ServerConnection connection, Int32 parameterGroupId, String interface, String application, String contextName)` [has Async]
- `ICollection`1 GetShowOpenAsCommandViews(ServerConnection connection, Int32 parameterGroupId, String interface, String application, String contextName, CancellationToken token)` [has Async]
- `Void RegisterSettingsType()`

### `SettingsManager`
**Методы:**
- `String GetSettingsData(SettingsSharingType settingsSharingType, Int32 groupId, String interfaceName, String appInstance, Guid folderGuid, Int32 objectId, String context, Guid viewGuid)` [has Async]
- `IReadOnlyCollection`1 GetViews(SettingsSharingType settingsSharingType, Int32 groupId, String interfaceName, String appInstance, Guid folderGuid, Int32 objectId, String context)` [has Async]
- `IReadOnlyCollection`1 GetAllViews(ParameterGroup referenceGroup)` [has Async]
- `RawSettingsView CreateView(String viewName, SettingsViewType type, ConfigurationUseType configurationUseType, List`1 configurations, Boolean inSettingsContext, SettingsSharingType sharingType, String data, Int32 groupId, String interfaceName, String appInstance, Guid folderGuid, Int32 objectId, String context)` [has Async]
- `Guid UpdateView(Guid viewId, String data, String viewName, SettingsViewType type, ConfigurationUseType configurationUseType, List`1 configurations, Boolean inSettingsContext, SettingsSharingType sharingType, Int32 groupId, String interfaceName, String appInstance, Guid folderGuid, Int32 objectId, String context) (+1)` [has Async]
- `Boolean DeleteView(Guid id)` [has Async]

### `SettingsView`1`
**Свойства:** Owner: SettingsContainer`1, Id: Guid, Name: String, Comment: String, Type: SettingsViewType, IsDefault: Boolean, IsShared: Boolean, IsInSettingsContext: Boolean, ConfigurationUseType: ConfigurationUseType, Configurations: ReadOnlyCollection`1, DefaultConfigurations: ReadOnlyCollection`1, IsDefaultForAllConfigurations: Boolean, ShowOpenAsCommand: Boolean, AccessType: SettingsViewAccessType, Users: ReadOnlyCollection`1
**Методы:**
- `Boolean CanUseInCurrentConfiguration()`
- `Boolean CanUseInConfiguration(BaseConfiguration configuration)`
- `String GetData()`
- `Int32 CompareTo(SettingsView`1 other) (+1)`

### `SettingsViewAccessTypeExtensions`
**Методы:**
- `String GetName(SettingsViewAccessType type)`

### `SettingsViewTypeExtensions`
**Методы:**
- `String GetName(SettingsViewType type)`

### `SharedDocument`
**Свойства:** OpenedDocuments: IList`1, FileName: String, VirtualAssembly: Guid, ReadOnly: Boolean
**Методы:**
- `String GetFilePreviewControlAssemblyNameByExtension(String extension)`
- `SharedDocument OpenDocument(String fileName, Object context, Boolean readOnly) (+2)`
- `T OpenVirtualDocument(FileContext fileContext)`
- `Void CloseDocument(SharedDocument sharedDocument)`
- `SharedDocument FindDocumentByContext(FileContext context)`
- `CADObjectInfo FindCADObject(String searchString)`
- `Object GetCADObjectPropertyValue(CADObjectInfo cadObjectInfo, CADObjectPropertyInfo cadObjectPropertyInfo)`
- `CADObjectPropertyInfo GetCADObjectPropertyValueWithUnit(CADObjectInfo cadObjectInfo, CADObjectPropertyInfo cadObjectPropertyInfo)`
- `CADVar[] GetVariables()`
- `CADStructureElementInfo[] GetStructureElements(String[] structureElementTypes)`
- `CADStructureElementTypeInfo[] GetStructureElementTypes()`
- `CADDim GetDimension(String searchString)`
- `CADRoughness GetRoughness(String searchString)`
- `CADObject GetCADObject(String searchString)`
- `InteractiveCADVersionInfo GetVersion()`
- `DataTable GetTable(CADObjectInfo cadObjectInfo)`
- `CadMeasure GetMeasure(String[] searchString, String measuredParameter)`

### `SharedDocumentImplementationAttribute`
**Свойства:** Extensions: String[]

### `ShortcutObject`
**Свойства:** Description: ShortcutDescription

### `ShortcutTypeExtension`
**Методы:**
- `String GetText(ShortcutType type)`

### `ShowFileContext`
**Свойства:** FilePath: String, OpeningDocumentId: Int32, OpeningObjectGuid: Guid, Parameters: String, CanPrint: Boolean, AdditionalUniqueKey: String, ReadOnly: Boolean, TFlexCadWindowType: Int32, ViewAreaWidth: Int32, ViewAreaHeight: Int32, LinkedObjectInstanceGuid: Guid, ViewAreaSize: Size

### `Signature`
**Свойства:** SignatureTypeCollection: List`1, Signatures: SignatureCollection, Id: Int32, TypeId: Int32, SignatureObjectType: SignatureType, UserObject: UserReferenceObject, State: SignatureState, UserId: Int32, UserName: String, OnBehalfOfName: String, OnBehalfOfId: Int32, OnBehalfOfUser: User, SignatureDate: Nullable`1, Resolution: String, Actual: Boolean, DigitalSignature: Byte[], SignedParameters: String, HasDigitalSignature: Boolean, ErrorMessage: String, CanDelete: Boolean, CanUpdate: Boolean, Item: Object
**Методы:**
- `Boolean Edit()`
- `Boolean UpdateDate()`
- `Boolean Update()`
- `Boolean Delete()`
- `Nullable`1 ValidateDigitalSignature()`
- `String FindParametersNames()`
- `List`1 GetParsedSignedParameters()`
- `Byte[] GenerateDigitalSignature(ReferenceObject referenceObject, X509Certificate2 certificate, Byte[] signingData)`

### `SignatureAccessor`
**Свойства:** SignatureType: String [RU: ТипПодписи], User: RefObj, SignatureDate: Nullable`1 [RU: ДатаПодписи], IsActual: Boolean [RU: Актуальная], IsSet: Boolean [RU: Актуальная], Resolution: String [RU: ТипПодписи], HasDigitalSignature: Boolean [RU: Актуальная], Пользователь: Объект [RU only]
**Методы:**
- `Boolean Delete()` [RU: Удалить]

### `SignatureAccessorList`1`
**Свойства:** Item: T, Item: T, Count: Int32
**Методы:**
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `SignatureFormulaMacro`
**Свойства:** CodeOffset: Int32

### `SignatureMacroContext`
**Свойства:** Signature: Signature

### `SignatureMacroProvider`
**Свойства:** Context: SignatureMacroContext, CurrentSignature: SignatureObj, ТекущаяПодпись: Подпись [RU only]

### `SignatureObj`
**Методы:**
- `SignatureObj CreateInstance(Signature signature, MacroContext context)`

### `SignatureObjectValue`
**Свойства:** Signature: Signature, SignatureParameter: SignatureParameter

### `SignatureParameterExtensions`
**Методы:**
- `String GetName(SignatureParameter parameter)`
- `String GetTypeDescription(SignatureParameter parameter)`
- `Type GetValueType(SignatureParameter parameter)`

### `SignatureParameterItem`
**Свойства:** Icon: IconImage, Name: String, Type: PathItemType, Parameter: SignatureParameter, SignatureIndex: Int32

### `SignaturePathItem`
**Свойства:** Name: String, Type: PathItemType
**Методы:**
- `Boolean IsOneToMany()`

### `SignatureStateExtensions`
**Методы:**
- `String GetName(SignatureState state)`

### `SignatureType`
**Свойства:** Types: SignatureTypes, Connection: ServerConnection, Id: Int32, Guid: Guid, Name: String, Description: String, UsersAccessType: ItemListUseType, IsSignatureTypeInUse: Boolean
**Методы:**
- `List`1 GetAccessUsers()`
- `Void SetAccessUsers(IEnumerable`1 users)`
- `Boolean ValidateUserAccess(UserReferenceObject user, SignatureState state, Boolean throwException)`
- `Boolean ValidateParameterGroupAccess(ParameterGroup group, Boolean throwException)`
- `Boolean Edit()`
- `Boolean Delete()`
- `SignatureType Find(ServerConnection connection, Int32 id) (+2)`

### `SignatureTypeAccessor`
**Свойства:** Id: Int32 [RU: Идентификатор], Guid: Guid [RU: УникальныйИдентификатор], Name: String [RU: Наименование], Description: String [RU: Наименование]

### `SignatureTypeAccessorList`1`
**Свойства:** Item: T, Item: T, Count: Int32
**Методы:**
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `SignatureTypeItem`
**Свойства:** Icon: IconImage, Name: String, SupportSearchType: SupportSearchTypes, Type: PathItemType, SignatureType: SignatureType

### `SignatureTypeObj`
**Методы:**
- `SignatureTypeObj CreateInstance(SignatureType signatureType, MacroContext context)`

### `SignatureTypes`
**Свойства:** Connection: ServerConnection
**Методы:**
- `SignatureType AddSignatureType(String name, String description)`
- `List`1 GetAccessibleSignatureTypes(User user)`
- `IEnumerator`1 GetEnumerator()`

### `SignatureTypesItem`
**Свойства:** Name: String, Type: PathItemType, Icon: IconImage, SupportSearchType: SupportSearchTypes

### `SigningParametersAttribute`
**Свойства:** Caption: String, IsSystem: Boolean, CanChangeCaption: Boolean, CanRemove: Boolean, Value: Object

### `SigningParametersInfo`
**Свойства:** SigningParameters: List`1, IsInherit: Boolean, IsDefault: Boolean

### `SingleParameter`
**Методы:**
- `Single GetSingle()`
- `TypeCode GetTypeCode()`

### `Smtp`
**Свойства:** SessionPassword: String, AskPassword: Boolean, ServerName: String, Login: String, Password: String, UseSSL: Boolean, UseAuthentication: Boolean, CopyToSent: Boolean, AuthenticationType: String, AuthenticationAsIncomingMail: Boolean, Port: Int32, IsEmpty: Boolean, IsModified: Boolean
**Методы:**
- `SmtpSettings ToServerSettings()`

### `SortRuleAction`
**Свойства:** FolderId: Int32, FolderPath: String
**Методы:**
- `MailRuleAction ToServer()`

### `SourceCode`
**Свойства:** Code: String, Source: String

### `SourceReferenceObjectTerm`
**Свойства:** Path: ReferencePath, SourcePath: ReferencePath, Coefficient: Double, CoefficientVariableName: String, CoefficientVariable: Variable`1, Factor: Double, FactorVariableName: String, FactorVariable: Variable`1, IsNumberSource: Boolean, ParameterName: String
**Методы:**
- `Void Clear()`
- `Boolean SupportsOperator(ComparisonOperator operator)`
- `Void ReplaceVariablesByValues()`

### `SourceRevisionReferenceObject`
**Свойства:** Class: SourceRevisionsType, Name: StringParameter, ApplyingStage: GuidParameter, SourceRevision: ReferenceObject

### `SourceRevisionsReference`
**Свойства:** Classes: SourceRevisionsTypes

### `SourceRevisionsType`
**Свойства:** Classes: SourceRevisionsTypes, IsSourceRevisionType: Boolean

### `SourceRevisionsTypes`
**Свойства:** SourceRevisionType: SourceRevisionsType

### `SpecialClassTree`1`
**Методы:**
- `TClass Find(Int32 classId) (+2)`
- `IEnumerator`1 GetEnumerator()`

### `SpecialComplexHierarchyLink`2`
**Свойства:** Reference: TReference, ParentObject: TReferenceObject, ChildObject: TReferenceObject

### `SpecialComplexHierarchyLinkParameters`1`
**Свойства:** Link: TComplexHierarchyLink

### `SpecialFilterArgs`
**Свойства:** ParameterGroup: ParameterGroup, PrototypeMode: Boolean, IsSlave: Boolean, IsSystemCatalog: Boolean, UseCache: Boolean

### `SpecialLinkPathItem`
**Свойства:** SupportSearchType: SupportSearchTypes, SystemType: SystemParameterType

### `SpecialReference`1`
**Свойства:** Objects: ReferenceObjectCollection`1
**Методы:**
- `TObject CreateReferenceObject(ReferenceObject parentObject, ClassObject classObject) (+3)`
- `TObject CreateRevisionsContainer(ReferenceObject parentObject, ClassObject classObject, Guid revisionsContainerGuid) (+1)`
- `IComparer`1 GetAfterLoadSortComparer()`
- `TObject Find(Int32 objectId, Boolean ignoreLinks) (+3)` [has Async]
- `TObject FindOne(ParameterInfo parameter, ComparisonOperator op, Object value) (+3)` [has Async]

### `SpecialReferenceFactory`
**Свойства:** IsStatic: Boolean, ReferenceType: Type, ClassTreeType: Type
**Методы:**
- `Void LoadRequiredParameters(LoadSettings settings, Boolean oneToOneLink)`
- `Filter GetSpecialFilter(SpecialFilterArgs args)`

### `SpecialReferenceFactory`2`
**Свойства:** ReferenceType: Type, ClassTreeType: Type
**Методы:**
- `TReference CreateReference(ParameterGroup masterGroup)`
- `TClassTree CreateClassTree(ParameterGroup masterGroup)`

### `SpecialReferenceObject`1`
**Свойства:** Reference: TReference

### `SpecialToManyLinkPathItem`
**Методы:**
- `Boolean IsOneToMany()`

### `SpendingResourceLinkObject`
**Свойства:** Price: Double
**Методы:**
- `Void UpdateValue()`

### `SSLModeExtensions`
**Методы:**
- `SSLMode ToServer(SSLMode apiValue)`
- `SSLMode ToModel(SSLMode serverValue)`

### `Stage`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, Name: String, Comment: String, Changing: Boolean, RequireModificationNotice: Boolean, SetModificationNoticeReady: Boolean
**Методы:**
- `Void BeginChanges()`
- `Boolean EndChanges()` [has Async]
- `Void CancelChanges()`
- `Boolean Delete()` [has Async]
- `List`1 Clear(ServerConnection connection, IEnumerable`1 objects, String comment) (+1)` [has Async]
- `List`1 Set(IEnumerable`1 objects, String comment) (+1)` [has Async]
- `List`1 Change(IEnumerable`1 objects, String comment) (+1)` [has Async]
- `List`1 AutomaticChange(IEnumerable`1 objects, String comment) (+1)` [has Async]
- `List`1 GetStages(ServerConnection connection) (+2)` [has Async]
- `Stage Find(ServerConnection connection, Int32 id) (+4)` [has Async]
- `Dictionary`2 LoadSimpleStages(ServerConnection connection)` [has Async]
- `List`1 SetObjectsStage(Stage stage, IEnumerable`1 objects)`
- `List`1 ChangeObjectsStage(Stage stage, IEnumerable`1 objects)`
- `List`1 AutomaticChangeObjectsStage(Stage stage, IEnumerable`1 objects)`

### `StageAccessType`
**Свойства:** Name: String, AccessTypeID: AccessTypeID, IsStage: Boolean

### `StartProductPathItem`
**Свойства:** Name: String, Type: PathItemType

### `StateCollection`1`
**Свойства:** IsModified: Boolean, Item: T, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `Void Rollback()`
- `IEnumerable`1 GetAddedItems()`
- `IEnumerable`1 GetDeletedItems()`
- `Int32 IndexOf(T item)`
- `Void Insert(Int32 index, T item)`
- `Void RemoveAt(Int32 index)`
- `Void Add(T item)`
- `Void Clear()`
- `Boolean Contains(T item)`
- `Void CopyTo(T[] array, Int32 arrayIndex)`
- `Boolean Remove(T item)`
- `IEnumerator`1 GetEnumerator()`

### `StateGuidDomainObject`
**Свойства:** IsAdded: Boolean, IsModified: Boolean, IsDeleted: Boolean, IsChanged: Boolean

### `StatusChangeCommentObject`
**Свойства:** OldStatusType: AssignmentStatus, NewStatusType: AssignmentStatus, OldStatus: Int32Parameter, NewStatus: Int32Parameter

### `StringFieldInputDialog`
**Свойства:** TypeName: String, DefaultValue: InArgument`1, IsMultiline: Boolean, Mask: InArgument`1

### `StringParameter`
**Свойства:** IsEmpty: Boolean
**Методы:**
- `String GetString()`
- `Guid GetGuid()`
- `TypeCode GetTypeCode()`

### `StringVariableData`
**Свойства:** Value: String

### `StructureColumn`
**Свойства:** Id: Guid, Name: String, IsHidden: Boolean, Index: Int32, IsSystem: Boolean, IsDynamic: Boolean, AllowEdit: Boolean
**Методы:**
- `Void CopyPropertiesFrom(StructureColumn column)`
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `StructureConfigurationData`
**Свойства:** Connection: ServerConnection, Item: StructureGroup, Roots: IEnumerable`1, Groups: ReadOnlyCollection`1, Columns: ReadOnlyCollection`1, Variables: VariableCollection
**Методы:**
- `Void CreateDefaultStructure(ParameterGroup parameterGroup) (+1)`
- `StructureGroup CreateGroup(ParameterGroup parameterGroup, StructureGroupType type, StructureGroup parent, HierarchyDirections hierarchyDirection, String userPath) (+1)`
- `Void RemoveGroup(StructureGroup group)`
- `Void AddGroup(StructureGroup group, StructureGroup parentGroup)`
- `StructureColumn CreateColumn(Guid id, String columnName, Boolean isDynamic) (+1)`
- `Void RemoveColumn(Guid id) (+1)`
- `Boolean HasVisibleGroupSupportsDesignContexts()`
- `Void UpdateColumnIndexes()`
- `Void UpdateDynamicColumnData(StructureColumn column)`
- `String Serialize()`
- `StructureConfigurationData Deserialize(String xmlData, ServerConnection connection)`
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`

### `StructureElementObject`
**Свойства:** Name: StringParameter, Date: DateTimeParameter, ProductStructureId: Int32Parameter, Amount: DoubleParameter, Position: Int32Parameter, BOMSection: StringParameter, VariationDescription: StringParameter, Denotation: StringParameter
**Методы:**
- `Void SetProductProperties(NomenclatureReferenceObject nomRefObject, NomenclatureHierarchyLink link)`
- `XElement GetXElement()`

### `StructureGroup`
**Свойства:** Owner: StructureConfigurationData, GroupCacheInfo: Object, GroupSettings: StructureGroupSettings, CanSupportOrder: Boolean, Filter: StructureGroupFilter, ExternalFilter: Filter, MergedFilter: Filter, UseParentColumns: Boolean, HasColumnsSettings: Boolean, IsChildrenWithParent: Boolean, IsEmpty: Boolean, Item: BaseColumnData, GroupId: Guid, ParameterGroup: ParameterGroup, Type: StructureGroupType, ReferencePath: String, ShowInStructure: Boolean, ClassId: Guid, Path: String, Parent: StructureGroup, AllParents: IEnumerable`1, Master: StructureGroup, Classes: IEnumerable`1, Children: IEnumerable`1, ContainActiveMultipleReferenceDetalization: Boolean, IsMultipleReferenceDetalization: Boolean, IsHidden: Boolean
**Методы:**
- `Boolean IsUnidirectionalLink(GroupCache groupCache)`
- `Void AddExtendedParameter(String key, Object value)`
- `Boolean RemoveExtendedParameter(String key)`
- `Boolean HasExtendedParameter(String key)`
- `Boolean TryGetExtendedParameter(String key, Object& value)`
- `Void RegisterExtendedParameterSerializer(String key, XmlSerializer serializer)`
- `List`1 GetDisplayChildGroups(DesktopObject referenceObject, GroupCache groupCache)`
- `StructureGroup CreateChild(ParameterGroup parameterGroup, StructureGroupType type, HierarchyDirections hierarchyDirection, String userPath) (+1)`
- `Void RemoveGroup(StructureGroup child)`
- `StructureGroup CreateClassStructure(Guid classId)`
- `Void Delete()`
- `Void DeleteWithChildren()`
- `StructureGroup GetClassStructure(ClassObject classObject)`
- `Void CopyPropertiesFrom(StructureGroup structureGroup)`
- `XmlSchema GetSchema()`
- `Void ReadXml(XmlReader reader)`
- `Void WriteXml(XmlWriter writer)`
- `Boolean CanContainStructureGroup(DesktopObject desktopObject, StructureGroup group, GroupCache groupCache)`

### `StructureGroupFilter`
**Свойства:** Owner: StructureConfigurationData, Variables: VariableCollection

### `StructureGroupSettings`
**Свойства:** Type: StructureGroupType, Owner: StructureConfigurationData, ParameterGroup: ParameterGroup, HierarchyDirection: HierarchyDirections, DisableConfigurationFilter: Boolean, Hidden: Boolean, ShowFolder: Boolean, ShowEmptyFolder: Boolean, ShowCreateCommand: Boolean, ShowDeleteCommand: Boolean, ShowAddCommand: Boolean, ShowRemoveCommand: Boolean, ShowReferenceCommands: Boolean, ShowDialogOnCreating: Nullable`1, SupportsOrder: Boolean, ShowReferenceFolders: Boolean, DefaultGroupIndex: Nullable`1, GroupIndex: Nullable`1, GlobalOrdering: Boolean, ShowCommandsFromRoot: Boolean, ObjectOrderPath: String, GroupFolderIconPath: String, VisibleToVarName: String, SelectedToVarName: String, ObjectOrderDirection: Nullable`1, UniversalPathOutputGroupGuid: Guid, RecursiveGroup: String, UserPath: String, GroupingPath: String, SystemFolderId: String, LinkGroupingKeyPath: String, UserFolderName: String, CustomIconGuid: Guid, Columns: Dictionary`2, Item: BaseColumnData
**Методы:**
- `Void RemoveColumn(Guid id)`
- `IEnumerator`1 GetEnumerator()`

### `StructureGroupType`
**Свойства:** ShowFolderLock: Nullable`1, ShowEmptyFolderLock: Nullable`1, ShowCreateCommandLock: Nullable`1, ShowAddCommandLock: Nullable`1, ShowDeleteCommandLock: Nullable`1, ShowRemoveCommandLock: Nullable`1, CanHidedLock: Nullable`1, DisableConfigurationFilterLock: Nullable`1, IsLinkOrParameterGroup: Boolean, CanContainMultipleReferencesDetalization: Boolean, Type: StructureGroupTypes
**Методы:**
- `String AppendToPath(String path, HierarchyDirections hierarchyDirection, String pathItem) (+2)`

### `StructurePath`
**Свойства:** CurrentElement: PathElement, ResultDefaultType: DefaultSupportedType, ResultType: Type, IsContextVariable: Boolean, IsVariable: Boolean, IsReference: Boolean, IsCorrect: Boolean, IsEmpty: Boolean, Item: PathElement, Count: Int32
**Методы:**
- `Boolean Validate()`
- `ObjectValue GetObjectValue(ServerConnection connection) (+2)`
- `Object GetValue(ServerConnection connection) (+2)`
- `Object GetAccessorValue(ServerConnection connection) (+2)`
- `String Serialize()`
- `String ToVariableString()`
- `Boolean TryParse(String value, StructurePath& path)`
- `StructurePath Parse(String value)`
- `Void RegisterType(RegisterPathType pathType)`
- `Int32 IndexOf(PathElement item)`
- `Void Clear()`
- `Boolean Contains(PathElement item)`
- `Void CopyTo(PathElement[] array, Int32 arrayIndex)`
- `IEnumerator`1 GetEnumerator()`

### `StructurePathContext`
**Свойства:** Path: StructurePath, MacroContext: MacroContext, ParentValue: ObjectValue

### `StructurePathExtensions`
**Методы:**
- `TStructurePath Add(TStructurePath path, PathElement pathElement)`
- `TStructurePath AddReference(TStructurePath path, ReferenceInfo referenceInfo, Boolean prototypeMode) (+2)`
- `TStructurePath AddObject(TStructurePath path, ReferenceObject referenceObject) (+1)`
- `TStructurePath AddLinkGroup(TStructurePath path, ParameterGroup parameterGroup)`
- `TStructurePath AddVariable(TStructurePath path, VariableInfo variableInfo, ReferenceInfo referenceInfo)`

### `StructuresMappingMacroContext`
**Свойства:** SourceInstance: IEnumerable`1, TargetInstance: IEnumerable`1

### `StructureTypeCriteria`
**Методы:**
- `Boolean DefaultValueIsNotNull()`
- `Object GetDefaultValue()` [has Async]
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`

### `StructureTypePathItem`
**Свойства:** Name: String, Type: PathItemType, SystemType: SystemParameterType

### `StructureTypesPathItem`
**Свойства:** Name: String, Type: PathItemType, SupportSearchType: SupportSearchTypes
**Методы:**
- `Boolean IsOneToMany()`

### `StructureTypesReference`
**Свойства:** BaseStructureType: StructureTypesReferenceObject, Item: StructureTypesReferenceObject, AllStructureTypes: IList`1, Classes: StructureTypesTypes
**Методы:**
- `StructureTypesReferenceObject GetDefaultEditableStructureType(Guid designContextGuid)`
- `StructureTypesReferenceObject Find(String name)` [has Async]

### `StructureTypesReferenceObject`
**Свойства:** Class: StructureTypesType, Name: StringParameter, Comment: StringParameter, IsDefault: BooleanParameter, ShareAccessForAllContexts: BooleanParameter, ParentStructure: StructureTypesReferenceObject
**Методы:**
- `Boolean ValidateEditByCurrentUser(Boolean throwOnError)`
- `Boolean ValidateEditByCurrentUserInContext(Guid designContextGuid, Boolean throwOnError)`
- `Boolean CanChangeParameter(Parameter p, Object newValue)`

### `StructureTypesType`
**Свойства:** Classes: StructureTypesTypes, IsStructureType: Boolean

### `StructureTypesTypes`
**Свойства:** StructureType: StructureTypesType

### `StructureVariantCriteria`
**Методы:**
- `Object GetValueFromConfigurationSettings(ConfigurationSettings configurationSettings, Boolean& apply)`
- `Void ApplyToConfigurationSettings(ConfigurationSettings configurationSettings, Object value, Boolean apply)`

### `StructureVariantFilterData`
**Свойства:** ActiveStructureVariant: StructureVariantsReferenceObject, LoadingStructureVariants: List`1

### `StructureVariantsReference`
**Свойства:** BaseStructureVariant: StructureVariantsReferenceObject, Classes: StructureVariantsTypes

### `StructureVariantsReferenceObject`
**Свойства:** IsBaseStructureVariant: Boolean, Class: StructureVariantsType, Name: StringParameter

### `StructureVariantsType`
**Свойства:** Classes: StructureVariantsTypes, IsStructureVariant: Boolean

### `StructureVariantsTypes`
**Свойства:** StructureVariant: StructureVariantsType

### `SubstitutesHelper`
**Методы:**
- `List`1 Replace(NomenclatureHierarchyLink sourceLink, NomenclatureSubstituteReferenceObject replacement)`

### `SwappedRelationRule`
**Методы:**
- `ParameterGroup FindParameterGroup(ParameterGroup mainGroup)`

### `SwappedToManyLinkStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, HierarchyDirections hierarchyDirection, String pathItem) (+1)`

### `SwappedToOneLinkStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, HierarchyDirections hierarchyDirection, String pathItem) (+1)`

### `SystemAccessType`
**Свойства:** AccessTypeID: AccessTypeID, Type: AccessCommandType, Name: String, IsSystem: Boolean, CreateReference: AccessCommand, EditCommonWorkingPages: AccessCommand, EditPersonalWorkingPages: AccessCommand, EditCommonSearchConditions: AccessCommand, EditPersonalSearchConditions: AccessCommand, EditCommonFilters: AccessCommand, EditPersonalFilters: AccessCommand, EditCommonViews: AccessCommand, EditPersonalViews: AccessCommand, EditCommonCatalogs: AccessCommand, EditPersonalCatalogs: AccessCommand, EditConfigurations: AccessCommand, EditEmailAccounts: AccessCommand, DevelopmentCommonPrototypeLinearBusinessProcesses: AccessCommand, EditCommonEventHandlers: AccessCommand, EditPersonalEventHandlers: AccessCommand, ManageServerTasks: AccessCommand, SubsystemAdministrator: AccessCommand, ObjectChangeMasterServer: AccessCommand

### `SystemObjectTypeExtensions`
**Методы:**
- `String GetName(SystemObjectType type)`

### `SystemParameter`
**Свойства:** IsReadOnly: Boolean, IsNull: Boolean
**Методы:**
- `TypeCode GetTypeCode()`

### `SystemParametersPathItem`
**Свойства:** Name: String, Type: PathItemType, Group: ParameterGroup, SupportSearchType: SupportSearchTypes

### `SystemReferences`
**Свойства:** Connection: ServerConnection, Certificates: CertificateReference, Credentials: CredentialsReference, Users: UserReference, GlobalParameters: GlobalParameterReference, Macros: MacroReference, Reports: ReportReference, Units: UnitReference, WorkingAreas: WorkingAreaReference, NavigationPanel: NavigationPanelReference, AssignmentFolders: AssignmentFolderReference, FileServers: FileServerReference, CachingFileServers: CachingFileServerReference, StructureTypes: StructureTypesReference, DesignContexts: DesignContextsReference, ProductsClassifier: ProductsClassifierReference, ProductOptions: ProductOptionsReference, ProductOptionValues: ProductOptionValuesReference, RevisionNamingRules: RevisionNamingRulesReference, ProductsApplicability: ProductsApplicabilityReference, TypicalConfigurationSettings: TypicalConfigurationSettingsReference, MasterDataServers: Reference, SearchQueries: SearchQueryReference, Configurators: ConfiguratorsReference, UserDialogs: UserDialogsReference, ProductsInstances: ProductsInstancesReference, ProductDesignNumbers: ProductsDesignNumbersReference, ProductsMilestones: ProductsMilestonesReference, ProductCategories: CategoriesReference, DataModels: DataModelsReference, NomParametersSynchro: NomParametersSynchroReference, StructureVariants: StructureVariantsReference, OptionsTableSet: OptionsTableSetReference

### `SystemTaskAction`
**Свойства:** TypeName: String, ActionExecuterType: Type, Name: String
**Методы:**
- `TaskActionResult Execute(MacroContext context)`

### `SystemWindowLink`
**Свойства:** Text: String, WindowType: MdiType, CanContainChildren: Boolean

### `TableIndex`
**Свойства:** Group: ParameterGroup, Name: String, Enable: Boolean, IndexSize: Int64, Fragmentation: Double

### `TaskAction`
**Свойства:** Name: String
**Методы:**
- `TaskActionResult Execute(MacroContext context)`

### `TaskActionContext`
**Свойства:** Task: ServerTask, ExecuteTime: DateTime, MacroTaskActionData: String

### `TaskActionResult`
**Свойства:** Result: String, Success: Boolean

### `TaskActionTypeExtension`
**Методы:**
- `String GetText(TaskActionType type)`

### `TaskFolder`
**Свойства:** Account: DOCsAccount, IsPrivate: Boolean, LoadSharedTasks: Boolean
**Методы:**
- `Filter GetFilter()`
- `Void SetFilter(Filter filter)`
- `List`1 GetTasks(TaskLoadSettings settings) (+1)`

### `TaskGroupReferenceObject`
**Свойства:** SaveFolder: FolderObject, InstanceConversionService: ReferenceObject
**Методы:**
- `ConversionTaskReferenceObject AddConversionTask(FileConversionModuleReferenceObject conversationModule, FileObject sourceFile, Guid objectESP, String conversionFormat, String outputFileName, Boolean attachFilesToObject) (+4)`
- `ICollection`1 AddConversionTasks(FileConversionModuleReferenceObject conversationModule, IReadOnlyCollection`1 sourceFiles, Guid objectESP, ConversionFormatReferenceObject conversionFormatReferenceObject, String outputFileName, Boolean attachFilesToObject, String prototypeFile, String conversionConfigurationSettings) (+9)`
- `ICollection`1 AddSecondaryRepresentationTasks(FileConversionModuleReferenceObject conversationModule, FileObject sourceFile, IReadOnlyCollection`1 secondaryRepresentationParamsList, Boolean attachSecondaryFilesToMasterFile)`
- `Queue`1 GetConversionTaskQueue(Int32 maxCount) (+1)`
- `Void UpdateTaskGroupStatus()`

### `TaskLinkClassType`
**Свойства:** Classes: TaskLinkTypes

### `TaskLinkObject`
**Свойства:** ChildObject: TaskObject, LinkType: TaskLinkType, ParentObject: BaseTaskObject, Delay: Int32
**Методы:**
- `Void UpdateParentObject()`

### `TaskLinkReference`
**Свойства:** Classes: TaskLinkTypes

### `TaskLinkReferenceObject`
**Свойства:** LinkType: TaskLinkType, ParentTask: TaskObject, Delay: Int32, ChildTask: TaskObject
**Методы:**
- `Void UpdateParentObject()`
- `Boolean Check()`

### `TaskLoadSettings`
**Свойства:** LoadControllerUser: Boolean, LoadOnBehalfUser: Boolean, Storage: ReferencesStorage

### `TaskObject`
**Свойства:** ParentTasksList: ReferenceObjectCollection, LinksToParentTasks: ReferenceObjectCollection`1
**Методы:**
- `IEnumerable`1 GetLinksFromChild()`
- `Boolean AddNewLink(TaskObject source, TaskLinkType linkType, Int32 delay)`
- `Void RemoveLinkToParentObject(BaseTaskObject parent)`
- `Void UpdatePositionByTask(BaseTaskObject task)`

### `TaskSettingFolder`
**Свойства:** Guid: Guid, IsVirtual: Boolean
**Методы:**
- `Int32 GetId()`
- `IEnumerable`1 GetMailItems(Filter filter)`
- `String GetFolderName()`
- `MailItemFolder GetMailItemFolder()`
- `IconImage GetIcon()`

### `TasksReference`
**Свойства:** Classes: TasksTypes
**Методы:**
- `Void Complete(TasksReferenceObject[] tasks)`
- `Void Uncomplete(TasksReferenceObject[] tasks)`
- `Void Cancel(TasksReferenceObject[] tasks, String comment)`
- `TasksReferenceObject[] GetSubtasksInProgress(TasksReferenceObject[] tasks)`
- `TasksReferenceObject[] GetSubtasksWithDeterminedStatus(TasksReferenceObject[] tasks, TaskStatus status)`
- `List`1 GetParentTasks(TasksReferenceObject[] tasks)`

### `TasksReferenceObject`
**Свойства:** Class: TasksType, IsTask: Boolean, IsTheme: Boolean, IsCompleted: Boolean, InProgress: Boolean, IsCancelled: Boolean, IsOverdue: Boolean, IsSupportedAutoCreationAssignments: Boolean, StatusType: TaskStatus, Percent: Double, AutoCalculation: Boolean, Name: StringParameter, TargetDate: DateTimeParameter, Progress: ProgressParameter, Description: StringParameter, Importance: Int32Parameter, LocalElement: BooleanParameter, NoAssignment: BooleanParameter, AssignmentsAutoCreationIsDisabled: BooleanParameter, Status: Int32Parameter, AutomaticCalculation: BooleanParameter, Executor: User, Assignments: ReferenceObjectCollection`1, LinkedMaterials: AnyReferenceLink
**Методы:**
- `Boolean CanChangeParameter(Parameter p, Object newValue)`
- `Boolean CanChangeStatus(TaskStatus status)`
- `Boolean CanChangeLink(LinkInfo link, ReferenceObject addObject, ReferenceObject removeObject)`
- `Boolean IsAutoCalculateProgress()`
- `AssignmentReferenceObject CreateAssignment(User executor, AssignmentType type, Boolean isBasic, Boolean shouldSaved) (+1)`
- `Void RecalculateProgressByAssignments()`
- `Boolean AppointExecutor(User newExecutor)`
- `Void Complete()`
- `Void Uncomplete()`
- `Void Cancel(String comment)`
- `TasksReferenceObject[] GetSubtasksInProgress()`
- `Void RecalculateProgress()`
- `Void ChangeAutoCalculation(Boolean autoCalculation)`
- `Boolean CanChangeAutoCalculation()`
- `Boolean CanChangePercent()`
- `Void ChangePercent(Double percent)`
- `ReferenceObject AddLinkedAssignment(ReferenceObject newLinkedObject)`
- `Boolean RemoveLinkedAssignment(ReferenceObject linkedObject)`
- `ReferenceObject AddLinkedMaterial(ReferenceObject newLinkedObject)`
- `Boolean RemoveLinkedMaterial(ReferenceObject linkedObject)`

### `TasksType`
**Свойства:** Classes: TasksTypes, IsTask: Boolean, IsTheme: Boolean

### `TasksTypes`
**Свойства:** Task: TasksType, Theme: TasksType

### `TaskTexts`
**Свойства:** Top: TaskText, Bottom: TaskText, Left: TaskText, Right: TaskText, Inside: TaskText
**Методы:**
- `TaskTexts Merge(TaskTexts other)`

### `TechnicalRequirementsDictionaryReference`
**Свойства:** Classes: TechnicalRequirementsDictionaryTypes

### `TechnicalRequirementsDictionaryType`
**Свойства:** Classes: TechnicalRequirementsDictionaryTypes, IsFolderRequirementsDictionaryReferenceObject: Boolean, IsTechnicalRequirementsDictionaryReferenceObject: Boolean

### `TechnicalRequirementsDictionaryTypes`
**Свойства:** FolderRequirementsDictionaryReferenceObject: TechnicalRequirementsDictionaryType, TechnicalRequirementsDictionaryReferenceObject: TechnicalRequirementsDictionaryType

### `TechnologyCadExchangeServiceClient`
**Свойства:** Info: ServiceInfo
**Методы:**
- `List`1 GetCadObjects(String documentFileName, String[] searchStrings, ClientCallContext context)` [has Async]
- `CadDimensionDto GetCadDimension(String documentFileName, String searchString, ClientCallContext context)` [has Async]
- `CadMeasureDto GetMeasures(String documentFileName, String[] searchStrings, String measuredParameter, ClientCallContext context)` [has Async]
- `CadObjectPropertyDto GetCadObjectProperty(CadObjectDto objectInfo, CadObjectPropertyDto propertyInfo, ClientCallContext context)` [has Async]
- `List`1 GetCadObjectProperties(CadObjectDto objectInfo, ClientCallContext context)` [has Async]
- `CadRoughnessDto GetCadRoughness(String draftFileName, String searchString, ClientCallContext context)` [has Async]
- `CadStructureDto GetCadStructureElements(String draftFileName, String[] structureElementTypes, ClientCallContext context)` [has Async]
- `CadObjectDto FindCadObject(String documentFileName, String searchString, ClientCallContext context)` [has Async]
- `CadObjectDto GetCadObject(String documentFileName, String searchString, ClientCallContext context)` [has Async]
- `List`1 GetVariables(String draftFileName, ClientCallContext context)` [has Async]
- `Void GetTextTable(CadObjectDto cadObjectInfo, ClientCallContext context)` [has Async]
- `Void SelectObject(String draftFileName, String searchString, ClientCallContext context)` [has Async]
- `Void SelectObjects(IntPtr controlHandle, AssemblyItemDto[] items, ClientCallContext context)` [has Async]
- `Void SubscribeSelectObjects(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void UnsubscribeSelectObjects(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void SubscribeGettingMeasures(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void UnsubscribeGettingMeasures(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void ChangeTree(IntPtr controlHandle, String configuration, ClientCallContext context)` [has Async]
- `Void ShowStepText(IntPtr controlHandle, String text, ClientCallContext context)` [has Async]
- `List`1 GetSelectionAllObjects(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void SetSelectionFragments(IntPtr controlHandle, Guid[] guids, ClientCallContext context)` [has Async]
- `Void SubscribeGettingCADSelection(IntPtr controlHandle, ClientCallContext context)` [has Async]
- `Void UnsubscribeGettingCADSelection(IntPtr controlHandle, ClientCallContext context)` [has Async]

### `TechnologyCadExchangeServiceServer`
**Свойства:** Info: ServiceInfo, SelectionCompleted: NotifyWriter`1, MeasuresCompleted: NotifyWriter`1, CADSelectionChanged: NotifyWriter`1
**Методы:**
- `ValueTask`1 GetCadObjects(String documentFileName, String[] searchStrings, ServerCallContext context)`
- `ValueTask`1 GetCadDimension(String documentFileName, String searchString, ServerCallContext context)`
- `ValueTask`1 GetMeasures(String documentFileName, String[] searchStrings, String measuredParameter, ServerCallContext context)`
- `ValueTask`1 GetCadObjectProperty(CadObjectDto objectInfo, CadObjectPropertyDto propertyInfo, ServerCallContext context)`
- `ValueTask`1 GetCadObjectProperties(CadObjectDto objectInfo, ServerCallContext context)`
- `ValueTask`1 GetCadRoughness(String draftFileName, String searchString, ServerCallContext context)`
- `ValueTask`1 GetCadStructureElements(String draftFileName, String[] structureElementTypes, ServerCallContext context)`
- `ValueTask`1 FindCadObject(String documentFileName, String searchString, ServerCallContext context)`
- `ValueTask`1 GetCadObject(String documentFileName, String searchString, ServerCallContext context)`
- `ValueTask`1 GetVariables(String draftFileName, ServerCallContext context)`
- `ValueTask GetTextTable(CadObjectDto cadObjectInfo, ServerCallContext context)`
- `ValueTask SelectObject(String draftFileName, String searchString, ServerCallContext context)`
- `ValueTask SelectObjects(IntPtr controlHandle, AssemblyItemDto[] items, ServerCallContext context)`
- `ValueTask SubscribeSelectObjects(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask UnsubscribeSelectObjects(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask SubscribeGettingMeasures(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask UnsubscribeGettingMeasures(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask ChangeTree(IntPtr controlHandle, String configuration, ServerCallContext context)`
- `ValueTask ShowStepText(IntPtr controlHandle, String text, ServerCallContext context)`
- `ValueTask`1 GetSelectionAllObjects(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask SetSelectionFragments(IntPtr controlHandle, Guid[] guids, ServerCallContext context)`
- `ValueTask SubscribeGettingCADSelection(IntPtr controlHandle, ServerCallContext context)`
- `ValueTask UnsubscribeGettingCADSelection(IntPtr controlHandle, ServerCallContext context)`
- `Void SetupSelectionCompleted(NotifyWriter`1 notify)`
- `Void SetupMeasuresCompleted(NotifyWriter`1 notify)`
- `Void SetupCADSelectionChanged(NotifyWriter`1 notify)`

### `TechnologyMacro`
**Свойства:** IsMethod: Boolean
**Методы:**
- `IEnumerable`1 GetReferences()`
- `Int32 GetUserCodeOffset()`

### `TechnologyPlugin`
**Методы:**
- `List`1 UpdateOperationNumbers(ReferenceObject techProcess, Int32 firstNumber, Int32 numerationStep, Int32 numberLength) (+1)`
- `List`1 UpdateStepNumbers(ReferenceObject techOperation, Int32 firstNumber, Int32 numerationStep, Int32 numberLength) (+1)`
- `List`1 GetToleranceLetters(ServerConnection connection, Int32 group) (+2)`
- `List`1 GetToleranceDigits(ServerConnection connection, Int32 group) (+2)`
- `List`1 GetToleranceDigitsInUse(ServerConnection connection, Double dimension, String letter, Int32 group) (+2)`
- `List`1 GetTolerance(ServerConnection connection, Double dimension, String letter, Int32 digit, Int32 group) (+2)`

### `Term`
**Свойства:** ParameterName: String, Operator: ComparisonOperator, AllQuantifier: Boolean, CaseInsensitive: Nullable`1, Value: Object, SkipUsingServerTermValue: Boolean, AsTerm: Term
**Методы:**
- `Void Clear()`
- `Boolean Match(Object obj, MacroContext formulaContext)`

### `TermGroup`
**Свойства:** Filter: Filter, IsRoot: Boolean, AsGroup: TermGroup, Item: TermGroupItem, Count: Int32, IsReadOnly: Boolean
**Методы:**
- `ReferenceObjectTerm AddTerm(LogicalOperator lo, ParameterInfo parameter, ComparisonOperator op, Object value, ParameterGroup[] groups) (+9)`
- `TermGroup AddGroup(LogicalOperator logicalOperator, TermGroupItemType termGroupItemType)`
- `TermGroup GroupTerms(IEnumerable`1 terms)`
- `List`1 Ungroup()`
- `List`1 RemoveEmptyGroups(Boolean recursive)`
- `List`1 Normalize()`
- `List`1 RemoveErrorItems(Boolean recursive)`
- `Boolean Match(Object obj, MacroContext formulaContext)`
- `String GetText()`
- `Int32 IndexOf(TermGroupItem item)`
- `Void Insert(Int32 index, TermGroupItem item)`
- `Void Exchange(TermGroupItem firstItem, TermGroupItem secondItem, Boolean exchangeLogicalOperator)`
- `Void RemoveAt(Int32 index)`
- `Void Add(TermGroupItem item)`
- `Void Clear()`
- `Boolean Contains(TermGroupItem item)`
- `Void CopyTo(TermGroupItem[] array, Int32 arrayIndex)`
- `Boolean Remove(TermGroupItem item)`
- `IEnumerator`1 GetEnumerator()`
- `Void ReplaceVariablesByValues()`

### `TermGroupItem`
**Свойства:** IsGroup: Boolean, IsTerm: Boolean, IsReferenceObjectTerm: Boolean, ItemType: TermGroupItemType, AsGroup: TermGroup, AsTerm: Term, AsReferenceObjectTerm: ReferenceObjectTerm, LogicalOperator: LogicalOperator, Not: Boolean, Owner: TermGroup, IsError: Boolean
**Методы:**
- `Void ReplaceVariablesByValues()`
- `Boolean Match(Object obj, MacroContext formulaContext)`
- `Boolean IsOwnerOfSearchRule(SearchRule searchRule, Boolean recursive)`

### `TextElementReferenceObject`
**Методы:**
- `String GetTestValue(String parameter)`

### `TextFieldInputDialog`
**Свойства:** TypeName: String, Text: InArgument`1, LineCount: InArgument`1

### `TextPropertyData`
**Свойства:** Value: String

### `TextRemarkObject`
**Свойства:** Detail: StringParameter, Files: ReferenceObjectCollection
**Методы:**
- `ReferenceObject AddFile(ReferenceObject newLinkedObject)`
- `Boolean RemoveFile(ReferenceObject linkedObject)`

### `TextSetting`
**Свойства:** Indent: Double, IsVisible: Boolean, SourceType: TextSourceType, Parameter: String, Formula: FormulaMacro, UniversalPath: String, Format: String, Font: FontSetting

### `TextToColorConverter`
**Методы:**
- `Void TrySetColor(String text, Action`1 setter, Nullable`1 defaultValue) (+1)`
- `String GetText(Nullable`1 color) (+1)`

### `TFlexCadContext`
**Свойства:** Keys: ICollection`1, Values: ICollection`1, Item: TFlexCadVariableValue, Count: Int32
**Методы:**
- `Byte[] GetData()`
- `Boolean TryGetReal(String name, Double& real)`
- `Boolean TryGetText(String name, String& text)`
- `Void SetReal(String name, Double real)`
- `Void SetText(String name, String text)`
- `Void Add(String name, TFlexCadVariableValue variable)`
- `Boolean ContainsKey(String name)`
- `Boolean Remove(String name)`
- `Boolean TryGetValue(String name, TFlexCadVariableValue& variable)`
- `Void Clear()`
- `IEnumerator`1 GetEnumerator()`

### `TFlexCadConversionModuleReferenceObject`
**Свойства:** PathInRegistry: StringParameter, CADVersionFrom: StringParameter, CADVersionTo: StringParameter, LinkApplicationIntegrationConfigurationRules: ApplicationsRelationsProfileReferenceObject

### `TFlexCadVariableValue`
**Свойства:** Text: String, Real: Double

### `TFlexPageInfo`
**Свойства:** Name: String, PageType: TFlexPageType, Index: Int32, Visible: Boolean, Properties: PageProperties

### `TflexParameterValueGeneratorData`
**Свойства:** ObjectGuid: Guid

### `TflexRepositoryAnyReferenceObjectLinkEditXMLData`
**Свойства:** DataSource: Int32, ParameterGuid: String, ReferencesWithFilters: List`1

### `TflexRepositoryItemXMLData`
**Свойства:** UserControlName: String, ParameterName: String, Parameter: ParameterInfo, ParameterGroup: ParameterGroup
**Методы:**
- `String ConvertToString(ServerConnection connection, TflexRepositoryItemXMLData data)`
- `TflexRepositoryItemXMLData ConvertFromString(ServerConnection connection, String data, String& controlName)`
- `String GetUserControlName(String data)`
- `Boolean Validate(Boolean throwOnError)`
- `ParameterGroup GetParameterGroup()`
- `Guid GetGuid(String guid)`

### `TflexRepositoryLinkEditComboBoxXMLData`
**Свойства:** ReferenceGuid: String, ReferenceFilterGuid: String, ParameterGuid: String, Editable: Boolean, SavePath: Boolean, LevelPath: Int32, SeparatorPath: String, IsLinkControl: Boolean, AutoComplete: Boolean, PrototypeMode: Boolean, PopupContentViewName: String, AllowClear: Boolean, AllowSelectFromDialog: Boolean, Parameter: ParameterInfo
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `TflexRepositoryMultiTextEditXMLData`
**Свойства:** FormatParameterGuid: Guid

### `TflexRepositorySelectFromDialogEditData`
**Свойства:** AsseblyName: String, DialogClassName: String, AllowEditControlValue: Boolean
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `TflexRepositorySelectReferenceObjectStageData`
**Свойства:** ReferenceGuid: Guid, ShowNullStage: Boolean, PathToParameterContainingReferenceId: String, EditValueType: String
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `TflexRepositoryUnitValueEditXMLData`
**Свойства:** DataSource: Int32, ParameterPath: String, StoreInBaseUnit: Boolean, ShowChooseButton: Boolean, ShowClearButton: Boolean

### `TflexSelectReferenceParameterGuidControlData`
**Свойства:** ReferenceGuid: Guid, PathToParameterContainingReferenceId: String, LinkParameterGuid: Guid, ShowAll: Boolean, ShowParameters: Boolean, ShowOnlyUserParameters: Boolean, ShowLinks: Boolean, ShowOnlyToOneLinks: Boolean, ShowOnlyToManyLinks: Boolean, ShowTablesToMany: Boolean, ParameterTypeId: Int32, ShowSignatures: Boolean
**Методы:**
- `Boolean Validate(Boolean throwOnError)`

### `TflexSelectReferenceTypeGuidControlData`
**Свойства:** ReferenceGuid: Guid, ObjectListPath: String, LinkParameterGuid: Guid, ParameterPath: String, ForbidSelectAbstractClass: Boolean, ConsiderSpecificClasses: Boolean, SpecificClasses: List`1, UseOnlySpecificClasses: Boolean
**Методы:**
- `ReferencePath GetOldValue(ParameterGroup parameterGroup)`
- `Boolean Validate(Boolean throwOnError)`

### `TimeChartPrintingProfile`
**Свойства:** PageNumberPosition: PageNumberPosition, FitContentMode: FitContentMode, Class: PrintingProfileType, Name: StringParameter, Default: BooleanParameter, Shared: BooleanParameter, Begin: DateTimeParameter, End: DateTimeParameter, PageWidth: DoubleParameter, PageHeight: DoubleParameter, Landscape: BooleanParameter, LeftMargin: DoubleParameter, RightMargin: DoubleParameter, TopMargin: DoubleParameter, BottomMargin: DoubleParameter, PageNumberPositionParameter: Int32Parameter, FitContentModeParameter: Int32Parameter, TransparentBackground: BooleanParameter, HighlightToday: BooleanParameter, RepeatHeader: BooleanParameter, PrintLegend: BooleanParameter, PrintTimeChart: BooleanParameter, CopyCount: Int32Parameter, Resolution: Int32Parameter, PageHeader: StringParameter, PageFooter: StringParameter, FirstPageHeader: StringParameter, FirstPageFooter: StringParameter, LastPageHeader: StringParameter, LastPageFooter: StringParameter, DifferentFirstPage: BooleanParameter, DifferentLastPage: BooleanParameter

### `TimeFieldInputDialog`
**Свойства:** TypeName: String

### `TimeIntervalExt`
**Методы:**
- `DateTimeInterval ToDateTimeInterval(TimeInterval interval, Boolean includeStart, Boolean includeEnd) (+1)`

### `TimeIntervalManager`
**Свойства:** Intervals: IReadOnlyCollection`1
**Методы:**
- `Boolean IsExists(TimeInterval newInterval)`
- `IEnumerable`1 Merge(TimeInterval newInterval)`

### `TimeSpanRepositoryItemXMLData`
**Свойства:** ShowYears: Boolean, ShowMonths: Boolean, ShowDays: Boolean, ShowHours: Boolean, ShowMinutes: Boolean, ShowSeconds: Boolean

### `TimeTrigger`
**Свойства:** StartTime: DateTime, Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `TitleSettings`
**Свойства:** Name: String, Dock: TitleDock, Alignment: TitleAlignmentType, TitleLinkType: TitleLinkType, Group: String

### `ToAnyStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean, CanContainMultipleReferencesDetalization: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `ToCharacteristicsLinkStructure`
**Свойства:** Type: StructureGroupTypes, ShowAddCommandLock: Nullable`1, ShowRemoveCommandLock: Nullable`1

### `ToleranceModel`
**Свойства:** BasicSize: Double, EngineeringFit: String, LowerDeviation: Double, UpperDeviation: Double, Quality: Int32
**Методы:**
- `List`1 GetToleranceLetters(ServerConnection connection, Int32 group) (+1)`
- `List`1 GetToleranceDigits(ServerConnection connection, Int32 group) (+1)`
- `List`1 GetToleranceDigitsInUse(ServerConnection connection, Double dimension, String letter, Int32 group) (+1)`
- `List`1 GetTolerance(ServerConnection connection, Double dimension, String letter, Int32 digit, Int32 group) (+1)`

### `ToleranceReference`
**Методы:**
- `List`1 GetToleranceLetters()`
- `List`1 GetToleranceDigits()`
- `List`1 GetToleranceDigitsInUse(Double dimension, String letter)`
- `List`1 GetTolerance(Double dimension, String letter, Int32 digit)`

### `ToMailField`
**Методы:**
- `List`1 GetComparisonOperators()`
- `Object Parse(ServerConnection connection, String str, IFormatProvider provider, ComparisonOperator operator)`

### `Tool`
**Свойства:** Code: String, CursorPosition: Int32, ElementName: String, IsFolder: Boolean, IsGroupedMethod: Boolean

### `ToolGroup`
**Свойства:** IsFolder: Boolean, IsGroupedMethod: Boolean, HasChildren: Boolean, Icon: IconImage, HasOverloads: Boolean, Name: String, Children: Collection`1
**Методы:**
- `ToolGroup FindByName(String name)`

### `ToolGroupHeader`
**Свойства:** Name: String, Icon: IconImage, GroupType: Type, IsStatic: Boolean, IsNeutral: Boolean, SubGroups: ToolGroupHeader[]

### `ToolGroupStaticHeader`
**Свойства:** IsStatic: Boolean

### `ToolsLoader`
**Методы:**
- `ToolGroup Load(ToolGroupHeader header, Language language)`
- `Boolean TryFillHeaderName(ToolGroupHeader header, Type groupType, TypeInfoAttribute currentLanguageAttribute, Type linkedType, Language language, String& headerName)`
- `Tool CreateToolItem(InfoAttribute attribute, MemberInfo member, Boolean isStatic)`

### `ToolsManagerData`
**Свойства:** Favorites: ToolGroup, Language: String, MacroLanguage: Language, References: List`1

### `ToOneStructure`
**Свойства:** Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `TransliteExtensions`
**Методы:**
- `String ToTranslit(Char c) (+1)`

### `Trigger`
**Свойства:** Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `TypeHelper`
**Методы:**
- `Boolean CanConvert(Type sourceType, Type destinationType)`
- `Object Convert(Object value, Type type, Boolean throwOnError, Boolean useBase64) (+1)`
- `Boolean TryConvert(Object value, Type type, Object& result, Boolean useBase64)`
- `Object GetDefaultValue(Type type)`
- `Object GetDOCsDefaultValue(Type type)`
- `Boolean IsDefaultValue(Object value)`
- `Object ParseExpression(String value)`

### `TypeInfoAttribute`
**Свойства:** Language: Language, Name: String, Key: String, NoIndexBaseClasses: Boolean

### `TypesRelationsReference`
**Свойства:** Classes: TypesRelationsTypes

### `TypesRelationsReferenceObject`
**Свойства:** Class: TypesRelationsType, Name: StringParameter, AppTypeName: StringParameter, NomenclatureType: StringParameter, LinkToFiles: StringParameter, ReferenceObjectType: Guid, PathForLinkToFiles: StringParameter

### `TypesRelationsType`
**Свойства:** Classes: TypesRelationsTypes, IsTypesRelationsClass: Boolean

### `TypesRelationsTypes`
**Свойства:** TypesRelationsClass: TypesRelationsType

### `TypicalConfigurationSettingsObject`
**Свойства:** Configurator: Configurator, Class: TypicalConfigurationSettingsType, Name: StringParameter, ConfiguratorGuid: GuidParameter, Data: StringParameter

### `TypicalConfigurationSettingsReference`
**Свойства:** Classes: TypicalConfigurationSettingsTypes
**Методы:**
- `TypicalConfigurationSettingsObject Find(String name)` [has Async]

### `TypicalConfigurationSettingsType`
**Свойства:** Classes: TypicalConfigurationSettingsTypes, IsTypicalConfiguration: Boolean

### `TypicalConfigurationSettingsTypes`
**Свойства:** TypicalConfiguration: TypicalConfigurationSettingsType

### `TypicalRepresentationsReference`
**Свойства:** Classes: TypicalRepresentationsTypes

### `TypicalRepresentationsReferenceObject`
**Свойства:** Class: TypicalRepresentationsType, Name: StringParameter, PresentationCode: StringParameter

### `TypicalRepresentationsType`
**Свойства:** Classes: TypicalRepresentationsTypes, IsTypicalRepresentationsReferenceObject: Boolean, IsSecondaryRepresentationReferenceObject: Boolean, IsMasterFileReferenceObject: Boolean

### `TypicalRepresentationsTypes`
**Свойства:** TypicalRepresentationsReferenceObject: TypicalRepresentationsType, SecondaryRepresentationReferenceObject: TypicalRepresentationsType, MasterFileReferenceObject: TypicalRepresentationsType

### `UndoBlock`
**Свойства:** Name: String
**Методы:**
- `Boolean CanClose()`

### `UndoBlockBase`
**Свойства:** Name: String, State: BlockState, AllowAddAction: Boolean
**Методы:**
- `Boolean CanClose()`
- `Void Undo()`
- `Void Redo()`
- `Void Close()`

### `UndoManager`
**Свойства:** ClosedBlocks: List`1, RestoredBlocks: List`1, BlockOpened: Boolean, Saving: Boolean
**Методы:**
- `Void SetReference(Reference reference)`
- `Void StartUndoBlock(String blockName)`
- `Void EndUndoBlock()`
- `Void CancelUndoBlock()`
- `Void Undo()`
- `Void Redo()`
- `Void CreateCustomUndoBlock(String blockName, Action undoAction, Action redoAction)`

### `UndoManagerActionHandler`
**Методы:**
- `Void Invoke(Object sender, UndoManagerEventArgs args)`
- `IAsyncResult BeginInvoke(Object sender, UndoManagerEventArgs args, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `UndoManagerExtensions`
**Методы:**
- `T RunOperationWithUndo(UndoManager undoManager, String blockName, Func`2 operation, TArg arg) (+4)`

### `UniqueIndex`
**Свойства:** Group: ParameterGroup, Id: Int32, Guid: Guid, Name: String, Parameters: ReadOnlyCollection`1

### `UniqueIndexBuilder`
**Свойства:** IsAdded: Boolean, IsModified: Boolean, ParameterGroup: ParameterGroup, Reference: ReferenceInfo, Index: UniqueIndex, Name: String, Parameters: ParameterCollection
**Методы:**
- `UniqueIndex Save()` [has Async]
- `Boolean Delete(UniqueIndex index)` [has Async]

### `UniqueIndexCheckResult`
**Свойства:** Index: UniqueIndex, ObjectId: Int32, IsObjectDeleted: Boolean, AddedClientView: ClientView
**Методы:**
- `ReferenceObject GetObject()`

### `UniqueObjectCheckParameters`
**Свойства:** Class: ClassObject, Values: IDictionary`2, CheckResult: UniqueIndexCheckResult, ExistingObject: ReferenceObject

### `UniqueObjectCheckResult`
**Свойства:** Object: ReferenceObject, ExistingObject: ReferenceObject, IsExistingInBatch: Boolean, IsObjectDeleted: Boolean, AddedClientView: ClientView, Index: UniqueIndex
**Методы:**
- `String GetErrorDetails()`

### `Unit`
**Свойства:** Class: UnitType, Name: StringParameter, ShortName: StringParameter, RCUMCode: Int32Parameter, Description: StringParameter, InternationalName: StringParameter, IsBase: Boolean, Coefficient: DoubleParameter, Offset: SingleParameter
**Методы:**
- `Double Convert(Double value, Unit unit)`

### `Unit`
**Свойства:** FullName: String, ShortName: String, TypeName: String

### `UnitData`
**Свойства:** FullName: String, ShortName: String, TypeName: String

### `UnitReference`
**Свойства:** Instance: UnitReference, Classes: UnitTypes
**Методы:**
- `Double Convert(Double value, Unit fromUnit, Unit toUnit)`

### `UnitType`
**Свойства:** Classes: UnitTypes
**Методы:**
- `List`1 GetUnits()` [has Async]
- `Unit GetBaseUnit()` [has Async]
- `Void SetBaseUnit(Unit unit)` [has Async]

### `UnitTypes`
**Свойства:** Instance: UnitTypes, Length: UnitType, Area: UnitType, Volume: UnitType, Weight: UnitType, Temperature: UnitType, Angle: UnitType, Velocity: UnitType, AngularVelocity: UnitType, Density: UnitType, Pressure: UnitType, Energy: UnitType, Power: UnitType, Voltage: UnitType, Amperage: UnitType, Resistance: UnitType, Electrocapacity: UnitType, Frequency: UnitType, Time: UnitType

### `User`
**Свойства:** FirstName: StringParameter, LastName: StringParameter, Patronymic: StringParameter, ShortName: StringParameter, Login: StringParameter, Password: PasswordParameter, MasterPassword: PasswordParameter, ForbidChangePassword: Boolean, PasswordExpirationDate: DateTimeParameter, Sex: Int32Parameter, Birthday: DateTimeParameter, Email: StringParameter, MailSendType: ByteParameter, MailSendMode: MailSendMode, BusinessPhone: StringParameter, InternalPhone: StringParameter, MobilePhone: StringParameter, HomePhone: StringParameter, Fax: StringParameter, BlockingDate: DateTimeParameter, BlockingReason: StringParameter, Sid: StringParameter, SidOnly: BooleanParameter, Photo: ImageParameter, FirstWorkDay: DateTimeParameter, MailSettings: StringParameter, Signature: ImageParameter, SharedWorkspace: BooleanParameter, CachingFileServer: CachingFileServerObject, IsCurrent: Boolean, IsSystem: Boolean
**Методы:**
- `Boolean ChangePassword(String oldPassword, String newPassword, Boolean changeOnLogin)`
- `Boolean SetMasterPassword(String masterPassword)`
- `Boolean IsMasterPasswordExists()` [has Async]
- `Boolean SetPasswordFromMasterPassword()` [has Async]
- `CachingFileServerObject GetCurrentCachingFileServer()` [has Async]
- `Void RestoreSettings(String application)`
- `List`1 GetAllInternalUsers(Boolean reloadChildren)`
- `List`1 GetAllInternalUsersAndGroups(Boolean reloadChildren)`
- `User LockAccount(Action`1 actionOnDisconnectedUser) (+1)`
- `User UnlockAccount()`

### `UserDialogObj`
**Методы:**
- `UserDialogObj CreateInstance(UserDialogObject object, MacroContext context)`

### `UserDialogObjectAccessor`
**Свойства:** Caption: String [RU: Заголовок], ShowConfirmationOnCancel: Boolean [RU: ПоказыватьПодтверждениеПриОтмене]
**Методы:**
- `UserDialogObjectAccessor CreateInstance(UserDialogObject object, MacroContext context)`
- `Boolean Show()` [RU: ПоказатьДиалог]

### `UserDialogsReference`
**Свойства:** Classes: UserDialogClassTree
**Методы:**
- `UserDialogObject Find(User user, String dialogTypeName) (+1)` [has Async]

### `UserDialogType`
**Свойства:** IsUserDialog: Boolean, IsUserPanel: Boolean

### `UserEvent`
**Свойства:** Events: EventCollection, Name: String, Button: UserEventButtonInfo, IsAdded: Boolean, IsModified: Boolean
**Методы:**
- `Boolean Save()` [has Async]
- `Boolean Delete()` [has Async]

### `UserEventButtonInfo`
**Свойства:** Event: UserEvent, Text: String, MenuCaption: String, Hint: String, ValidateMethod: String, ShortcutKeys: String, FilterEnable: Filter, FilterVisible: Filter, Position: PositionInMenu, DisplayMode: CommandDisplayMode, EditObject: Boolean, AllowedForUsers: Boolean, XmlUsers: Int32[], XmlUsersIds: Guid[], Users: UserReferenceObject[], ExecuteForEachObject: Boolean, Icon: IconImage, PopupIcon: IconImage, IconBytes: Byte[], PopupIconBytes: Byte[]
**Методы:**
- `Boolean AllowedForUser(Int32 userId)` [has Async]

### `UserFolder`
**Свойства:** AsUserFolder: UserFolder
**Методы:**
- `Boolean Add(ReferenceObject referenceObject) (+1)`
- `Boolean Remove(ReferenceObject referenceObject) (+1)`

### `UserFolderStructure`
**Свойства:** ShowCreateCommandLock: Nullable`1, ShowDeleteCommandLock: Nullable`1, Type: StructureGroupTypes, IsLinkOrParameterGroup: Boolean
**Методы:**
- `String AppendToPath(String path, StructureGroup structureGroup)`

### `UserObjectAccessor`
**Свойства:** Name: String [RU: Наименование], Description: String [RU: Наименование], FirstName: String [RU: Наименование], LastName: String [RU: Наименование], Patronymic: String [RU: Наименование], ShortName: String [RU: Наименование], Login: String [RU: Наименование]
**Методы:**
- `UserObjectAccessor CreateInstance(User object, MacroContext context)`

### `UserReference`
**Свойства:** Instance: UserReference, Classes: UserTypes
**Методы:**
- `List`1 GetAllUsersGroup()` [has Async]
- `List`1 GetAllUsers()` [has Async]
- `IEnumerable`1 FindUsersAndGroups(IEnumerable`1 objects)`
- `Boolean CanDeleteHierarchyLink(ComplexHierarchyLink link)`
- `User FindUser(String fullName)` [has Async]

### `UserReferenceObject`
**Свойства:** Class: UserType, IsUser: Boolean, IsGroup: Boolean, FullName: StringParameter, Description: StringParameter, WorkTimeManager: WorkTimeManager, CurrentWorkTimeElements: IEnumerable`1, Calendar: CalendarReferenceObject, CalendarChanges: IEnumerable`1
**Методы:**
- `ReferenceObject BeginChanges(ClassObject newClass)` [has Async]
- `List`1 GetAllInternalUsers(Boolean reloadChildren) (+1)` [has Async]
- `List`1 GetAllInternalUsersAndGroups(Boolean reloadChildren) (+1)`
- `Void UpdateWorkTimeElements()`
- `List`1 GetWorkTimeElements()`
- `Void ClearWorkTimeElements()`

### `UserRefObj`
**Методы:**
- `UserRefObj CreateInstance(User object, MacroContext context)`

### `UsersGroup`
**Свойства:** PostAddress: StringParameter, ContactPhone: StringParameter, Email: StringParameter, Sid: StringParameter, CachingFileServer: CachingFileServerObject

### `UserType`
**Свойства:** Classes: UserTypes, IsGroup: Boolean, IsActiveDirectoryGroup: Boolean, IsSubdivision: Boolean, IsEnterprise: Boolean, IsDivision: Boolean, IsUser: Boolean, IsEmployee: Boolean, IsDisconnectedUser: Boolean, IsOutsideUser: Boolean, IsAdministrator: Boolean, IsPost: Boolean, IsProductionUnit: Boolean, IsShop: Boolean, IsArea: Boolean, IsWorkplace: Boolean, IsWorkcenter: Boolean, IsWorkflowRole: Boolean, IsRole: Boolean

### `UserTypes`
**Свойства:** GroupBaseType: UserType, ActiveDirectoryGroup: UserType, SubdivisionType: UserType, EnterpriseType: UserType, DivisionType: UserType, UserBaseType: UserType, EmployerType: UserType, DisconnectedUserType: UserType, OutsideUserType: UserType, AdministratorType: UserType, PostBaseType: UserType, ProductionUnitType: UserType, ShopType: UserType, AreaType: UserType, WorkplaceType: UserType, WorkflowRoleType: UserType

### `ValueChangedFieldInputDialog`
**Свойства:** TypeName: String, Code: InArgument`1

### `ValueFieldInputDialog`
**Свойства:** FieldName: InArgument`1, IsRequired: Boolean

### `ValueList`
**Методы:**
- `ValueList CreateInstance(ParameterValueList valueList)`

### `ValueListItem`
**Методы:**
- `ValueListItem CreateInstance(ListValue listValue)`

### `ValueListItemAccessor`
**Свойства:** Name: String [RU: Наименование], Value: Object [RU: Значение], Icon: IconObj, Иконка: Иконка [RU only]

### `Variable`
**Свойства:** Name: String, Value: String

### `Variable`
**Свойства:** Name: String, Value: Object, Expression: String, Description: String, IsExternal: Boolean, GroupName: String, Hidden: Boolean, Unit: Unit, IsModify: Boolean, Owner: VariableCollection
**Методы:**
- `Void SetModify()`
- `Void CopyFrom(Variable other)`

### `Variable`
**Свойства:** Connection: ServerConnection, Variables: VariableCollection, Name: String, Comment: String, IsArray: Boolean, Type: Type, AllowNullValue: Boolean, IsNull: Boolean, Value: Object
**Методы:**
- `Void SetDefaultValue()`

### `Variable`1`
**Свойства:** Value: T

### `Variable`1`
**Свойства:** Type: Type, IsNull: Boolean, Value: T
**Методы:**
- `Void SetDefaultValue()`

### `VariableAccessor`
**Свойства:** Item: Object

### `VariableArray`1`
**Свойства:** Value: T[], IsArray: Boolean, Type: Type, IsNull: Boolean
**Методы:**
- `T[] GetConvertedArray(Object value)`
- `Void SetDefaultValue()`

### `VariableData`
**Свойства:** Name: String, Expression: String, Description: String, IsExternal: Boolean, GroupName: String, Hidden: Boolean, Unit: UnitData

### `VariableInfo`
**Свойства:** DisplayName: String, VariableName: String, Type: Type, Value: String, DefaultType: DefaultSupportedType, Description: String, IsEmbed: Boolean, IsContext: Boolean, ContextVariableInfo: ContextVariableInfo, IsPath: Boolean, Path: StructurePath, Image: Object, ImageResource: String, IsImageLoad: Boolean, GroupName: String, Reference: Guid, Classes: Guid[], IsReferenceObject: Boolean, IsHierarchyLink: Boolean, IsMultiple: Boolean, VariableDefaultType: DefaultSupportedType
**Методы:**
- `VariableInfo Create(String variableName, Type variableType) (+7)`
- `Boolean IsEmbedVariable(String variableName)`
- `Boolean IsContextVariable(String variableName)`
- `Boolean IsPathVariable(String variableName)`
- `Object GetValue(ActivityContext context) (+1)`
- `Object GetAccessorValue(ActivityContext context) (+1)`

### `VariableManager`
**Методы:**
- `Void SetFilterVariables(Filter filter, ActivityContext context)`
- `Boolean IsSupportVariableType(Type variableType)`
- `Boolean IsEqualTypes(Type filterType, Type variableType)`
- `List`1 GetAvailableVariables(ActivityContext context)`

### `VariablePathElement`
**Свойства:** VariableInfoString: String, ReferenceGuid: Guid, IsContext: Boolean, VariableInfo: VariableInfo, IsContextReference: Boolean, DefaultType: DefaultSupportedType, Type: Type
**Методы:**
- `ObjectValue GetValue(StructurePathContext context)`
- `Boolean IsEqual(PathElement pathElement)`

### `VariableValueChangedDelegate`
**Методы:**
- `Void Invoke(Variable variable, Object oldValue)`
- `IAsyncResult BeginInvoke(Variable variable, Object oldValue, AsyncCallback callback, Object object)`
- `Void EndInvoke(IAsyncResult result)`

### `VariantReplaceActionReferenceObject`
**Свойства:** IsAutomatic: Boolean, VariantObj: NomenclatureObject

### `ViewerService`
**Свойства:** OperationTimeout: TimeSpan
**Методы:**
- `Int32 GetNewId()`
- `ViewProviderProxy GetCallback(ServiceCallbackOwnerInfo ownerInfo, Process& process) (+1)`
- `Void CloseProcess(Process process)`
- `CADServiceProxy GetCADService(ServiceCallbackOwnerInfo ownerInfo)`
- `TechnologyCadExchangeServiceClient GetTechnologyCadExchangeService(ServiceCallbackOwnerInfo ownerInfo, String assemblyPath, String assemblyName)`

### `ViewProviderProxy`
**Свойства:** IsAvailable: Boolean
**Методы:**
- `IntPtr ShowFile(Int32 id, ShowFileContext context)`
- `Void CloseFilePreviews(String file)`
- `Void SetControlSize(Int32 id, Int32 width, Int32 height)`
- `Byte[] GenerateReport(String moduleName, String className, Byte[] context)`
- `Byte[] ExchangePluginData(String pluginModuleName, String pluginClassName, Int32 controlId, Byte[] data)`
- `Int32 GetImagePageCount(Int32 id, String filePath)`
- `Byte[] GetPreviewImage(Int32 id, String filePath, Int32 pageIndex)`
- `Boolean IsInstalledPreviewProgram(Int32 id, String extension, Boolean isAnyCPUMode)`
- `String GetCadServiceAddress()`
- `Boolean IsSupportSaving(Int32 id)`
- `Boolean SaveAs(Int32 id, String filePath)`
- `Boolean IsDocumentChandged(Int32 id)`
- `Void SaveChanges(Int32 id)`
- `String GetFilePreviewInformation(Int32 id)`
- `Void Print(Int32 id)`
- `Tuple`2 ExecuteDocumentRequest(Int32 id, FilePreviewRequest request)`
- `String GetMeasureServiceAddress(String assemblyPath, String assemlbyName)`

### `VisualSetting`
**Свойства:** Radius: Double, BorderColor: Int32, BorderThickness: Double, UnderlaymentColor: Nullable`1, CanChangeBorderParams: Boolean, CanChangeRadius: Boolean

### `WaitingDialogAccessor`
**Методы:**
- `Void Show(String caption, Boolean canCancel)` [RU: Показать]
- `Void Hide()` [RU: Скрыть]
- `Boolean NextStep(String description, Nullable`1 progress) (+1)` [RU: Скрыть]
- `Boolean СледующийШаг(String текст, Nullable`1 прогресс)` [RU alternative]

### `WebConfiguration`
**Свойства:** RootMenuLink: MenuLinkGroup, IsVisibleControlPanel: Boolean, AsWebConfiguration: WebConfiguration
**Методы:**
- `ClientConfiguration ToServerData()`
- `Void LoadLinks()`

### `WebConnectionSettings`
**Свойства:** ApplicationDirectory: String, SystemUserName: String, SystemPassword: String
**Методы:**
- `String CreateConnectionData()`
- `ServerConnection CreateConnection(ConnectionParameters connectionParameters)`
- `String Serialize()`
- `WebConnectionSettings Deserialize(String data)`

### `WeekEditRepositoryItemXMLData`
**Свойства:** UseStartOfWeek: Boolean

### `WeeklyObject`
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `WeekTrigger`
**Свойства:** Item: Boolean, Days: Boolean[], WeekInterval: Int32, Name: String
**Методы:**
- `DateTime GetExecuteTime(DateTime lastExecuteTime)`

### `WhileActivityBase`
**Свойства:** Condition: Activity`1, Body: Activity

### `WindowAccessor`
**Свойства:** Name: String [RU: Наименование]
**Методы:**
- `Void Reload()` [RU: Обновить]
- `Void ReloadItem(String name)` [RU: ОбновитьЭлементУправления]
- `LayoutItemObj FindItem(String name)` [RU: ОбновитьЭлементУправления]
- `ЭлементУправления НайтиЭлементУправления(String name)` [RU alternative]

### `WindowObj`
**Методы:**
- `WindowObj CreateInstance(IWindow window, MacroContext context)`

### `WindowsInCompatibilityMode`
**Свойства:** Connection: ServerConnection
**Методы:**
- `WindowsInCompatibilityMode Get(ServerConnection connection)` [has Async]
- `Boolean OpenInCompatibilityMode(Guid windowId)`
- `Boolean OpenReferenceInCompatibilityMode(Int32 referenceId)`
- `Boolean OpenWorkingPageInCompatibilityMode(Int32 workingPageId)`
- `List`1 GetWindows()`
- `Void Reload()` [has Async]
- `Void Save(ICollection`1 windowsInCompatibilityMode)`
- `Void Clear()`

### `WorkflowRole`
**Методы:**
- `List`1 GetAllInternalUsers(Boolean reloadChildren)`
- `List`1 GetAllInternalUsersAndGroups(Boolean reloadChildren)`

### `WorkingAreaDesktopObject`
**Свойства:** UserPageData: ByteArrayParameter
**Методы:**
- `Void DeleteWithAllObjects()`

### `WorkingAreaFolder`
**Свойства:** IsFolderTypeTreeChildren: Boolean
**Методы:**
- `WorkingAreaShortcut CreateShortcutToReference(Reference reference)`
- `WorkingAreaShortcut CreateShortcutToWindow(Int32 windowType, String windowName, IconImage windowIcon)`
- `WorkingAreaShortcut CreateShortcutToReferenceObject(ReferenceObject referenceObject)`
- `WorkingAreaShortcut CreateShortcutToMacros(Macro macros, String macrosName)`
- `WorkingAreaShortcut CreateShortcutToSearchQuery(SearchQueryObject searchQuery)`
- `WorkingAreaShortcut CreateShortcutToWorkPage(WorkingPage workingPage)`

### `WorkingAreaReference`
**Свойства:** Instance: WorkingAreaReference, PrivateFolder: WorkingAreaFolder, CommonFolder: WorkingAreaFolder, Classes: WorkingAreaTypes

### `WorkingAreaReferenceObject`
**Свойства:** Class: WorkingAreaType, Name: StringParameter, ObjectType: Int32Parameter, Icon: IconParameter, WorkingAreaIcon: IconImage

### `WorkingAreaShortcut`
**Свойства:** ReferenceGuid: GuidParameter, MacrosGuid: GuidParameter, WorkPageGuid: GuidParameter, MacrosName: StringParameter, FilterParameter: StringParameter, LinkedReference: ReferenceInfo, LinkedObject: ReferenceObject, WorkingAreaIcon: IconImage, Filter: Filter, ToReference: Boolean, ToReferenceObject: Boolean, ToMacros: Boolean, ToWorkPage: Boolean, ToSearchQuery: Boolean

### `WorkingAreaType`
**Свойства:** Classes: WorkingAreaTypes, IsWorkingAreaFolder: Boolean, IsWorkingAreaShortcut: Boolean, IsWorkingAreaDesktop: Boolean

### `WorkingAreaTypes`
**Методы:**
- `WorkingAreaType GetWorkingAreaFolderClass()`
- `WorkingAreaType GetWorkingAreaShortcutClass()`
- `WorkingAreaType GetWorkingAreaDesktopClass()`

### `WorkingFolderInfo`
**Свойства:** Id: Int32, WorkingFolder: String, PendingWorkingFolder: String, PendingStatus: WorkingFolderPendingStatus, Changing: Boolean, IsModified: Boolean
**Методы:**
- `Void BeginChanges()`
- `Void CancelChanges()`
- `List`1 GetClientWorkingFolders(ServerConnection connection, IEnumerable`1 clientViews)` [has Async]
- `Void EndChanges(IEnumerable`1 workingFolders)` [has Async]

### `WorkingFolderPendingStatusExtensions`
**Методы:**
- `String GetName(WorkingFolderPendingStatus status)`
- `Byte[] GetIconBytes(WorkingFolderPendingStatus status)`
- `String GetIconKey(WorkingFolderPendingStatus status)`

### `WorkingInterval`
**Свойства:** Duration: TimeSpan, StartTime: DateTime, EndTime: DateTime, StartSpan: TimeSpan, EndSpan: TimeSpan, Class: WorkingIntervalType, Name: StringParameter, Start: DateTimeParameter, End: DateTimeParameter, ChangeNumber: Int32Parameter

### `WorkingIntervalReference`
**Свойства:** Classes: WorkingIntervalTypes

### `WorkingIntervalType`
**Свойства:** Classes: WorkingIntervalTypes, IsWorkingInterval: Boolean

### `WorkingIntervalTypes`
**Свойства:** WorkingInterval: WorkingIntervalType

### `WorkingPage`
**Свойства:** Connection: ServerConnection, Id: Int32, Guid: Guid, IsAdded: Boolean, IsModified: Boolean, Name: String, Comment: String, Type: WorkingPageType, AlwaysVisible: Boolean, AccessType: WorkingPageAccessType, AccessUsers: UserCollection, ConfigurationUseType: ConfigurationUseType, Configurations: ConfigurationCollection, Data: Byte[], Icon: IconImage, IsPrivate: Boolean, StartPageUsers: StartPageUserCollection, LastEditor: User, LastEditDate: Nullable`1
**Методы:**
- `Boolean CanUseInCurrentConfiguration()`
- `Boolean CanUseInConfiguration(BaseConfiguration configuration)`
- `Boolean Save()`
- `String GetHyperlink(String serverAddress)` [has Async]
- `Boolean Delete()`
- `Boolean MoveUp()`
- `Boolean MoveDown()`
- `Boolean Move(Int32 range)`

### `WorkingPageLink`
**Свойства:** Text: String, WorkingPageGuid: Guid, WorkingPage: WorkingPage, CanContainChildren: Boolean

### `WorkingPageManager`
**Методы:**
- `List`1 GetPages(ServerConnection connection) (+1)`
- `List`1 GetWindowsPages(ServerConnection connection)` [has Async]
- `List`1 GetWebPages(ServerConnection connection)`
- `WorkingPage GetDefaultStartPage(ServerConnection connection) (+1)` [has Async]
- `WorkingPage Find(ServerConnection connection, Int32 pageId) (+3)`
- `Boolean Export(ServerConnection connection, Stream stream, IEnumerable`1 pages) (+2)`
- `List`1 Import(ServerConnection connection, Stream stream) (+1)`

### `WorkSessionElementReferenceObject`
**Свойства:** Class: CadWorkSessionsType, Name: StringParameter
**Методы:**
- `ReferenceObject AddReferenceObject(ReferenceObject newLinkedObject)` [has Async]
- `Boolean RemoveReferenceObject(ReferenceObject linkedObject)` [has Async]
- `Boolean ReferenceObjectIsContains(ReferenceObject linkedObject)` [has Async]

### `WorkSessionInstanceParameters`
**Свойства:** Reference: Guid, ReferenceObject: Guid, ReferenceObjectInstance: Guid

### `WorkSessionObjectPath`
**Свойства:** ObjectId: Int32, PathToParent: List`1

### `WorkSessionOpenParameters`
**Свойства:** ReferenceObjectInstance: List`1, ParentPaths: List`1

### `WorkSessionParameters`
**Свойства:** WorkSessionObject: Guid, LoadFiles: Boolean, UnloadWorkObjects: Boolean, LoadByDataModel: Guid

### `WorkSessionReferenceObject`
**Свойства:** StructureSettings: ByteArrayParameter, CadSettings: ByteArrayParameter, ActionCloseInCAD: Int32Parameter, MethodBeforeGetStructure: StringParameter, SessionFile: ReferenceObject, Context: ReferenceObject, DataModel: DataModelReferenceObject, Macro: Macro
**Методы:**
- `WorkSessionOpenParameters GetSessionOpenParameters()`
- `Void SetSessionOpenParameters(WorkSessionOpenParameters value)`

### `WorkspaceManager`
**Методы:**
- `Guid Save(ServerConnection connection, Guid id, String workspaceInterface, String data)`
- `String Load(ServerConnection connection, Guid id)`
- `Boolean Delete(ServerConnection connection, Guid id)`

### `WorkTimeManager`
**Свойства:** IsEmpty: Boolean
**Методы:**
- `Void Refresh()`
- `IEnumerable`1 GetAllIntervals()`
- `Boolean IsIncludedInWorkingInterval(DateTime dateTime, Boolean planInDays)`
- `Boolean ExistWorkDaysLessThan(DateTime date)`
- `Boolean ExistWorkDaysMoreThan(DateTime date)`
- `List`1 GetWorkingIntervals(DateTime startTime, DateTime endTime, IWorkTimeChangeCollection changeCollection) (+2)`
- `TimeSpan GetRemainingTime(DateTime date)`
- `DateTime GetNextWorkTime(DateTime date)`
- `List`1 GetHolydayIntervals(TimeInterval interval)`
- `List`1 CalcHolydayIntervals(TimeInterval interval)`
- `List`1 GetUnworkingIntervals(TimeInterval interval)`
- `List`1 CalcUnworkingIntervals(TimeInterval resultInterval, IWorkTimeChangeCollection changeCollection) (+1)`
- `List`1 PlanTask(DateTime startTime, TimeSpan duration)`
- `DateTime CalcTaskStartTime(DateTime endTime, Int32 duration)`
- `DateTime CalculateTaskStartTime(DateTime endTime, TimeSpan duration)`
- `DateTime GetValidEndDate(DateTime dateTime)`
- `DateTimeInterval FromWorkingInterval(DateTime startTime, IWorkingInterval wInterval)`
- `WorkTimeManager Union(WorkTimeManager[] workTimeManagers)`
- `TimeSpan ConvertDaysToTimeSpan(DateTime startDate, Int32 days)`
- `Int32 ConvertTimeSpanToDays(DateTime startDate, TimeSpan timeSpan)`
- `DateTime CalcTaskEndTime(DateTime startDate, TimeSpan duration, IWorkTimeChangeCollection changeCollection) (+2)`
- `Int32 CalcDurationInDays(DateTime startTime, DateTime endTime)`
- `TimeSpan CalcTaskDuration(DateTime startDate, DateTime endDate, IWorkTimeChangeCollection changeCollection) (+1)`
- `IWorkTimeObject GetWorkTimeObject(DateTime date)`
- `DateTime GetNextWorkDayStart(DateTime date, IWorkTimeChangeCollection changeCollection) (+1)`
- `DateTime GetWorkDayStart(DateTime date)`
- `DateTime GetPreviousWorkDayEnd(DateTime date, IWorkTimeChangeCollection changeCollection) (+1)`
- `DateTime GetPreviousWorkTimeEnd(DateTime date)`
- `DateTime GetWorkDayEnd(DateTime date)`

### `WorkTimeReference`
**Свойства:** Classes: WorkTimeTypes

### `WorkTimeReferenceObject`
**Свойства:** DayOfWeekValue: Int32, DayOfMonthValue: Int32, MonthValue: Int32, YearValue: Int32, StartDateValue: DateTime, IsStartDateSetValue: Boolean, EndDateValue: DateTime, IsEndDateSetValue: Boolean, PriorityValue: Int32, Priority: Int32Parameter, Class: WorkTimeType, Name: StringParameter, DayOfWeek: Int32Parameter, DayOfMonth: Int32Parameter, Month: Int32Parameter, Year: Int32Parameter, StartDate: DateTime, IsStartDateSet: Boolean, EndDate: DateTime, IsEndDateSet: Boolean, WorkTimeIntervals: IEnumerable`1, Users: ReferenceObjectCollection, Equipment: ReferenceObjectCollection
**Методы:**
- `Boolean ContainsDate(DateTime date)`
- `ReferenceObject CreateWorkTimeInterval(Guid listObjectClass) (+1)`
- `ReferenceObject AddUser(ReferenceObject newLinkedObject)`
- `Boolean RemoveUser(ReferenceObject linkedObject)`
- `ReferenceObject AddEquipment(ReferenceObject newLinkedObject)`
- `Boolean RemoveEquipment(ReferenceObject linkedObject)`

### `WorkTimeReferenceObjectChange`
**Свойства:** StartDate: DateTime, WorkTimeIntervals: IEnumerable`1, PriorityValue: Int32
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `WorkTimeType`
**Свойства:** Classes: WorkTimeTypes, IsWorkTime: Boolean, IsYearly: Boolean, IsDaily: Boolean, IsMonthely: Boolean, IsWeekl: Boolean, IsDate: Boolean, IsPeriodical: Boolean

### `WorkTimeTypes`
**Свойства:** WorkTime: WorkTimeType, Yearly: WorkTimeType, Daily: WorkTimeType, Monthely: WorkTimeType, Weekl: WorkTimeType, Date: WorkTimeType, Periodical: WorkTimeType

### `YearElementReferenceObject`
**Свойства:** ShowOnlyLastTwoDigits: BooleanParameter
**Методы:**
- `String GetTestValue(String parameter)`

### `YearlyObject`
**Методы:**
- `Boolean ContainsDate(DateTime date)`

### `ДиалогВвода`
**Свойства:** Заголовок: String [RU only], Высота: Double [RU only], Ширина: Double [RU only]
**Методы:**
- `Void ДобавитьЦелое(String имя, Int32 значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьДвоичное(String имя, Double значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьДействительное(String имя, Double значение, Int32 точность, Boolean обязательное)` [RU alternative]
- `Void ДобавитьСтроковое(String имя, String значение, Boolean многострочное, Boolean обязательное, Boolean использоватьВсюШирину, Int32 количествоСтрок)` [RU alternative]
- `Void ДобавитьМаску(String имя, String маска, ТипМаски типМаски, String значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьДату(String имя, DateTime значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьВремя(String имя, DateTime значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьДатуИВремя(String имя, DateTime значение, Boolean обязательное, String маска)` [RU alternative]
- `Void ДобавитьФлаг(String имя, Boolean значение, Boolean обязательное, Boolean использоватьВсюШирину)` [RU alternative]
- `Void ДобавитьВыборИзСписка(String имя, Object значение, Boolean обязательное, Object[] значения)` [RU alternative]
- `Void ДобавитьМножественныйВыборИзСписка(String имя, Object[] значения, Boolean обязательное)` [RU alternative]
- `Void ДобавитьВыборСправочника(String имя, Object значение, Boolean обязательное)` [RU alternative]
- `Void ДобавитьВыборИзСправочника(String имя, String справочник, String параметр, Object значение, Boolean обязательное, String фильтр, Guid корневойОбъект)` [RU alternative]
- `Void ДобавитьПодборОбъекта(String имя, String справочник, String параметр, String контекстРелевантности, Object значение, Boolean обязательное, String фильтр, String вид, Boolean использоватьФильтрСодержит)` [RU alternative]
- `Void ДобавитьКнопку(String имя, Action`1 обработчик, Nullable`1 ширина)` [RU alternative]
- `Void ДобавитьПанель(String имя, String заголовок, Double высота, Boolean вертикальнаяПолосаПрокрутки, Boolean автоотображениеВертикальнойПолосыПрокрутки)` [RU alternative]
- `Void ДобавитьЭлементыНаПанель(String имяПанели, String[] именаЭлементов)` [RU alternative]
- `Boolean Показать()` [RU alternative]
- `Object Значение(String имя)` [RU alternative]
- `Void ДобавитьКомментарий(String имя, String комментарий)` [RU alternative]
- `Void ДобавитьГруппу(String текст)` [RU alternative]
- `Int32 ДобавитьИзображение(ObjectAccessor объект, String путьКИзображению, Int32 количествоСтрок)` [RU alternative]
- `Void ИзменитьИзображение(Int32 индекс, ObjectAccessor объект, String путьКИзображению)` [RU alternative]
- `Int32 ДобавитьИконку(ObjectAccessor объект, String путьКИконке, Int32 количествоСтрок)` [RU alternative]
- `Void ИзменитьИконку(Int32 индекс, ObjectAccessor объект, String путьКИконке)` [RU alternative]
- `Void ДобавитьТекст(String текст, Int32 количествоСтрок)` [RU alternative]
- `Void УстановитьИконку(Guid guid)` [RU alternative]
- `Void УстановитьРазмер(Int32 ширина, Int32 высота)` [RU alternative]
- `Void ОтобразитьПолосыПрокрутки(Boolean вертикальнаяПолосаПрокрутки, Boolean автоотображениеВертикальнойПолосыПрокрутки)` [RU alternative]
- `Void УстановитьВидимостьЭлемента(String имя, Boolean значение)` [RU alternative]
- `Void УстановитьДоступностьЭлемента(String имя, Boolean значение)` [RU alternative]
- `Void УстановитьОбязательнымДляЗаполнения(String имя, Boolean значение)` [RU alternative]
- `Void УстановитьФильтрЭлемента(String имя, String фильтр)` [RU alternative]

### `ДиалогВыбораОбъектов`
**Свойства:** МножественныйВыбор: Boolean [RU only], Фильтр: String [RU only], ВыборФлажками: Boolean [RU only], АвтоВыборФлажками: Boolean [RU only], ВыбранныеОбъекты: Объекты [RU only], ВыбранныеПодключения: Подключения [RU only], ФокусированныйОбъект: Объект [RU only], ФокусированноеПодключение: Подключение [RU only], КорневойОбъект: Объект [RU only], Заголовок: String [RU only], Вид: String [RU only], Каталог: String [RU only], ПапкаКаталога: String [RU only], ПоказатьПанельКнопок: Boolean [RU only], РежимПрототипов: Boolean [RU only], ТолькоЧтение: Boolean [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]

### `ДиалогВыбораОбъектовИзНабора`
**Свойства:** Заголовок: String [RU only], СортироватьВручную: Boolean [RU only], ОтображатьСтрокуПоиска: Boolean [RU only], СкрытьСистемныеКолонки: Boolean [RU only], ОтзеркалитьДиалог: Boolean [RU only], НаборОбъектов: Объекты [RU only], ВыбранныеОбъекты: Объекты [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]
- `Void ДобавитьКолонку(String наименованиеКолонки, Func`2 методВычисленияЗначения)` [RU alternative]

### `ДиалогВыбораОбъектовИзСправочников`
**Свойства:** ВыбранныеОбъекты: Объекты [RU only], Заголовок: String [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]

### `ДиалогВыбораПапки`
**Свойства:** Заголовок: String [RU only], ИмяПапки: String [RU only], НачальнаяПапка: String [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]

### `ДиалогВыбораТипов`
**Свойства:** Заголовок: String [RU only], ВыбранныеТипы: ТипОбъекта[] [RU only], РазрешенныеТипы: ТипОбъекта[] [RU only], ВыборАбстрактныхТипов: Boolean [RU only], ВыборФлажками: Boolean [RU only], АвтоВыборФлажками: Boolean [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]

### `ДиалогВыбораФайла`
**Свойства:** ДобавитьРасширение: Boolean [RU only], Заголовок: String [RU only], РасширениеПоУмолчанию: String [RU only], ИмяФайла: String [RU only], ИменаФайлов: String[] [RU only], Фильтр: String [RU only], ИндексФильтра: Int32 [RU only], НачальнаяПапка: String [RU only], МножественныйВыбор: Boolean [RU only], ПоддержкаСоставныхРасширений: Boolean [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]
- `Stream ОткрытьФайл()` [RU alternative]

### `ДиалогСохраненияФайла`
**Свойства:** Заголовок: String [RU only], НачальнаяПапка: String [RU only], ИндексФильтра: Int32 [RU only], Фильтр: String [RU only], ИменаФайлов: String[] [RU only], ИмяФайла: String [RU only], ПроверкаНаименований: Boolean [RU only], ДобавитьРасширение: Boolean [RU only], РасширениеПоУмолчанию: String [RU only], ЗапросРазрешенияНаСозданиеФайла: Boolean [RU only], ЗапросРазрешенияНаПерезаписьФайла: Boolean [RU only]
**Методы:**
- `Boolean Показать()` [RU alternative]
- `Stream ОткрытьФайл()` [RU alternative]

### `Задание`
**Методы:**
- `Задание CreateInstance(MailTask mailTask, MacroContext context)`

### `ЗаданиеКанцелярии`
**Методы:**
- `ЗаданиеКанцелярии CreateInstance(MailResolution mailTask, MacroContext context)`

### `ЗначениеСписка`
**Методы:**
- `ЗначениеСписка CreateInstance(ListValue listValue)`

### `Объект`
**Методы:**
- `Объект CreateInstance(ReferenceObject object, MacroContext context, ComplexHierarchyLink hierarchyLink) (+1)`

### `Объекты`
**Методы:**
- `Объекты CreateInstance(IEnumerable`1 objects, MacroContext context)`
- `Объекты Соответствует(String фильтр)` [RU alternative]
- `Объекты ВыбратьОбъектыВерхнегоУровняСредиСписка()` [RU alternative]

### `Окно`
**Методы:**
- `Окно CreateInstance(IWindow window, MacroContext context)`

### `Подключение`
**Методы:**
- `Подключение CreateInstance(ComplexHierarchyLink hierarchyLink, MacroContext context)`

### `Подключения`
**Методы:**
- `Подключения CreateInstance(IEnumerable`1 links, MacroContext context)`

### `Подпись`
**Методы:**
- `Подпись CreateInstance(Signature signature, MacroContext context)`

### `Пользователь`
**Методы:**
- `Пользователь CreateInstance(User object, MacroContext context)`

### `ПользовательскийДиалог`
**Методы:**
- `ПользовательскийДиалог CreateInstance(UserDialogObject object, MacroContext context)`

### `Сообщение`
**Методы:**
- `Сообщение CreateInstance(MailMessage mailMessage, MacroContext context)`

### `СписокЗначений`
**Методы:**
- `СписокЗначений CreateInstance(ParameterValueList valueList)`

### `ТипПодписи`
**Методы:**
- `ТипПодписи CreateInstance(SignatureType signatureType, MacroContext context)`

### `Условия`
**Методы:**
- `Условия СоздатьЭкземпляр(IEnumerable`1 условия)` [RU alternative]

### `ЭкземплярОбъекта`
**Методы:**
- `ЭкземплярОбъекта CreateInstance(ReferenceObjectInstance object, MacroContext context)`

### `ЭлементУправления`
**Методы:**
- `ЭлементУправления CreateInstance(ILayoutItem item, MacroContext context)`

## TFlex.DOCs.Model.Entities.dll

### `BaseEntity`
**Свойства:** ReferenceGroup: ParameterGroup, ParameterGroup: ParameterGroup, LoadSettings: EntityLoadSettings, EntitySet: EntitySet, Id: Int32, Guid: Guid, AuthorId: Int32, Author: User, CreationDate: DateTime, EditorId: Int32, Editor: User, EditDate: DateTime, StartDate: Nullable`1, EndDate: Nullable`1, DesignContextId: Int32, OriginalId: Int32, DeletedInDesignContext: Boolean, ConflictWithOriginal: ConflictWithOriginal, StructureTypeId: Int32, StructureType: StructureTypesReferenceObject, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, LockState: ReferenceObjectLockState
**Методы:**
- `Boolean TryGetParameter(SystemParameterType systemParameter, Object& value) (+7)`
- `Object GetParameter(SystemParameterType systemParameter) (+7)`
- `Boolean TryGetLinkBaseEntity(Int32 linkId, BaseEntity& entity) (+2)`
- `Boolean TryGetLinkEntity(Int32 linkId, Entity& entity) (+2)`
- `Boolean TryGetLinkHierarchyEntity(Int32 linkId, HierarchyEntity& entity) (+2)`
- `Boolean TryGetLinkBaseEntities(Int32 linkId, IReadOnlyList`1& entities) (+2)`
- `Boolean TryGetLinkEntities(Int32 linkId, IReadOnlyList`1& entities) (+2)`
- `Boolean TryGetLinkHierarchyEntities(Int32 linkId, IReadOnlyList`1& entities) (+2)`
- `Boolean TryGetApplicabilityEntities(IReadOnlyList`1& entities)`
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, Boolean throwOnError) (+1)`
- `ParameterGroup FindRelation(Guid groupGuid)`
- `Boolean ContainsRelation(Int32 groupId)`

### `ChunkEntitiesArgs`
**Свойства:** Part: Int32, EntitySet: EntitySet

### `Entity`
**Свойства:** ReferenceGroup: ParameterGroup, Version: Int32, ClassId: Int32, Class: ClassObject, OwnerId: Int32, Owner: UserReferenceObject, OnBehalfOfId: Int32, OnBehalfOf: UserReferenceObject, CredentialId: Int32, Credential: CredentialsReferenceObject, StageEditDate: DateTime, Deleted: Boolean, ClientViewId: Int32, ClientView: ClientView, Order: Nullable`1, StageId: Int32, Stage: SchemeStage, LogicalObjectGuid: Guid, RevisionName: String, LastRevisionName: String, SourceRevisionName: String, IsActualRevision: Boolean, IsRevisionsContainer: Boolean, MasterServerId: Int32, MasterServer: ReferenceObject, InstanceGroupGuid: Guid, InstanceMappingType: InstancesMappingType, InstanceSequenceNumbers: String, IsStandaloneProduct: Boolean, Master: BaseEntity, MasterEntity: Entity, MasterHierarchyEntity: HierarchyEntity, IsMaster: Boolean, Parents: EntityCollection, Parent: Entity, Children: EntityCollection, HasChildren: Boolean, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, LockState: ReferenceObjectLockState, IsLinkedToNomenclature: Boolean, LinkedObjectId: Int32
**Методы:**
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, HierarchyEntity hierarchyEntity, InstanceEntity instanceEntity, Boolean throwOnError) (+4)`
- `Boolean TryGetStartProductEntity(Entity& productEntity)`
- `Boolean TryGetEndProductEntity(Entity& productEntity)`
- `Boolean TryGetBaseRepresentationEntity(Entity& baseRepresentationEntity)`
- `Boolean TryGetObjectRemarksEntities(IReadOnlyList`1& entities)`
- `String GetFileLocalPath()` [has Async]
- `String GetFileHeadRevision(Boolean checkIsActual)` [has Async]
- `Stream LoadFileAsStream()` [has Async]
- `Entity GetLinkedEntity()`

### `EntityAnalyzer`
**Методы:**
- `FormulaAnalyzer Create(ReferenceInfo referenceInfo) (+2)`
- `MacroContext CreateMacroContext(Entity entity)`

### `EntityAnyLinkLoadSettings`
**Методы:**
- `Boolean Add(ParameterInfo parameter)`

### `EntityExtensions`
**Методы:**
- `IDisposable ClearAndHoldUseConfigurationSettings(EntityLoadSettings loadSettings)`
- `IDisposable ChangeAndHoldConfigurationSettings(EntityLoadSettings loadSettings, ConfigurationSettings configurationSettings) (+1)`
- `Entity ConvertToEntity(ReferenceObject referenceObject) (+1)`
- `Dictionary`2 ConvertToEntityMap(IReadOnlyCollection`1 objects)`

### `EntityFiles`
**Методы:**
- `Dictionary`2 LoadAsStream(IEnumerable`1 files)` [has Async]

### `EntityLinkLoadSettings`
**Свойства:** Connection: ServerConnection, Owner: EntityLoadSettings, LinkGroup: ParameterGroup, StaticReference: Reference, StaticReferenceHierarchyDirection: RecursiveLoadDirection, ConfigurationSettings: ConfigurationSettings

### `EntityLoadSettings`
**Свойства:** Connection: ServerConnection, MasterGroup: ParameterGroup, ReferenceGroup: ParameterGroup, PrototypeMode: Boolean, ConfigurationSettings: ConfigurationSettings, SpecialConfigurationSettings: ConfigurationSettings, UseConfigurationSettings: Boolean, UseInstanceMode: Boolean, ParentInstance: ReferenceObjectInstance, PreloadSystemParameters: Boolean, LoadHierarchy: Boolean, LoadMissingParents: Boolean, UseCache: Boolean, HierarchyDirection: RecursiveLoadDirection, OmitHasChildrenCheck: Boolean, HasParameters: Boolean, Parameters: ParameterInfoCollection, HasHierarchyParameters: Boolean, HierarchyParameters: ParameterInfoCollection, SortFields: ReadOnlyCollection`1, HasSortFields: Boolean, SelectionContext: String, LoadDeleted: Boolean, HasLinks: Boolean, Links: IReadOnlyCollection`1
**Методы:**
- `LinkedEntityLoadSettings GetLinkedEntity()`
- `LinkedEntityLoadSettings AddLinkedEntity()`
- `StructureTypesEntityLoadSettings GetStructureTypesEntity()`
- `StructureTypesEntityLoadSettings AddStructureTypesEntity()`
- `Boolean AddParameter(Int32 parameterId) (+2)`
- `Void AddParameters(Int32[] parameterIds) (+5)`
- `Boolean AddHierarchyParameter(SystemParameterType systemParameter)`
- `Void AddHierarchyParameters(SystemParameterType[] systemParameters) (+1)`
- `Boolean Add(ParameterInfo parameter) (+4)`
- `Boolean ContainsParameter(Int32 parameterId) (+2)`
- `Boolean ContainsHierarchyParameter(SystemParameterType systemParameter)`
- `Boolean Contains(ParameterInfo parameter)`
- `Boolean RemoveParameter(Int32 parameterId) (+2)`
- `Boolean RemoveHierarchyParameter(SystemParameterType systemParameter)`
- `Boolean Remove(ParameterInfo parameter)`
- `SortField AddSortField(ParameterGroup linkGroup, ParameterInfo parameter, SortOrder order) (+1)`
- `Void AddSortFields(SortField[] sortFields) (+1)`
- `Boolean RemoveSortField(SortField field)`
- `Void ClearSortFields()`
- `EntityLinkLoadSettings GetLink(Int32 linkId) (+2)`
- `EntityLinkLoadSettings AddLink(Int32 linkId) (+2)` [has Async]
- `StructureTypeEntityLoadSettings GetStructureTypeEntity()`
- `StructureTypeEntityLoadSettings AddStructureTypeEntity()`
- `ApplicabilityEntityLoadSettings GetApplicabilityEntity()`
- `ApplicabilityEntityLoadSettings AddApplicabilityEntity()`
- `StartProductEntityLoadSettings GetStartProductEntity()`
- `StartProductEntityLoadSettings AddStartProductEntity()`
- `EndProductEntityLoadSettings GetEndProductEntity()`
- `EndProductEntityLoadSettings AddEndProductEntity()`
- `ObjectRemarksEntityLoadSettings GetObjectRemarksEntity()`
- `ObjectRemarksEntityLoadSettings AddObjectRemarksEntity()`
- `AuthorEntityLoadSettings GetAuthorEntity()`
- `AuthorEntityLoadSettings AddAuthorEntity()`
- `EditorEntityLoadSettings GetEditorEntity()`
- `EditorEntityLoadSettings AddEditorEntity()`
- `OwnerEntityLoadSettings GetOwnerEntity()`
- `OwnerEntityLoadSettings AddOwnerEntity()`
- `OnBehalfOfEntityLoadSettings GetOnBehalfOfEntity()`
- `OnBehalfOfEntityLoadSettings AddOnBehalfOfEntity()`
- `CredentialEntityLoadSettings GetCredentialEntity()`
- `CredentialEntityLoadSettings AddCredentialEntity()`
- `MasterServerEntityLoadSettings GetMasterServerEntity()`
- `MasterServerEntityLoadSettings AddMasterServerEntity()`
- `BaseRepresentationEntityLoadSettings AddBaseRepresentationEntity()`
- `EntityLoadSettings Create(ReferenceInfo referenceInfo, Boolean prototypeMode) (+1)` [has Async]

### `EntityLoadSettingsExtensions`
**Методы:**
- `Void AddParentsRecursiveLoad(EntityLoadSettings loadSettings)`
- `Void AddChildrenRecursiveLoad(EntityLoadSettings loadSettings)`
- `Void AddRecursiveLoad(EntityLoadSettings loadSettings, RecursiveLoadDirection loadDirection)`
- `String GetVisualization(EntityLoadSettings loadSettings)`

### `EntityMatcher`
**Методы:**
- `Boolean Match(ReferenceObjectTerm term, Object obj, MacroContext formulaContext)`

### `EntityPathPerformer`
**Методы:**
- `EntityPathPerformer Build(PathPerformerSettings settings)`
- `Object GetValue(Entity entity, HierarchyEntity hierarchyEntity)`
- `Object GetOneValue(Entity entity, HierarchyEntity hierarchyEntity)`

### `EntitySet`
**Свойства:** LoadSettings: EntityLoadSettings, ConfigurationSettings: ConfigurationSettings, ParameterGroup: ParameterGroup, LoadDirection: RecursiveLoadDirection, Item: Entity, EntitiesCountLoaded: Int32
**Методы:**
- `ReadOnlyCollection`1 GetEntities()`
- `Entity GetFirstEntity()`
- `IReadOnlyCollection`1 GetHierarchyEntities()`
- `IReadOnlyCollection`1 GetLoadedEntities()`
- `Entity FindLoadedEntity(Int32 id)`
- `Boolean TryFindLoadedEntity(Int32 id, Entity& entity)`
- `Boolean ContainsLoadedEntity(Int32 id)`
- `IReadOnlyCollection`1 GetLoadedIdEntities()`
- `IReadOnlyCollection`1 GetLoadedHierarchyEntities()`
- `IReadOnlyCollection`1 GetLoadedIdHierarchyEntities()`
- `EntitySet Find(EntityLoadSettings loadSettings, Filter filter, ReferenceObject rootObject, Int32 offset, Int32 count, MacroContext formulaContext, ObjectIterator iterator, Boolean onlyChildren) (+3)` [has Async]
- `Void Load(EntityLoadSettings loadSettings, Action`1 onPartLoaded, Filter filter, ReferenceObject rootObject, Int32 offset, Int32 count, MacroContext formulaContext, ObjectIterator iterator, Boolean onlyChildren)` [has Async]
- `Int32 GetCount(EntityLoadSettings loadSettings, Filter filter, ReferenceObject rootObject, MacroContext formulaContext, Boolean objectsOnly) (+2)` [has Async]

### `EntityStructurePathExtensions`
**Методы:**
- `TStructurePath AddObject(TStructurePath path, Entity entity) (+1)`

### `EntityValue`
**Свойства:** IsObject: Boolean, Entity: Entity, HierarchyEntity: HierarchyEntity

### `EntityVisualizationExtensions`
**Методы:**
- `String GetLoadedLinksVisualization(Entity entity) (+1)`

### `FormulaExtensions`
**Методы:**
- `Void AddToLoadSettings(FormulaMacro formulaMacro, EntityLoadSettings loadSettings)`

### `HierarchyEntity`
**Свойства:** ReferenceGroup: ParameterGroup, IsPrimary: Boolean, AutoSelectRevision: Boolean, ParentId: Int32, Parent: Entity, ChildId: Int32, Child: Entity, IsCheckedOut: Boolean, IsCheckedOutByCurrentUser: Boolean, LockState: ReferenceObjectLockState
**Методы:**
- `ObjectValue GetObjectValue(ReferencePath path, PathCalculationSettings settings, Boolean throwOnError)`
- `Boolean TryGetStructureTypesEntities(IReadOnlyList`1& entities)`

### `HierarchyEntityValue`
**Свойства:** IsHierarchyLink: Boolean, HierarchyEntity: HierarchyEntity

### `InstanceEntity`
**Свойства:** Entity: Entity, HierarchyEntity: HierarchyEntity, AltRepGroupGuid: Guid, MasterServerId: Int32

### `InstanceEntityExtensions`
**Методы:**
- `IEnumerable`1 GetObjectInstances(Entity entity)`

### `LinkedEntityLoadSettings`
**Свойства:** LoadLinkedEntities: Boolean

### `ParameterEntityValue`
**Свойства:** Parameter: ParameterInfo, IsParameter: Boolean

### `ReferencePathExtensions`
**Методы:**
- `EntityLoadSettings AddToLoadSettings(ReferencePath path, EntityLoadSettings loadSettings)`

## TFlex.DOCs.Model.UniversalPath.dll

### `BytesImage`
**Свойства:** Bytes: Byte[]

### `CalculationParameters`
**Свойства:** MacroContext: MacroContext

### `CanSetCheckerUniversalLoaderTreeNode`
**Свойства:** Type: UniversalLoaderTreeNodeType

### `CanSetUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `CastToReferenceUniversalPathItem`
**Свойства:** Target: UniversalArg, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `ValidationResult ValidateArguments(UniversalArg target)`
- `Boolean TryDeserialize(CastToReferenceUniversalPathItemData data, ServerConnection connection, CastToReferenceUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`

### `CastToReferenceUniversalPathItemData`
**Свойства:** ReferenceString: String, IsHierarchy: Boolean, ListIdString: String, Target: UniversalArgData
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `CastUniversalPathItemLoader`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalPathItem item, PathUniversalLoaderTreeNode pathNode, SharedLoadState state, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalPathItem item)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalPathItem item, SharedLoadState state, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalPathItem item, ServerConnection connection)`

### `Chain`
**Свойства:** Path: IReadOnlyCollection`1, MasterGroup: ParameterGroup, OutputGroup: ParameterGroup, NeedСonvert: Boolean [RU only]
**Методы:**
- `Chain TryDeletePrefix(Chain prefix)`
- `Chain MergeFilterNodes()`
- `Chain TryAdd(Filter filter) (+2)`

### `CheckLinkUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `CheckLinkUniversalLoaderTreeNode`
**Свойства:** LinkGroup: ParameterGroup, Type: UniversalLoaderTreeNodeType

### `CompositeUniversalLoaderTreeNavigator`
**Методы:**
- `List`1 GetPath(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`

### `ConfigurationSettingsFilterUniversalPathItem`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `Boolean TryDeserialize(ConfigurationSettingsFilterUniversalPathItemData data, UniversalArg input, ServerConnection connection, ConfigurationSettingsFilterUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`

### `ConfigurationSettingsFilterUniversalPathItemData`
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `ConfigurationSettingsHolderUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `ConfigurationSettingsHolderUniversalLoaderTreeNode`
**Свойства:** ConfigurationSettings: ConfigurationSettings, IsFilter: Boolean, Type: UniversalLoaderTreeNodeType

### `ConfigurationSettingsRunHelper`
**Методы:**
- `ValueTask`1 RunWithConfigSettings(ConfigurationSettings settings, Reference reference, ParameterGroup linkGroup)`

### `ConstantUniversalPathItem`
**Свойства:** Value: Object, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateArguments(Object value)`
- `ConstantUniversalPathItem CreateDefault(Type type, ServerConnection connection)`
- `Boolean TryDeserialize(ConstantUniversalPathItemData data, ServerConnection connection, ConstantUniversalPathItem& result)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `ConstantUniversalPathItemData`
**Свойства:** Type: UniversalArgData, Value: String
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `CurrentDateTimeUniversalPathItem`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`

### `CurrentDateTimeUniversalPathItemData`
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `CurrentObjectUniversalPathItem`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `Boolean TryDeserialize(CurrentObjectUniversalPathItemData data, CurrentObjectUniversalPathItem& result)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `CurrentObjectUniversalPathItemData`
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `CustomColumnUniversalPathItem`
**Свойства:** CalculationString: String, Type: UniversalPathItemType
**Методы:**
- `Boolean TryDeserialize(CustomColumnUniversalPathItemData data, CustomColumnUniversalPathItem& result)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `CustomColumnUniversalPathItemData`
**Свойства:** CalculationString: String
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `DateTimeOperatorSettings`
**Свойства:** Function: DateTimeFunction, InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `Object GetFunctionResult(DateTime dt, TimeSpan offset, DateTime second)`
- `Boolean TryDeserialize(DateTimeOperatorSettingsData data, DateTimeOperatorSettings& res)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`

### `DateTimeOperatorSettingsData`
**Свойства:** Function: DateTimeFunction
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `DelegateAdditionalPathCreator`
**Свойства:** Id: Guid, Name: String
**Методы:**
- `UniversalPath CreatePath(AdditionalPathCreatorContext input)`
- `Boolean IsEnabled(AdditionalPathCreatorContext input)`

### `DependencyInfo`
**Свойства:** Node: UniversalLoaderTreeNodeBase
**Методы:**
- `DependencyPathInfo <Clone>$()`

### `DependencyPathInfo`
**Свойства:** Id: Int32, Path: UniversalPath, SupportMultivalue: Boolean, IsRecursive: Boolean
**Методы:**
- `DependencyPathInfo <Clone>$()`
- `Void Deconstruct(Int32& Id, UniversalPath& Path, Boolean& SupportMultivalue, Boolean& IsRecursive)`

### `DependencyValue`
**Свойства:** Id: Int32, Values: UniversalValue[], SingleValue: UniversalValue
**Методы:**
- `DependencyValue <Clone>$()`
- `Void Deconstruct(Int32& Id, UniversalValue[]& Values)`

### `DependencyValue`
**Свойства:** Id: Int32, Values: UniversalValue[], SingleValue: UniversalValue
**Методы:**
- `DependencyValue <Clone>$()`
- `Void Deconstruct(Int32& Id, UniversalValue[]& Values)`

### `FilterContainer`
**Свойства:** LoadFilter: Filter, ConfigurationSettings: ConfigurationSettings, LoadDeleted: Boolean, FilterContext: MacroContext, LinkGroup: ParameterGroup
**Методы:**
- `FilterContainer CreateRecursiveContainer(Boolean toParents)`
- `FilterContainer Merge(Filter filter, LogicalOperator logicalOperator)`
- `Boolean MustFilter(Reference reference)`
- `ValueTask`1 CheckFilter(DesktopObject obj, CancellationToken token) (+1)`

### `FilteredMinMaxReferenceUniversalLoaderTreeNode`
**Свойства:** Reference: ReferenceInfo, Parameter: ParameterInfo, Filter: Filter, Prefix: ReferencePath, Mode: MinMaxMode, ConfigurationSettings: ConfigurationSettings, Type: UniversalLoaderTreeNodeType
**Методы:**
- `Nullable`1 TryAddPath(ReferencePath path)`
- `FilteredMinMaxReferenceUniversalLoaderTreeNode TryAddFilter(Filter filter)`
- `FilteredMinMaxReferenceUniversalLoaderTreeNode TryAddConfigurationSettings(ConfigurationSettings settings)`

### `FilteredReferenceLoadHelper`
**Методы:**
- `ValueTask`1 Load(Reference reference, Dictionary`2 filterMap, Action`1 settingsConfigurer, ConfigurationSettings configurationSettings, Boolean loadDeleted, MacroContext filterContext, Boolean onlyRoots, ParameterGroup linkGroup, ReferenceStoragesProvider referenceStoragesProvider, CancellationToken token, Int32 maxCount)`

### `FilterUniversalPathItem`
**Свойства:** IsMatchMode: Boolean, Filter: Filter, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `Boolean TryDeserialize(FilterUniversalPathItemData data, UniversalArg input, ServerConnection connection, FilterUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`

### `FilterUniversalPathItemData`
**Свойства:** FilterString: String, IsMatchMode: Boolean
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `FormatByParameterOperatorSettings`
**Свойства:** Parameter: ParameterInfo, InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`
- `Boolean TryDeserialize(FormatByParameterOperatorSettingsData data, ServerConnection connection, FormatByParameterOperatorSettings& res)`

### `FormatByParameterOperatorSettingsData`
**Свойства:** ReferenceGuid: Guid, GroupGuid: Guid, ParameterGuid: Guid
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `FormatByParameterSingleUniversalPathOperatorLoader`
**Свойства:** Type: OperatorType
**Методы:**
- `IEnumerable`1 Load(SourceValue value, IOperatorSettings settings, ServerConnection connection)`
- `ReverseLoadResult ReverseLoad(SourceValue sourceValue, IOperatorSettings settings, ServerConnection connection)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(ServerConnection connection)`

### `FormatStringArgInfo`
**Свойства:** Arg: OperatorArgInfo, Format: String, ItemString: String, JoinString: String
**Методы:**
- `Boolean TryDeseriaize(FormatStringArgInfoData data, ServerConnection connection, FormatStringArgInfo& res)`
- `FormatStringArgInfoData Serialize()`

### `FormatStringArgInfoData`
**Свойства:** Data: OperatorArgInfoData, Format: String, ItemString: String, JoinString: String

### `FormatStringOperatorSettings`
**Свойства:** InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[], FormatArgs: FormatStringArgInfo[], FormatString: String
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `String FormatValue(Object value, String format)`
- `Boolean TryDeserialize(FormatStringOperatorSettingsData data, ServerConnection connection, FormatStringOperatorSettings& res)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`

### `FormatStringOperatorSettingsData`
**Свойства:** Args: FormatStringArgInfoData[], FormatString: String
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `HasChildrenUniversalLoaderTreeNode`
**Свойства:** Filter: Filter, Prefix: ReferencePath, ConfigurationSettings: ConfigurationSettings, Type: UniversalLoaderTreeNodeType
**Методы:**
- `HasChildrenUniversalLoaderTreeNode TryAddPrefix(ReferencePath prefix)`
- `HasChildrenUniversalLoaderTreeNode TryAddFilter(Filter filter)`
- `HasChildrenUniversalLoaderTreeNode TryAddConfigurationSettings(ConfigurationSettings settings)`

### `HierarchyUniversalLoaderTreeNavigator`
**Методы:**
- `List`1 GetPath(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`

### `HierarhyWithFilterUniversalLoaderTreeNode`
**Свойства:** Path: ReferencePath, ConfigurationSettings: ConfigurationSettings, TargetFilter: Filter, Type: UniversalLoaderTreeNodeType
**Методы:**
- `HierarhyWithFilterUniversalLoaderTreeNode TryMergeHierarhy(HierarhyWithFilterUniversalLoaderTreeNode child)`
- `HierarhyWithFilterUniversalLoaderTreeNode TryAddConfigurationSettings(ConfigurationSettings settings)`
- `HierarhyWithFilterUniversalLoaderTreeNode TryAddFilter(Filter filter)`
- `Boolean IsCorrectPath(ReferencePath path)`

### `HierarhyWithFilterUniversalLoaderTreeNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `IAdditionalPathCreator`
**Свойства:** Id: Guid, Name: String
**Методы:**
- `UniversalPath CreatePath(AdditionalPathCreatorContext input)`
- `Boolean IsEnabled(AdditionalPathCreatorContext input)`

### `IdenticalUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `IdenticalUniversalLoaderTreeNode`
**Свойства:** Type: UniversalLoaderTreeNodeType

### `IGetHasChildrenRequest`
**Свойства:** SharedState: SharedLoadState
**Методы:**
- `ValueTask`1 GetHasChildren(UniversalValue from, MacroContext macroContext, CancellationToken token)`

### `IModelUniversalPathsService`
**Свойства:** ColorType: Type
**Методы:**
- `Object CreateColorFromArgb(Int32 argb)`
- `Nullable`1 ColorToArgb(Object color)`
- `Type[] GetUniversalArgSupportedBasicTypes()`
- `String GetUniversalArgTypeName(Type type)`
- `Type[] GetOperatorFormulaMacroAdditionalTypes()`
- `Boolean GetConstantUniversalPathItemValueEquals(Object first, Object second, Boolean& ret)`
- `Boolean GetConstantUniversalPathItemDefaultValue(Type type, Object& obj)`
- `String GetConstantUniversalPathItemSerializeValue(Object value)`
- `Boolean GetConstantUniversalPathItemTryDeserializeValue(String source, Type type, Object& value)`
- `IValueCalculator GetCustomColumnUniversalPathItemLoaderCreate(ParameterGroup masterGroup, String calculateString)`

### `IOperatorSettings`
**Свойства:** InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`

### `IPreparedLoadRequest`
**Свойства:** SharedState: SharedLoadState
**Методы:**
- `ValueTask`1 Load(Func`2 resultGetter, MacroContext macroContext, CancellationToken token, ValueTuple`2[] startValues) (+1)`

### `ISingleUniversalPathOperatorLoader`
**Свойства:** Type: OperatorType
**Методы:**
- `IEnumerable`1 Load(SourceValue value, IOperatorSettings settings, ServerConnection connection)`
- `ReverseLoadResult ReverseLoad(SourceValue sourceValue, IOperatorSettings settings, ServerConnection connection)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(ServerConnection connection)`

### `ITreeRule`
**Методы:**
- `Boolean TryApply(UniversalLoaderTreeNodeBase node)`

### `IUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `IUniversalLoaderTreeNavigator`
**Методы:**
- `List`1 GetPath(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`

### `IUniversalPathItemLoader`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalPathItem item, PathUniversalLoaderTreeNode pathNode, SharedLoadState state, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalPathItem item)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalPathItem item, SharedLoadState state, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalPathItem item, ServerConnection connection)`

### `IUniversalPathOperatorLoader`
**Свойства:** Type: OperatorType
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, IOperatorSettings settings, PathUniversalLoaderTreeNode pathNode, SharedLoadState state, ServerConnection connection, CancellationToken token)`
- `ReverseLoadResult ReverseLoad(SourceValue sourceValue, IOperatorSettings settings, ServerConnection connection)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(ServerConnection connection)`

### `IUniversalPathServiceBase`
**Свойства:** ThemeName: String
**Методы:**
- `String GetCustomColumnName(String calculationText)`

### `IUniversalPathUserInteractionService`
**Методы:**
- `ValueTask`1 ShowPropertiesInDialog(DesktopObjectWithLink obj, CancellationToken token)`

### `LinkedPathUniversalPathItem`
**Свойства:** DesktopObject: DesktopObject, Parameter: ParameterInfo, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateArguments(DesktopObject desktopObject, ParameterInfo parameter)`
- `ValueTask Refresh(LinkedPathUniversalPathItem[] linkItems)`
- `UniversalPath GetPath()`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`
- `Boolean TryDeserialize(LinkedPathUniversalPathItemData data, ServerConnection connection, LinkedPathUniversalPathItem& item)`

### `LinkedPathUniversalPathItemData`
**Свойства:** Object: UniversalPathItemData, ParameterId: Guid
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `MacroOperatorSettings`
**Свойства:** InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[], MacroText: String, AdditionalTypes: UniversalArg[]
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `Boolean TryDeserialize(MacroOperatorSettingsData data, ServerConnection connection, MacroOperatorSettings& res)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`

### `MacroOperatorSettingsData`
**Свойства:** InputType: UniversalArgData, OutputType: UniversalArgData, AdditionalTypes: UniversalArgData[], Args: OperatorArgInfoData[], MacroText: String
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `ModifyDesktopObjectOperatorSettings`
**Свойства:** Parameters: ParameterInfo[], Links: ParameterGroup[], ParentSetMode: ParentSetMode, InputType: UniversalArg, IsCreate: Boolean, OutputType: UniversalArg, Args: OperatorArgInfo[], FullArgs: ArgInfo[]
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `OperatorSettingsData Serialize()`
- `Boolean TryDeserialize(ModifyDesktopObjectOperatorSettingsData data, ServerConnection connection, ModifyDesktopObjectOperatorSettings& result)`
- `ValidationResult ValidateParentSetMode(ParentSetMode mode)`
- `ClassObject GetClass()`
- `ValidationResult Validate()`

### `ModifyDesktopObjectOperatorSettingsData`
**Свойства:** ReferenceType: UniversalArgData, Links: Guid[], Parameters: Guid[], ParentSetMode: ParentSetMode, IsCreate: Boolean
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `MultipleChoiceOperatorSettings`
**Свойства:** PairCount: Int32, HasDefault: Boolean, InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `OperatorSettingsData Serialize()`
- `Boolean TryDeserialize(MultipleChoiceOperatorSettingsData data, MultipleChoiceOperatorSettings& res)`
- `ValidationResult Validate()`
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `ValidationResult ValidateArgs(Int32 pairCount)`

### `MultipleChoiceOperatorSettingsData`
**Свойства:** PairCount: Int32, HasDefault: Boolean
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `OperatorArgInfo`
**Методы:**
- `Boolean TryDeseriaize(OperatorArgInfoData data, ServerConnection connection, OperatorArgInfo& res)`
- `OperatorArgInfoData Serialize()`

### `OperatorArgInfoData`
**Свойства:** InputTypes: UniversalArgData[], Name: String, Tooltip: String, SupportMultiValues: Boolean, CanBeEmpty: Boolean, SupportZeroOrOneValue: Boolean, IsTransparent: Boolean

### `OperatorFormulaMacro`
**Методы:**
- `ValueTask`1 Calculate(MacroContext context, SourceValue[] sourceValues, CancellationToken token)`

### `OperatorSettingsData`
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `OperatorUniversalPathItem`
**Свойства:** Type: UniversalPathItemType, Operator: OperatorType, Operands: UniversalPath[], FirstOperand: UniversalPath, SecondOperand: UniversalPath, OperatorSettings: IOperatorSettings
**Методы:**
- `Boolean TryDeserialize(OperatorUniversalPathItemData data, ServerConnection connection, OperatorUniversalPathItem& result)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `ValidationResult ValidateArguments(OperatorType operator, IOperatorSettings operatorSettings, UniversalPath[] operands)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`
- `UniversalArg[] GetArgTargetByExternal(OperatorType type, Int32 argNumber, IOperatorSettings settings, ServerConnection connection, UniversalArg[] external, UniversalArg[] args)`
- `Boolean ArgPathCanBeEmpty(OperatorType type)`
- `Type GetOperatorSettingsType(OperatorType type)`
- `IOperatorSettings CreateDefaultOperatorSettings(OperatorType type, ServerConnection connection)`
- `Boolean IsTransparentArg(OperatorType type, Int32 argNumber, IOperatorSettings settings)`
- `Boolean IsSupportZeroOrOneValueInArg(OperatorType type, Int32 argNumber, IOperatorSettings settings)`
- `Boolean IsSupportMultiValueInArg(OperatorType type, Int32 argNumber, IOperatorSettings settings, UniversalArg firstArgType)`
- `String GetOperatorGroup(OperatorType type)`
- `IEnumerable`1 GetArgNames(OperatorType type, IOperatorSettings settings, UniversalArg[] args)`
- `Nullable`1 IsCorrectSettings(OperatorType type, IOperatorSettings settings)`
- `Boolean IsFixedArgCount(OperatorType type, IOperatorSettings settings, UniversalArg firstArgType)`
- `Int32 GetMinArgCount(OperatorType type, IOperatorSettings settings, UniversalArg firstArgType)`
- `Int32 GetMaxArgCount(OperatorType type, IOperatorSettings settings, UniversalArg firstArgType)`
- `OperatorArgCount GetArgCount(OperatorType type, UniversalArg firstArgType)`
- `UniversalArg GetInputType(OperatorType type, IOperatorSettings settings)`
- `UniversalArg[] GetArgTypes(Int32 argNum, OperatorType type, IOperatorSettings settings, UniversalArg inputType, ServerConnection connection, UniversalArg[] selectedArgs)`
- `UniversalArg GetReturnType(OperatorType type, UniversalArg input, UniversalPath[] operands, IOperatorSettings settings)`
- `UniversalArg CalcMathReturnType(OperatorType type, UniversalArg[] inputs)`

### `OperatorUniversalPathItemData`
**Свойства:** Operator: OperatorType, Operands: UniversalPathData[], OperatorSettings: OperatorSettingsData
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `ParameterEqualityUniversalPathItem`
**Свойства:** From: ParameterInfo, Target: ParameterInfo, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `ValidationResult ValidateArguments(ParameterInfo from, ParameterInfo target)`
- `Boolean TryDeserialize(ParameterEqualityUniversalPathItemData data, UniversalArg input, ServerConnection connection, ParameterEqualityUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`

### `ParameterEqualityUniversalPathItemData`
**Свойства:** FromString: String, TargetString: String, TargetReferenceString: String, TargetGroupString: String, IsHierarchy: Boolean
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `PathServices`
**Свойства:** ModelUniversalPathService: IModelUniversalPathsService

### `PathUniversalLoaderTreeNode`
**Свойства:** PathItem: UniversalPathItem, ConfigurationSettings: ConfigurationSettings, ConfigurationLinkGroup: ParameterGroup, Type: UniversalLoaderTreeNodeType

### `PossibleReverseLoadSources`
**Свойства:** BySource: Boolean, IsEnd: Boolean
**Методы:**
- `PossibleReverseLoadSources <Clone>$()`
- `Void Deconstruct(Boolean& BySource, Boolean& IsEnd)`

### `RecursiveClosureUniversalLoaderTreeNode`
**Свойства:** RecursiveTarget: UniversalLoaderTreeNodeBase, Type: UniversalLoaderTreeNodeType

### `ReferenceCatalogUniversalPathItem`
**Свойства:** Reference: ReferenceInfo, Operation: ReferenceCatalogOperation, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateArguments(ReferenceCatalogOperation operation, ReferenceInfo reference)`
- `Boolean TryDeserialize(ReferenceCatalogUniversalPathItemData data, UniversalArg input, ServerConnection connection, ReferenceCatalogUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `ValidationResult ValidateInputGroup(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`

### `ReferenceCatalogUniversalPathItemData`
**Свойства:** Operation: ReferenceCatalogOperation, ReferenceGuid: Guid
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `ReferenceFilterOperatorSettings`
**Свойства:** Filter: Filter, VarArgs: ReferenceFilterArgType[], LogicalValue: Boolean, InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`
- `Type GetVarArgType(ReferenceFilterArgType type)`
- `String FormatArgName(Int32 i)`
- `Boolean TryDeserialize(ReferenceFilterOperatorSettingsData data, ServerConnection connection, ReferenceFilterOperatorSettings& result)`

### `ReferenceFilterOperatorSettingsData`
**Свойства:** Filter: String, VarArgs: ReferenceFilterArgType[], LogicalValue: Boolean
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `ReferenceParameterConverter`
**Методы:**
- `Boolean NeedConvert(ReferencePath path, Boolean disableAutoConvert)`
- `UniversalValue ReverseAutoConvert(ReferencePath path, UniversalValue value)`
- `UniversalValue AutoConvert(ReferencePath path, UniversalValue value)`

### `ReferencePathUniversalPathItem`
**Свойства:** Path: ReferencePath, DisableAutoConvert: Boolean, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg source)`
- `Type GetParameterConversionType(ParameterInfo parameter)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `Boolean TryDeserialize(ReferencePathUniversalPathItemData data, UniversalArg input, ReferencePathUniversalPathItem& item)`
- `UniversalPathItemData Serialize()`

### `ReferencePathUniversalPathItemData`
**Свойства:** PathString: String, DisableAutoConvert: Boolean
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `ReferenceStoragesProvider`
**Методы:**
- `ValueTask`1 Get(Guid referenceId, ConfigurationSettings settings, ParameterGroup confLinkGroup, ServerConnection connection, CancellationToken token) (+1)`
- `Void Clear()`
- `Void TryAdd(Reference reference)`
- `Void SetStaticReferences(LoadSettings settings, ConfigurationSettings confSettings, ParameterGroup confLinkGroup, ServerConnection connection)`
- `Reference[] Find(Reference reference)`

### `ReferenceWithContextFilterUniversalPathItem`
**Свойства:** OnlyRoots: Boolean, MaxCount: Nullable`1, Filter: Filter, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateInputGroup(UniversalArg input)`
- `ValidationResult ValidateArgs(Filter filter, Boolean onlyRoots, Nullable`1 maxCount)`
- `Boolean TryDeserialize(ReferenceWithContextFilterUniversalPathItemData data, UniversalArg input, ServerConnection connection, ReferenceWithContextFilterUniversalPathItem& item)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`

### `ReferenceWithContextFilterUniversalPathItemData`
**Свойства:** FilterString: String, OnlyRoots: Boolean, MaxCount: Nullable`1
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `RelationTreeHierarchyNavigator`
**Методы:**
- `List`1 GetPath(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`

### `RelationTreeLoadSettingsHelper`
**Свойства:** LoadSettings: LoadSettings, RootLoadDirection: RecursiveLoadDirection, Storage: ReferencesStorage, RootFilter: Filter, ConfigurationSettings: ConfigurationSettings, UseConfigurationSettings: Boolean, LoadDeleted: Boolean
**Методы:**
- `Void SetSourceReference(Reference reference)`
- `Void AddReferencesStorage(ReferencesStorage storage)`
- `Void CheckLink(Chain chain, ParameterGroup link)`
- `ReferencePath AddChain(Chain chain)`
- `LoadSettings AddPath(ReferencePath path)`

### `RelationTreeUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `RelationTreeUniversalLoaderTreeNavigator`
**Методы:**
- `List`1 GetPath(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`

### `RelationTreeUniversalLoaderTreeNode`
**Свойства:** Type: UniversalLoaderTreeNodeType, ConfigurationSettings: ConfigurationSettings
**Методы:**
- `Chain[] GetAllPaths()`
- `RelationTreeUniversalLoaderTreeNode TryAddSatellite(SatelliteRelationTreeUniversalLoaderTreeNode satellite)`
- `Chain GetPrefix(SatelliteRelationTreeUniversalLoaderTreeNode satellite)`

### `ResultInfo`
**Свойства:** From: UniversalValueId, Result: UniversalValue
**Методы:**
- `ResultInfo <Clone>$()`
- `Void Deconstruct(UniversalValueId& From, UniversalValue& Result)`

### `ReverseLoadResult`
**Свойства:** ValueConverter: Func`2, ObjectForSet: DesktopObject, ParameterForSet: ParameterInfo, DependencyId: Nullable`1
**Методы:**
- `ReverseLoadResult <Clone>$()`

### `RootUniversalLoaderTreeNode`
**Свойства:** SharedLoadState: SharedLoadState, DebugView: String, Type: UniversalLoaderTreeNodeType
**Методы:**
- `Void SetStateFromObjects(ConfigurationSettings configurationSettings)`
- `RootUniversalLoaderTreeNode CloneTree()`

### `SatelliteRelationTreeUniversalLoaderNodeLoader`
**Свойства:** Type: UniversalLoaderTreeNodeType, AllowLoadGhosts: Boolean
**Методы:**
- `ValueTask`1 Load(SourceValue[] sourceValues, UniversalLoaderTreeNodeBase node, ServerConnection connection, CancellationToken token)`
- `IEnumerable`1 GetDependencyPaths(UniversalLoaderTreeNodeBase node)`
- `Task`1 ReverseLoad(SourceValue sourceValue, UniversalLoaderTreeNodeBase node, CanSetCalculationCache cache, ServerConnection connection, CancellationToken token)`
- `PossibleReverseLoadSources GetPossibleReverseLoadSources(UniversalLoaderTreeNodeBase node, ServerConnection connection)`

### `SatelliteRelationTreeUniversalLoaderTreeNode`
**Свойства:** Chain: Chain, Prefix: Chain, LinkForCheck: ParameterGroup, IsAddedToTree: Boolean, ConfigurationSettings: ConfigurationSettings, Type: UniversalLoaderTreeNodeType
**Методы:**
- `SatelliteRelationTreeUniversalLoaderTreeNode TryAdd(Filter filter) (+2)`
- `SatelliteRelationTreeUniversalLoaderTreeNode SetPrefix(Chain prefix)`
- `SatelliteRelationTreeUniversalLoaderTreeNode SetConfigurationSettings(ConfigurationSettings settings)`

### `SharedLoadState`
**Свойства:** ItemsForReload: HashSet`1, UseConfigSettings: Boolean, LoadDeleted: Boolean, UseExisted: Boolean, Variables: Dictionary`2, FilterContext: MacroContext, GroupCache: GroupCache, CanSetCache: CanSetCalculationCache, ShowPropertiesService: IUniversalPathUserInteractionService, RootConfigurationSettings: ConfigurationSettings, RootParameterGroup: ParameterGroup, ReferenceStoragesProvider: ReferenceStoragesProvider, ObjectsChanged: Action`1

### `SourceValue`
**Свойства:** Value: UniversalValue, Dependency: DependencyValue[]
**Методы:**
- `SourceValue <Clone>$()`
- `Void Deconstruct(UniversalValue& Value, DependencyValue[]& Dependency)`

### `SourceValue`
**Свойства:** Value: UniversalValue, Dependency: DependencyValue[]
**Методы:**
- `SourceValue <Clone>$()`
- `Void Deconstruct(UniversalValue& Value, DependencyValue[]& Dependency)`

### `SubPathUniversalPathItem`
**Свойства:** SubPath: SubUniversalPathInfo, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateArguments(SubUniversalPathInfo variable)`
- `Boolean TryDeserialize(SubPathUniversalPathItemData data, ServerConnection connection, SubPathUniversalPathItem& result)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `SubPathUniversalPathItemData`
**Свойства:** SubPath: SubUniversalPathInfoData
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `SubUniversalPathInfo`
**Методы:**
- `SubUniversalPathInfoData Serialize()`
- `Boolean TryDeserialize(SubUniversalPathInfoData data, ServerConnection connection, SubUniversalPathInfo& res)`

### `SubUniversalPathInfoData`
**Свойства:** Name: String, Id: Guid, SubPath: UniversalPathData

### `SwappedLinkUniversalLoaderTreeNode`
**Свойства:** Link: ParameterGroup, Filter: Filter, ConfigurationSettings: ConfigurationSettings, Type: UniversalLoaderTreeNodeType
**Методы:**
- `ReferencePath[] TrySplitPath(ReferencePath path)`
- `SwappedLinkUniversalLoaderTreeNode ConvertPath(ReferencePath path)`
- `SwappedLinkUniversalLoaderTreeNode TryAddFilter(SwappedLinkUniversalLoaderTreeNode node, Filter filter)`
- `SwappedLinkUniversalLoaderTreeNode TryAddConfigurationSettings(ConfigurationSettings settings)`

### `TupleItemOperatorSettings`
**Свойства:** Mode: TupleItemMode, ReplaceType: UniversalArg, InputTupleType: UniversalArg, Index: Int32, InputType: UniversalArg, OutputType: UniversalArg, Args: OperatorArgInfo[]
**Методы:**
- `String FormatArgTypeError(UniversalArg type, Int32 num, OperatorArgInfo arg)`
- `OperatorSettingsData Serialize()`
- `ValidationResult Validate()`
- `Boolean TryDeserialize(TupleItemOperatorSettingsData data, ServerConnection connection, TupleItemOperatorSettings& res)`

### `TupleItemOperatorSettingsData`
**Свойства:** Index: Int32, InputTupleType: UniversalArgData, ReplaceType: UniversalArgData, Mode: TupleItemMode
**Методы:**
- `Boolean TryDeserializeCore(ServerConnection connection, IOperatorSettings& item)`

### `UnidirectionalLinkUniversalLoaderTreeNode`
**Свойства:** LinkGroup: ParameterGroup, ConfigurationSettings: ConfigurationSettings, TargetFilter: Filter, Type: UniversalLoaderTreeNodeType
**Методы:**
- `UnidirectionalLinkUniversalLoaderTreeNode TryAddConfigurationSettings(ConfigurationSettings settings)`
- `UnidirectionalLinkUniversalLoaderTreeNode TryAddFilter(UnidirectionalLinkUniversalLoaderTreeNode node, Filter filter)`
- `ReferencePath[] TrySplitPath(ReferencePath path, GroupCache groupCache)`
- `UnidirectionalLinkUniversalLoaderTreeNode ConvertPath(ReferencePath path, GroupCache groupCache)`

### `UniversalArg`
**Методы:**
- `UniversalArg SetIsRecommended(Boolean isRecomended)`
- `String GetTypeName(Type type) (+1)`
- `Boolean IsCorrectCompositeType(CompositeUniversalArgType type, UniversalArg[] args)`
- `ValidationResult ValidateCompositeType(CompositeUniversalArgType type, UniversalArg[] args)`
- `Boolean IsCorrectGroup(ParameterGroup group)`
- `UniversalArgData Serialize()`
- `String SerializeToString(ServerConnection connection)`
- `Boolean TryDeserialize(String data, ServerConnection connection, UniversalArg& result) (+1)`
- `String GetShortToString()`

### `UniversalArg`
**Методы:**
- `String GetTypeName()`

### `UniversalArgData`
**Свойства:** Mode: UniversalArgType, CompositeType: CompositeUniversalArgType, ReferenceGroupGuid: Guid, AssemblyName: String, TypeName: String, ClassId: Guid, CompositeArgs: UniversalArgData[], IsFixedCompositeArgumentCount: Boolean

### `UniversalArgExtensions`
**Методы:**
- `UniversalArg ToUniversalArg(Type type)`
- `UniversalArg[] ToUniversalArgs(Type type) (+1)`
- `UniversalArg ToNullable(UniversalArg type)`
- `UniversalArg ClearClass(UniversalArg arg)`
- `UniversalArg GetCommon(IEnumerable`1 argsEnumerable)`
- `UniversalArg CreateNullableType(Type baseType)`
- `UniversalArg GetTypeOfValue(Object value)`
- `UniversalArg TryParseCompositeType(Type type)`

### `UniversalLoader`
**Методы:**
- `ValueTask`1 SetValues(UniversalValue item, Boolean shouldAll, Boolean useConfigSettings, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CanSetCalculationCache canSetCache, ServerConnection connection, CancellationToken token, ValueTuple`2[] newValues)`
- `Void CheckCanSet(UniversalLoaderTreeNodeBase from)`
- `DesktopObject TryGetSourceDesktopObject(UniversalLoaderTreeNodeBase from, UniversalValue value)`
- `ParameterInfo GetParameterForSet(UniversalLoaderTreeNodeBase from, UniversalValue value)`
- `Func`2 GetSetConverter(UniversalLoaderTreeNodeBase from, UniversalValue value)`
- `Boolean CanSet(UniversalLoaderTreeNodeBase from, UniversalValue value)`
- `Void AddRecursiveClosure(UniversalLoaderTreeNodeBase from, UniversalLoaderTreeNodeBase to)`
- `Void CheckLink(UniversalLoaderTreeNodeBase from, ParameterGroup linkGroup)`
- `ValueTask`1 GetMin(UniversalPath path, UniversalValue[] from, Boolean useConfigSettings, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CancellationToken token)`
- `ValueTask`1 GetMax(UniversalPath path, UniversalValue[] from, Boolean useConfigSettings, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CancellationToken token)`
- `UniversalLoaderTreeNodeBase SetConfigurationSettings(UniversalLoaderTreeNodeBase tree, ConfigurationSettings settings)`
- `ValueTask`1 GetHasChildren(UniversalPath path, UniversalValue from, Boolean loadDeleted, Boolean useConfigSettings, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CanSetCalculationCache canSetCache, CancellationToken token)`
- `ValueTask`1 MakeGetHasChildrenRequest(UniversalPath path, Boolean loadDeleted, Boolean useConfigSettings, MacroContext filterContext, GroupCache groupCache, ParameterGroup rootGroup, ConfigurationSettings rootConfigurationSettings, Dictionary`2 variables, CanSetCalculationCache canSetCache, ServerConnection connection, CancellationToken token)`
- `Boolean TryGetValues(UniversalLoaderTreeNodeBase tree, UniversalValue from, UniversalPath path, UniversalValue[]& result) (+1)`
- `ValueTask`1 MakeRequest(RootUniversalLoaderTreeNode root, ParameterGroup rootGroup, ConfigurationSettings rootConfigurationSettings, ServerConnection connection, CancellationToken token)`
- `ValueTask Load(RootUniversalLoaderTreeNode root, ServerConnection connection, CancellationToken token)`
- `T TryGetSingleValueC(UniversalLoaderTreeNodeBase tree, UniversalValue from, UniversalPath path)`
- `Nullable`1 TryGetSingleValue(UniversalLoaderTreeNodeBase tree, UniversalValue from, UniversalPath path)`
- `UniversalValue TryGetSingleCore(UniversalLoaderTreeNodeBase tree, UniversalValue from, UniversalPath path, UniversalArg target)`
- `ValueTask`1 LoadSingleC(UniversalPath path, ServerConnection connection, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CanSetCalculationCache canSetCache, IUniversalPathUserInteractionService userInteractionService, CancellationToken cancellationToken, UniversalValue universalValue)`
- `ValueTask`1 LoadSingle(UniversalPath path, ServerConnection connection, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CanSetCalculationCache canSetCache, IUniversalPathUserInteractionService userInteractionService, CancellationToken cancellationToken, UniversalValue universalValue)`
- `ValueTask`1 CalculateVariableValues(Dictionary`2 vars, Dictionary`2 varValues, Boolean useConfigSettings, Boolean loadDeleted, MacroContext filterContext, ServerConnection connection)`
- `RootUniversalLoaderTreeNode Create(Boolean useConfigSettings, Boolean loadDeleted, Boolean useExisted, MacroContext filterContext, GroupCache groupCache, Dictionary`2 variables, CanSetCalculationCache canSetCache, IUniversalPathUserInteractionService userInteractionService, UniversalValue[] startValues) (+4)`
- `UniversalLoaderTreeNodeBase AddPath(UniversalLoaderTreeNodeBase root, UniversalPath path, Boolean setCheckPoint)`
- `UniversalLoaderTreeNodeBase GetNodeByPath(UniversalLoaderTreeNodeBase root, UniversalPath path)`
- `String GetDebug(UniversalLoaderTreeNodeBase root)`

### `UniversalLoaderTreeModificationHelper`
**Методы:**
- `Void ValidateTree(RootUniversalLoaderTreeNode root)`
- `RootUniversalLoaderTreeNode Convert(RootUniversalLoaderTreeNode root, ITreeRule[] rules)`
- `ITreeRule DeleteNode(Func`2 predicate, Boolean withChildren)`
- `Boolean CanDeleteNode(UniversalLoaderTreeNodeBase node)`
- `ITreeRule ReplaceTwoNode(Func`3 nodeGetter)`
- `ITreeRule SplitParent(Func`3 predicate)`
- `ITreeRule MoveAllDependencyToParent(Func`3 predicate)`
- `Boolean CanMoveAllDependencyToParent(UniversalLoaderTreeNodeBase node)`
- `ITreeRule ReplaceOneNode(Func`2 predicate, Func`2 nodeGetter) (+1)`
- `ITreeRule ReplaceOneNodeToPath(Func`2 nodeGetter)`
- `ITreeRule ReplaceOneNodeToChain(Func`2 predicate, Func`2 nodeGetter) (+1)`

### `UniversalLoaderTreeNodeBase`
**Свойства:** Type: UniversalLoaderTreeNodeType, LoadState: NodeLoadState, CheckPoint: Nullable`1, Parent: UniversalLoaderTreeNodeBase, Children: IReadOnlyCollection`1, Values: TwoDirectionMultiMap`2, DependedFrom: List`1, DependedTo: List`1, RecursiveTargetFrom: List`1, LoadedSources: HashSet`1
**Методы:**
- `Void AddChild(UniversalLoaderTreeNodeBase child)`
- `Void RemoveChild(UniversalLoaderTreeNodeBase oldChild)`
- `Void ReplaceChild(UniversalLoaderTreeNodeBase oldChild, UniversalLoaderTreeNodeBase newChild)`
- `UniversalValue GetValueById(UniversalValueId id)`
- `PathUniversalLoaderTreeNode GetOrDefaultChild(UniversalPathItem pathItem)`
- `UniversalLoaderTreeNodeBase CloneNode()`

### `UniversalLoaderTreeOptimizator`
**Методы:**
- `ValueTask`1 PrepareCanSet(RootUniversalLoaderTreeNode root, Func`2 canSetParentNodeGetter, CancellationToken token)`
- `ValueTask`1 Optimize(RootUniversalLoaderTreeNode root, ServerConnection connection, CancellationToken token)`
- `ReferencePath[] TrySplitPathBySearchLinks(ReferencePath path)`

### `UniversalPath`
**Свойства:** Chain: IReadOnlyCollection`1, SubPathes: IReadOnlyCollection`1, Input: UniversalArg, Connection: ServerConnection, Output: UniversalArg
**Методы:**
- `Boolean TryAddSubPath(SubUniversalPathInfo info)`
- `Boolean TryAdd(UniversalPathItem item)`
- `UniversalPath CastToInput(UniversalArg inpuGroup)`
- `Boolean TryDeserialize(String data, ServerConnection connection, UniversalPath& path) (+1)`
- `UniversalPathData Serialize()`
- `String SerializeToString()`

### `UniversalPathCommandData`
**Свойства:** Name: String, Id: Guid, Tier: Byte, Path: String, PrevItemPath: String, Getter: UniversalPathData, NameGetter: UniversalPathData, IconGetter: UniversalPathData, IsVisibleGetter: UniversalPathData, IsEnabledGetter: UniversalPathData, CommandAction: UniversalPathData, VarSetters: UniversalPathVariableData[], ChildrenCommands: UniversalPathCommandData[]

### `UniversalPathCommandInfo`
**Методы:**
- `ValidationResult ValidateArguments(String name, UniversalPath getter, UniversalPath nameGetter, UniversalPath iconGetter, UniversalPath isVisibleGetter, UniversalPath isEnabledGetter, UniversalPath commandAction, IReadOnlyCollection`1 varSetters, IReadOnlyCollection`1 childrenCommands)`
- `UniversalArg[] GetActionOutputTargets(UniversalPath action, IReadOnlyCollection`1 varSetters)`
- `UniversalPathCommandData Serialize()`
- `Boolean TryDeserialize(UniversalPathCommandData data, ServerConnection connection, UniversalPathCommandInfo& info)`
- `UniversalPathCommandInfo SetId(Guid id)`
- `UniversalPathCommandInfo SetPath(String path)`
- `UniversalPathCommandInfo SetPrevItemPath(String prevItemPath)`
- `UniversalPathCommandInfo SetChildren(IReadOnlyCollection`1 children)`
- `IReadOnlyCollection`1 SetPaths(IReadOnlyCollection`1 items)`
- `IReadOnlyCollection`1 Merge(IReadOnlyCollection`1 first, IReadOnlyCollection`1 second)`
- `IReadOnlyCollection`1 Except(IReadOnlyCollection`1 first, IReadOnlyCollection`1 other)`

### `UniversalPathData`
**Свойства:** SubPathes: List`1, Chain: List`1, Input: UniversalArgData

### `UniversalPathExtensions`
**Методы:**
- `Boolean TryAddCast(UniversalPath path, ParameterGroup group) (+1)`
- `Boolean TryAddCurrentDateTime(UniversalPath path)`
- `Boolean TryAddReferenceWithFilter(UniversalPath path, Filter filter, Boolean onlyRoots, Nullable`1 maxCount)`
- `Boolean TryAddReferenceCatalog(UniversalPath path, ReferenceCatalogOperation operation, ReferenceInfo reference)`
- `Boolean TryAddFilter(UniversalPath path, Filter filter)`
- `Boolean TryAddMatchFilter(UniversalPath path, Filter filter)`
- `Boolean TryAddConfigSettingsFilter(UniversalPath path)`
- `Boolean TryAddPath(UniversalPath path, ReferencePath refPath, Boolean disableAutoConvert)`
- `Boolean TryAddEquality(UniversalPath path, ParameterInfo from, ParameterInfo to)`
- `Boolean TryAddCustomColumn(UniversalPath path, String calculationString)`
- `Boolean TryAddConstant(UniversalPath path, Object value)`
- `Boolean TryAddConstantEx(UniversalPath path, UniversalValue[] values)`
- `Boolean TryAddVariable(UniversalPath path, UniversalPathVariableInfo variable)`
- `Boolean TryAddSubPath(UniversalPath path, SubUniversalPathInfo subPath)`
- `Boolean TryAddOperator(UniversalPath path, IOperatorSettings operatorSettings, OperatorType operatorType, UniversalPath[] args) (+1)`
- `Boolean TryAddSubPathItem(UniversalPath path, SubUniversalPathInfo subpath)`
- `UniversalPath ToUniversalPath(ReferencePath path, Boolean disableAutoConvert)`
- `UniversalPath CreateFromConstant(ServerConnection connection, Object value, UniversalArg input)`
- `UniversalValue[] GetConstantValues(UniversalPath path)`
- `T GetConstantClassValue(UniversalPath path)`
- `Nullable`1 GetConstantStructValue(UniversalPath path)`
- `UniversalPath ToFilter(UniversalPath path)`
- `UniversalPath ToIsBiggerThen(UniversalPath left, UniversalPath right)`
- `UniversalPath ToParallelOperator(UniversalPath[] paths)`
- `UniversalPath ToMin(UniversalPath first, UniversalPath[] seconds)`
- `UniversalPath ToMax(UniversalPath first, UniversalPath[] seconds)`
- `UniversalPath ToIsEquals(UniversalPath left, UniversalPath right)`
- `UniversalPath ToAnd(UniversalPath left, UniversalPath[] right)`
- `UniversalPath ToOr(UniversalPath left, UniversalPath[] right) (+1)`
- `UniversalPath ToNot(UniversalPath path)`
- `UniversalPath Concat(UniversalPath first, UniversalPath second)`
- `UniversalPath SubPath(UniversalPath path, Int32 start, Int32 count)`
- `UniversalPath CopySubPathesFrom(UniversalPath target, UniversalPath source)`
- `UniversalPath CastToInputOrDefault(UniversalPath path, UniversalArg source, ServerConnection connection, Boolean returnNull, Boolean exactOp) (+2)`
- `IEnumerable`1 GetAllVarNames(UniversalPath path)`
- `IEnumerable`1 GetUsedSubPaths(UniversalPath path)`
- `UniversalPath RenameVariable(UniversalPath path, String oldName, String newName)`
- `Nullable`1 AddConfigFilterToAllSubItems(UniversalPath source, Boolean hasFilterAfter, Boolean processOperatorArgs) (+1)`
- `UniversalArg[] GetPossibleInputsByOutputs(UniversalPathItem pathItem, ServerConnection connection, UniversalArg[] outputs) (+1)`
- `UniversalPath RefreshSubPathes(UniversalPath path, SubUniversalPathInfo[] subPathes)`
- `UniversalPathVariableInfo[] GetUsedVariables(UniversalPath path)`
- `ValidationResult ValidatePathVariables(UniversalPath path, List`1 variables)`
- `ValidationResult ValidatePathTarget(UniversalPath path, UniversalArg[] wantedTargets) (+1)`
- `ClassObject[] CalcAllowedClasses(UniversalArg[] targets)`
- `UniversalPath[] ExpandOperatorSubPathes(UniversalPath path)`
- `UniversalPath[] GetSourceObjectsSubpathes(UniversalPath path)`

### `UniversalPathExtensionsData`
**Свойства:** Variables: UniversalPathVariablesData, Commands: UniversalPathCommandData[]

### `UniversalPathExtensionsInfo`
**Методы:**
- `UniversalPathExtensionsInfo Merge(UniversalPathExtensionsInfo shared)`
- `UniversalPathExtensionsInfo Except(UniversalPathExtensionsInfo other)`
- `UniversalPathExtensionsData Serialize()`
- `String SerializeToString(ServerConnection connection)`
- `Boolean TryDeserialize(UniversalPathExtensionsData data, ServerConnection connection, UniversalPathExtensionsInfo& res) (+1)`

### `UniversalPathItem`
**Свойства:** Type: UniversalPathItemType
**Методы:**
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `UniversalPathItemData`
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

### `UniversalPathVariableData`
**Свойства:** Type: UniversalArgData, Name: String, Value: UniversalPathData, ValueValidator: UniversalPathData, QuickAccess: Boolean

### `UniversalPathVariableInfo`
**Свойства:** ValueValidatorTargets: UniversalArg[], ValueValidatorTargetsList: List`1
**Методы:**
- `UniversalPathVariableInfo WithoutValue()`
- `ValueTask`1 ValidateArgumentsEx(String name, UniversalArg type, UniversalPath value, UniversalPath valueValidator)`
- `ValueTuple`3 ValidateArguments(String name, UniversalArg type, UniversalPath value, UniversalPath valueValidator)`
- `UniversalPathVariableData Serialize()`
- `Boolean TryDeserialize(UniversalPathVariableData data, ServerConnection connection, UniversalPathVariableInfo& res)`

### `UniversalPathVariablesData`
**Свойства:** Variables: UniversalPathVariableData[]

### `UniversalValue`
**Свойства:** ReferenceObject: ReferenceObject, Link: ComplexHierarchyLink, DesktopObject: DesktopObject, DesktopObjectWithLink: DesktopObjectWithLink

### `UniversalValue`
**Свойства:** ObjectType: UniversalArg, Value: Object, Id: UniversalValueId, IsNull: Boolean, ReferenceObject: ReferenceObject, Link: ComplexHierarchyLink, DesktopObject: DesktopObject, DesktopObjectWithLink: DesktopObjectWithLink
**Методы:**
- `UniversalValue CreateNullValue(Type type)`

### `UniversalValueExtensions`
**Методы:**
- `Int32 GetHashCodeByContent(UniversalValue value)`
- `Boolean IsEqualByContent(UniversalValue first, UniversalValue second)`
- `UniversalValue ToUniValue(UniversalValue value)`
- `Nullable`1 ToDotNetValue(UniversalValue value) (+1)`
- `T ToDotNetValueC(UniversalValue value)`
- `UniversalValue CastValue(UniversalValue value, UniversalArg to)`
- `ITuple ReplaceInTuple(ITuple tuple, Int32 index, UniversalValue newValue)`
- `ITuple CreateTuple(Object[] values)`
- `Boolean CanCast(UniversalArg from, UniversalArg to)`

### `VariableUniversalPathItem`
**Свойства:** Variable: UniversalPathVariableInfo, Type: UniversalPathItemType
**Методы:**
- `ValidationResult ValidateArguments(UniversalPathVariableInfo variable)`
- `Boolean TryDeserialize(VariableUniversalPathItemData data, ServerConnection connection, VariableUniversalPathItem& result)`
- `UniversalArg GetOutputInfo(UniversalArg input)`
- `UniversalArg[] GetInputInfo(UniversalArg output, ServerConnection connection)`
- `UniversalPathItemData Serialize()`
- `ValidationResult ValidateInputGroup(UniversalArg input)`

### `VariableUniversalPathItemData`
**Свойства:** Variable: UniversalPathVariableData
**Методы:**
- `Boolean TryDeserializeCore(UniversalArg input, ServerConnection connection, UniversalPathItem& item)`

## TFlex.DOCs.Model.StructuredDocuments.dll

### `AbstractNumAdapter`
**Методы:**
- `Int32 FindStartValueOnLevel(Int32 level)`

### `ClearDocumentDecorator`
**Методы:**
- `Void ClearDocument(WordprocessingDocument document)`

### `ClearImagesTextAndNumerationDecorator`
**Методы:**
- `Void ClearDocument(WordprocessingDocument document)`

### `CommentNode`
**Свойства:** CommentId: Int32, DateTime: DateTime
**Методы:**
- `Void Accept(IVisitor visitor)`

### `CommonClearDocumentStrategy`
**Методы:**
- `Void ClearDocument(WordprocessingDocument document)`

### `CreateOneNodeDocumentBase`
**Методы:**
- `Byte[] CreateDocument(Byte[] cleanDocumentBytesArray, NodeBase node) (+1)`

### `DocsNode`
**Свойства:** StringNumber: String, PlainText: String, OpenXmlBytes: Byte[], Start: Int32, End: Int32, ClassGuidForMapping: Guid, Nodes: IReadOnlyCollection`1
**Методы:**
- `Void Add(DocsNode node)`
- `ClassObject GetClass(Reference reference)`

### `DocumentInfo`
**Свойства:** NumberingInstances: IDictionary`2, AbstractNums: IDictionary`2, Styles: IDictionary`2, Footnotes: IDictionary`2, ImageStorage: WordImageStorage
**Методы:**
- `Style GetStyle(String styleId)`
- `Boolean TryGetAbstractNums(Int32 abstractNumId, AbstractNum& abstractNum)`
- `Boolean TryGetNumberingInstance(Int32 numberingInstanceId, NumberingInstance& numberingInstance)`
- `Byte[] GetImageBytes(String id)`

### `DocumentNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `DocumentObfuscator`
**Методы:**
- `Byte[] Obfuscate(Stream stream, CancellationToken cancellationToken)` [has Async]

### `DocumentParserSettings`
**Свойства:** InjectBookmarks: InjectBookmarks, IgnoreHierarchy: Boolean

### `DocumentStructExtractor`
**Методы:**
- `IDocumentTree GetTree(Stream stream, DocumentParserSettings documentParserSettings, ServerConnection connection, CancellationToken cancellationToken)`
- `IDictionary`2 GetStyles(WordprocessingDocument document)`
- `IDictionary`2 GetNumberingInstances(WordprocessingDocument document)`
- `IDictionary`2 GetAbstractNum(WordprocessingDocument document)`
- `WordImageStorage GetImageStorage(WordprocessingDocument document)`

### `DocumentStructUploader`
**Методы:**
- `ReferenceObject Upload(DocsNode root, FileObject fileObject, IProgress`1 progress, CancellationToken cancellationToken)` [has Async]

### `DocumentTree`
**Свойства:** Root: NodeBase, Name: String, DocumentInfo: DocumentInfo
**Методы:**
- `Void Add(NodeBase nodeToAdd)`
- `NodeBase FindClosestParent(NodeBase node)`
- `NodeBase FindFirst(Func`2 func)`
- `Void Rebuild(Byte[] bytes, ICreateOneNodeDocument createDocumentStrategy)`

### `DocxTreeBookmarks`
**Методы:**
- `Void AddBookmark(NodeBase node)`

### `EmptyDocumentCreator`
**Методы:**
- `Byte[] CreateEmptyDocument(Stream stream)`

### `FormulaNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `HeaderDocsNode`
**Свойства:** ClassGuidForMapping: Guid

### `HeaderListNode`
**Методы:**
- `Void Accept(IVisitor visitor)`
- `Int32 GetNodeLevel()`

### `HeaderNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `HeaderNodeFactory`
**Методы:**
- `NodeBase Create()`

### `HyperlinkNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `IAbstractFactory`
**Методы:**
- `IClearDocumentStrategy CreateClearStrategy()`
- `ICreateOneNodeDocument CreateOneNodeDocumentStrategy()`

### `IAbstractNum`
**Методы:**
- `Int32 FindStartValueOnLevel(Int32 level)`

### `IClearDocumentStrategy`
**Методы:**
- `Void ClearDocument(WordprocessingDocument document)`

### `ICreateOneNodeDocument`
**Методы:**
- `Byte[] CreateDocument(Byte[] cleanDocumentBytesArray, NodeBase nodes) (+1)`

### `IDocumentTree`
**Свойства:** Root: NodeBase, Name: String, DocumentInfo: DocumentInfo
**Методы:**
- `Void Add(NodeBase node)`
- `Void Rebuild(Byte[] clearDocumentBytes, ICreateOneNodeDocument createDocumentStrategy)`

### `IListNumberAssigner`
**Методы:**
- `String GetCorrectNumber(LinkedListNode`1 numerableNode, DocumentInfo documentInfo, LinkedList`1 allNumerableNodes)`

### `ImageDocsNode`
**Свойства:** ClassGuidForMapping: Guid

### `ImageNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `InitialLetterNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `IntExtensions`
**Методы:**
- `String ToRoman(Int32 number)`
- `String IntToAZSystem(Int32 number)`
- `String IntToWordListLetterNumericSystem(Int32 number)`
- `String IntToUpperLetter(Int32 number)`
- `String ToRussianLower(Int32 number)`
- `String ToRussianUpper(Int32 number)`

### `ISupportTreeBookmarks`
**Методы:**
- `Void AddBookmark(NodeBase node)`

### `ITreeKnife`
**Методы:**
- `NodeBase GetViewBetween(NodeBase startNode, NodeBase endNode)`

### `IVisitor`
**Методы:**
- `Void Visit(DocumentNode documentNode) (+12)`

### `ListNode`
**Методы:**
- `Void Accept(IVisitor visitor)`
- `Int32 GetNodeLevel()`

### `ListNodeExtensions`
**Методы:**
- `NumerableNode FindLastListNode(NodeBase listNode, Func`2 condition)`

### `ListNumberAssigner`
**Методы:**
- `String GetCorrectNumber(LinkedListNode`1 numerableNode, DocumentInfo documentInfo, LinkedList`1 allNumerableNodes)`

### `ManualListNodeFactory`
**Методы:**
- `NodeBase Create()`

### `MixedTextNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `NodeBase`
**Свойства:** OrderId: Int32, Name: String, Parent: NodeBase, LevelInDocument: Int32, ActualLevelInTree: Int32, Index: Int32, InnerOpenXmlElement: OpenXmlElement, Nodes: List`1, BookmarkId: String, RtfText: String, DocumentBytes: Byte[], StartPosition: Int32, EndPosition: Int32, ContainsFieldStart: Boolean, ContainsFieldEnd: Boolean, MergedWith: IList`1, StyleId: String, StyleName: String, StyleBasedOn: String, OutlineLevel: Int32
**Методы:**
- `Void Add(NodeBase node)`
- `Void Remove(NodeBase node)`
- `String GetPath()`
- `NodeBase GetRootNode()`
- `NodeBase GetViewBetween(Int32 startPosition, Int32 endPosition)`
- `NodeBase FindNode(NodeBase node, Func`2 condition)`
- `Void Accept(IVisitor visitor)`
- `Int32 CompareTo(NodeBase other)`

### `NodeNumberParser`
**Методы:**
- `NodeBase Parse(Token token, String text, Boolean considerListHeading)`

### `NumerableNode`
**Свойства:** ListId: Int32, AbstractListId: Int32, LevelInList: Int32, Symbol: String, NumberingType: NumberingTypes, ListType: ListType, StringNumber: String, NumbersOnLevels: IList`1, NumberOnLevelInList: Int32, StartNumberingValue: Int32, LevelOverride: Int32, CreatedFrom: CreatedFrom
**Методы:**
- `Int32 GetNodeLevel()`

### `PagesRangesService`
**Методы:**
- `Void Add(Int32 pageIndex, Int32 start, Int32 end)`
- `Range GetRangesIntersection(Int32 rangeStart, Int32 rangeEnd, Int32 pageIndex) (+1)`
- `Void Clear()`

### `ParagraphContext`
**Свойства:** StyleId: String, StyleHierarchyPath: String, StyleName: String, StyleBasedOn: String, OutlineLevel: Nullable`1, IsHeader: Boolean

### `PictureNodeFactory`
**Методы:**
- `NodeBase Create()`

### `StringExtensions`
**Методы:**
- `String ToUnicodeString(String symbol)`

### `StyledNodeFactory`
**Методы:**
- `NodeBase Create()`

### `SupportingText`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `SupportingTextDocsNode`
**Свойства:** ClassGuidForMapping: Guid

### `TableDocsNode`
**Свойства:** ClassGuidForMapping: Guid

### `TableNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `TextDocsNode`
**Свойства:** ClassGuidForMapping: Guid

### `TextNode`
**Методы:**
- `Void Accept(IVisitor visitor)`

### `TextNodeFactory`
**Методы:**
- `NodeBase Create()`

### `Token`
**Свойства:** Type: TokenType, Value: String

### `Tokenizer`
**Методы:**
- `ICollection`1 Read(String text)`

### `TwoLevelsTree`
**Свойства:** Root: NodeBase, Name: String, DocumentInfo: DocumentInfo
**Методы:**
- `Void Add(NodeBase nodeToAdd)`
- `Void Rebuild(Byte[] clearDocumentBytes, ICreateOneNodeDocument createDocumentStrategy)`

### `WithNumerationAbstractFactory`
**Методы:**
- `IClearDocumentStrategy CreateClearStrategy()`
- `ICreateOneNodeDocument CreateOneNodeDocumentStrategy()`

### `WithoutNumerationAbstractFactory`
**Методы:**
- `IClearDocumentStrategy CreateClearStrategy()`
- `ICreateOneNodeDocument CreateOneNodeDocumentStrategy()`

### `WordImageStorage`
**Методы:**
- `Void AddImage(String id, Byte[] bytes)`
- `Byte[] GetBytes(String id)`

