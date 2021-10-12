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
Is being called after database has been loaded.  
```csharp
    public DataboxEvents OnDatabaseLoaded;
```  

### OnDatabaseSaving
Is being called as soon as saving the databox object starts.  
```csharp
    public DataboxEvents OnDatabaseSaving;
```
  
### OnDatabaseSaved
Is being called after successfully saving the database.  
```csharp
    public DataboxEvents OnDatabaseSaved;
```
  
### OnDatabaseCloudDownloaded
Is being called after the database has been downloaded.  
```csharp
    public DataboxEvents OnDatabaseCloudDownloaded;
```
  
### OnDatabaseCloudDownloadFailed
Is being called after database download failed.  
```csharp
    public DataboxEvents OnDatabaseCloudDownloadFailed;
```
  
### OnDatabaseCloudUploaded
Is being called after the database has been uploaded.  
```csharp
    public DataboxEvents OnDatabaseCloudUploaded;
```
  
### OnDatabaseCloudUploadFailed
Is being called after database upload failed.  
```csharp
    public DataboxEvents OnDatabaseCloudUploadFailed;
```
  
## Databox Types
### Reset
Resets the value back to it's initial value. When creating a custom class you will need to add the reset functionality to it yourself.  
See the Create a custom class Example.
```csharp
    public virtual void Reset(){}
```
  
**Example**
```csharp
    public DataboxObject data;
    // First get the data you want to reset
    var value = data.GetData<FloatType>("Table", "Entry", "Value");
    
    // Now reset the value
    value.Reset();
```
  
### OnValueChanged
This event is being called as soon as the appropriate value has been changed.  
This is also great for custom data binding.  
```csharp
    public ValueChanged OnValueChanged;
```  
**Example**  
```csharp
    // Register to event
    public void OnEnable()
    {
        FloatType health = database.GetData<FloatType>("Table", "Entry", "Value");
        health.OnValueChanged += ValueChanged;
    }
    // Called as soon as value has been changed
    public void ValueChanged(DataboxType _value)
    {
        Debug.Log("Value has changed")
    }
```
  
## Databox Object Manager
  
### GetDataboxObject
Returns the Databox object according to it's id specified in the DataboxManager.  
```csharp
    public DataboxObject GetDataboxObject(string _dbName)
```
  
## Databox UIBinding
The UIBinding component allows you to bind ui elements to your Databox object.  
  
### Bind
Binds a Unity UI component at runtime to a Databox object.  
```csharp
    public void Bind(DataboxObject _databoxObject, string _tableID, string _entryID, string _valueID)
    public void Bind(string _tableID, string _entryID, string _valueID)
  
    //Passing the databaseID to the method will use the DataboxManager script to retrieve the databox object
    public void Bind (string _dbID, string _tableID, string _entryID, string _valueID)
```
  
`_databoxObject`: The Databox object which should be used  
`_dbID`: The database id assigned to DataboxManager  
`_tableID`: The name of the Databox table  
`_entryID`: The entry name  
`_valueID`: The value name  
  
