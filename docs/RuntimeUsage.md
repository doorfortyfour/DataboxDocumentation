# Runtime usage
To use Databox at runtime simply make sure to have a reference to a Databox object.  
!> It is important to load your data before accessing it.   

You can register a method to the `OnDatabaseLoaded` event, which will be called when your database has been loaded.

## Namespace
```csharp
 using Databox;
```  

## Loading
```csharp
  using Databox;
  public class Example : MonoBehaviour
  {
    // The reference to your databox object
    public DataboxObject data;
    
    void OnEnable()
    {
        data.OnDatabaseLoaded += DataReady;
    }
    
    void OnDisable()
    {
        data.OnDatabaseLoaded -= DataReady;
    }
    
    void Start()
    {
        data.LoadDatabase();
    }
    
    void DataReady()
    {
        // Access data
    }
  }
```

## Saving
```csharp
  // The reference to your databox object
  public DataboxObject data;
    
  void OnEnable()
  {
      data.OnDatabaseSaved += DataSaved;
  }
    
  void OnDisable()
  {
      data.OnDatabaseSaved -= DataSaved;
  }
    
  void Start()
  {
    data.SaveDatabase();
  }
    
  void DataSaved()
  {
      // Data has been saved
  }

```
  
## Get Data
> GetData returns a reference of the data in the database. This means that, when changing the health value in the example you won't need to put the changed value back to the database as it gets updated automatically.
  
```csharp
  using Databox;
  public class Example : MonoBehaviour
  {
    // The reference to your databox object
    public DataboxObject data;
    // return data of type float
    public void GetData()
    {
      FloatType health = data.GetData<FloatType>("TableName", "EntryName", "ValueName");
      // modify value
      health.Value = 10f;
      Debug.Log(health.Value.ToString());
    }
  }
```  

## AddData  
To add data by script simply call AddData.
```csharp
  using Databox;
  public class Example : MonoBehaviour
  {
    // The reference to your databox object
    public DataboxObject data;
    public void AddData()
    {
      // create a new float value
      FloatType health = new FloatType();
      // add value
      health.Value = 100f;
      // Add health to our database
      data.AddData("TableName", "EntryName", "ValueName", health);
    }
  }
```  

## OnValueChanged
Each data value has a "on value changed" event which gets called if a value has been changed.  
```csharp
  using Databox;
  public class Example : MonoBehaviour
  {
    public DataboxObject data;
    FloatType health;
    public void Start()
    {
      // get data
      health = data.GetData<FloatType>("TableName", "EntryName", "ValueName");
      // register event
      health.OnValueChanged += OnHealthChanged;
    }
    
    void OnHealthChanged(DataboxType _data)
    {
      // instead of using a global variable you can also convert the data back
      // var _health = _data as FloatType;
      Debug.Log("Health has been changed " + health.Value.ToString());
    }
}
```
  
 
