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


### GetEntriesFromTable
### GetValuesFromEntry
### SetData
### EntryExists
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
