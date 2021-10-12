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
> Set data to DataboxObject. Returns true if succeeded.  
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
### RegisterToDatabase
### LoadDatabase
### LoadDatabaseAsync
### SaveDatabase
### SaveDatabaseAsync
### UploadToCloud
### DownloadFromCloud
### RemoveDatabaseTable
### RemoveEntry
### RemoveValue

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
