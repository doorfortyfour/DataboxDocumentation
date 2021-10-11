# Custom data type
Every supported data type in Databox is derived from DataboxType. Follow these instructions to create a custom databox type class.  
  
You can also have a look at the `ExampleCustomDataType.cs` script to see how you can create your own data types with custom editor ui.  
  
1. Create a new C# class and name it like you wish. (In this example: CustomDataClass)  
2. Add the namespace Databox to the class.  
```csharp
using Databox;
```
3. Derive from `DataboxType`  
```csharp
public class CustomDataClass : DataboxType 
{
  ...
}
```
  
4. While deriving from DataboxType you will get access to several overrideable methods.  
```csharp
public override void DrawEditor(){}
public override void DrawInitValueEditor(){}
public override void Reset(){}
public override string Equal(DataboxType _changedValue){}
```  

5. Let's add a simple int value called health to our class.  
```csharp
    [SerializeField]
    private int _health;
    [SerializeField]
    public int InitHealth; // The initial health value
    // Public property of health. By using get and set we can add an OnValueChanged callback
    public int Health
    {
        get {return _health;}
        set
        {
            if (value == _health){return;}
            _health = value;
            if (OnValueChanged != null){OnValueChanged(this);}
        }
    }
```

6. Several things we need to consider.  

To make sure the values are being serialized add a [SerializeField] attribute to the variable
InitHealth stores the initial default value of our health variable. We will use the Reset() override method to set health back to InitHealth.  
  
7. Next we will create a custom editor for our custom class. This will be drawn in the Databox editor.  
```csharp
    public override void DrawEditor()
    {
        var _healthString = Health.ToString();
        _healthString = GUILayout.TextField(_healthString);
        int.TryParse(_healthString, out _health);
    }
```
> Note you can make use of the GUILayout or EditorGUILayout(not working at runtime) API to create your custom editor gui for your data class. Also check out the example class EnemyType in the project folder.
  
8. Let's add the additional GUI code to draw the initial value.
```csharp
    public override void DrawInitValueEditor()
    {
        GUI.color = Color.yellow;
        GUILayout.Label ("Init Health:");
        GUI.color = Color.white;
        var _healthString = InitHealth.ToString();
        _healthString = GUILayout.TextField(_healthString);
        int.TryParse(_healthString, out InitHealth);
    }
```

9. To make sure our reset to initial value functionality works we need to add the Reset() method.  
```csharp
    // Reset value back to initial value
    public override void Reset()
    {
        Health = InitHealth;
    }
```

10. To make sure the cloud sync comparison works we need to add following method. We basically compare each value and if they're different we return a string with the changes.
```csharp
    // Important for the cloud sync comparison
    public override string Equal(DataboxType _changedValue)
    {
        var _v = _changedValue as CustomDataClass;
        if (Health != _v.Health)
        {
            // return original value and changed value
            return Health.ToString() + " : " + _v.Health.ToString();
        }
        else
        {
            return "";
        }
    }
```  

11. Finally we have to add the convert method to make sure the CSV import works. The convert method simply converts the string which comes from the CSV file to the appropriate data type. In this example we simply parse the string to a integer value.
```csharp
    // Convert the CSV string to an integer value
    public override void Convert(string _value)
    {
        Health = int.Parse(_value);
        InitHealth = Health;
    }
```
  
12. Here's the complete custom class. After saving the file you can add data entries of type "YourCustomDataClass"  
```csharp
    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;
    using Databox;
    [System.Serializable]
    public class CustomDataClass : DataboxType {
        [SerializeField]
        private int _health;
        [SerializeField]
        public int InitHealth;
        public int Health
        {
            get {return _health;}
            set
            {
                if (value == _health){return;}
                _health = value;
                if (OnValueChanged != null){OnValueChanged(this);}
            }
        }
        public override void DrawEditor()
        {
            var _healthString = Health.ToString();
            _healthString = GUILayout.TextField(_healthString);
            int.TryParse(_healthString, out _health);
        }
        public override void DrawInitValueEditor()
        {
            GUI.color = Color.yellow;
            GUILayout.Label ("Init Health:");
            GUI.color = Color.white;
            var _healthString = InitHealth.ToString();
            _healthString = GUILayout.TextField(_healthString);
            int.TryParse(_healthString, out InitHealth);
        }
        // Reset value back to initial value
        public override void Reset()
        {
            Health = InitHealth;
        }
        // Important for the cloud sync comparison
        public override string Equal(DataboxType _changedValue)
        {
            var _v = _changedValue as CustomDataClass;
            if (Health != _v.Health)
            {
                // return original value and changed value
                return Health.ToString() + " : " + _v.Health.ToString();
            }
            else
            {
                return "";
            }
        }
    }
```
