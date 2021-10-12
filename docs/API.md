# API

## Databox Object Methods

### AddData
Add data to a databox object. If table and/or entry does not exist. Databox will create a new table/entry.  
```csharp
    // Returns true on success
    public bool AddData(string _tableID, string _entryID, string _valueID, DataboxType _data)
```  
**Example**  
```csharp
    public DataboxObject database;
    FloatType _health = new FloatType();
    _health.Value = 100f;
    database.AddData("TableName", "EntryName", "ValueName", _health);
````
  
### GetData
Returns the data object of type `T`
```csharp
    public T GetData<T>(string _tableID, string _entryID, string _valueID) where T : DataboxType
```  
**Example**  
```csharp
  public DataboxObject database;
  FloatType _floatValue = database.GetData<FloatType>("TableName", "EntryName", "ValueName");
```
  
### TryGetData
Trys to get the data of a specific type, returns true or false if succeeded.  
```csharp
    public bool TryGetData<T>(string _tableID, string _entryID, string _valueID, out T _data) where T : DataboxType
```  
**Example**  
```csharp
    public DataboxObject database;
    public string tableName;
    public string entryName;
    public string valueName;
    FloatType _float;
    if (database.TryGetData<FloatType>(tableName, entryName, valueName, out _float))
    {
        // Return the float value 
        Debug.Log(_float.Value);
    }
```
  
### GetEntriesFromTable
Returns a dictionary with all entries from a table
```csharp
    public OrderedDictionary<string, DatabaseEntry> GetEntriesFromTable(string _fromTable)
```  

**Example**
```csharp
    public DataboxObject database;
    public string tableName;
    var _table = database.GetEntriesFromTable(tableName);
    Debug.Log(_table.Count + " Entries in " + tableName);
    // Iterate through all entries
    foreach(var entry in _table.Keys)
    {
        // Do something
    }
```
  
### GetValuesFromEntry
Returns a dictionary with all values from an entry in a table.  
```csharp
    public Dictionary<string, Dictionary<Type, DataboxType>> GetValuesFromEntry(string _fromTable, string _fromEntry)
```  
**Example**  
```csharp
    public DataboxObject database;
    public string tableName;
    public string entryName;
    var _values = database.GetValuesFromEntry(tableName, entryName);
    Debug.Log(_values.Count + " Values in " + entryName);
    // Then we iterate through all values
    foreach ( var value in _values.Keys)
    {
        // Do something
    }
```
  
### SetData
Set data to DataboxObject. Returns true if succeeded.  
```csharp
    public bool SetData<T>(string _tableID, string _entryID, string _valueID, DataboxType _value) where T : DataboxType
```  
**Example**  
```csharp
    public DataboxObject database;
    var _ok = database.SetData<BoolType>(tableID, entryID, valueID, new BoolType(false));
```
  
### EntryExists
Checks if an entry in a databox object exists. Returns true or false  
```csharp
        public bool EntryExists(string _tableID, string _entryID)
```  
**Example**  
```csharp
    public DataboxObject database;
    var _ok = database.EntryExists(tableID, entryID);
```
  
### ValueExists
Checks if a value in a databox object exists. Returns true or false.  
```csharp
    public bool ValueExists(string _tableID, string _entryID, string _valueID)
```  
**Example**  
```csharp
    public DataboxObject database;
    var _ok = database.ValueExists(tableID, entryID, valueID);
```
  
### RegisterToDatabase
Takes an existing entry and registers it to a new Databox object. This can be used if you are creating game objects at runtime. The newly created object takes the initial data information from an initial Databox object and registers itself to a runtime save game Databox object. Please see the advanced demo scene example here.  
```csharp
    public bool RegisterToDatabase(DataboxObject _dbToRegister, string _tableID, string _entryID, string _newEntryID)
```  

`_dbToRegister`: The Databox object where we want to add the entry  
`_tableID`: The original table name  
`_entryID`: The original entry name  
`_newEntryID`: The new entry name. You should usually use a unique id for this.  

**Example**  
```csharp
    public DataboxObjectManager manager;
    // Get DataboxObject from DataboxObjectManager
    DataboxObject _fromDB = manager.GetDataboxObject(fromDBId);
    DataboxObject _toDB = manager.GetDataboxObject(toDBId);
    // Get unique Instance id from object for new entry id
    int _objectId = this.gameObject.GetInstanceID().ToString()
    _fromDB.RegisterToDatabase(_toDB, "TableName", "EntryName", _objectId);
```  

### LoadDatabase
Loads the saved databox object  
```csharp
    public void LoadDatabase()
```  
With custom file name.  
```csharp
    public void LoadDatabase(string _fileName)
```
  
### LoadDatabaseAsync
Loads the saved databox object asynchronously  
```csharp
    public void LoadDatabaseAsync()
```
  
With custom file name.  
```csharp
    public void LoadDatabaseAsync(string _fileName)
```  
**Example**  
```csharp
    public DataboxObject data;
    StartCoroutine(data.LoadDatabaseAsync());
```
  
### SaveDatabase
Saves the databox object to a json file  
```csharp
    public void SaveDatabase()
```
  
With custom file name.  
```csharp
    public void SaveDatabase(string _fileName)
```
  
### SaveDatabaseAsync
Saves the databox object to a json file asynchronously  
```csharp
    public void SaveDatabaseAsync()
```
  
With custom file name.  
```csharp
    public void SaveDatabaseAsync(string _fileName)
```  
**Example**  
```chsarp
    public DataboxObject data;
    StartCoroutine(data.SaveDatabaseAsync());
```  

### UploadToCloud
Uploads the database from the appropriate DataboxObject to the cloud.  

!> Uploading overrides the complete file stored in the cloud.  
```csharp
    public void UploadToCloud()
```
  
### DownloadFromCloud
Downloads the database from the cloud by using the settings of the appropriate Databox object.  
```csharp
    public void DownloadFromCloud()
```
  
### RemoveDatabaseTable
Remove a complete table from the databox object.  
```csharp
    public void RemoveDatabaseTable(string _tableName)
```
  
### RemoveEntry
Remove specific entry from table  
```csharp
    public void RemoveEntry(string _tableName, string _entryName)
```
  
### RemoveValue
Remove value from entry.  
```csharp
    public void RemoveValue(string _tableName, string _entryName, string _valueName);
```
  
  
## Databox Object Events

### OnDatabaseLoaded
### OnDatabaseSaving
### OnDatabaseSaved
### OnDatabaseCloudDownloaded
### OnDatabaseCloudDownloadFailed
### OnDatabaseCloudUploaded
### OnDatabaseCloudUploadFailed

## Databox Types
### Reset
### OnValueChanged

## Databox Object Manager
### GetDataboxObject

## Databox UIBinding
### Bind
