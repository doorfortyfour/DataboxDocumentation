# Save and load on Mobile
Loading and in particular saving works a bit differently on Android / iOS especially when using streaming asset path.  
From the official Unity [Documentation](https://docs.unity3d.com/Manual/StreamingAssets.html=Save and load on Android)
    
> "On many platforms, the streaming assets folder location is read-only; you can not modify or write new files there at runtime."  
It's important to consider this when using Databox for Android.

**Here you'll find two possible workflows:**

### Workflow 1:
You can use two Databox objects with different save path configurations. One contains all of your game data which is saved in StreamingAssets folder or Resource folder. This data will be read only during game play.  
Then you have the second Databox object which is empty and is configured to be saved in the persistent data path. During runtime you can then put all data which have to be saved in the second Databox object.  
  
### Workflow 2:
This is quite a common work-flow on Android and suits you probably better. When the user starts your game for the very first time, you simply copy your database file from the StreamingAssets or Resource folder to the persistent data path. It's important to do this only once, otherwise you would constantly overwrite the existing save file.  
Now you simply use the data during runtime (loading and saving) from the persistent data path. In this case you would also use two Databox Objects. One which contains all initial data and is used only in the Unity editor and is being saved in to the streaming asset or resource folder. And a second one which is being used during runtime and loads the data from the persistent data path.  
  
To copy the file to the persistent data path you can use following coded:

**From Resources folder: ("Data" -> file name without extension)**
```csharp
  var jsonString = Resources.Load<TextAsset>("Data");
  File.WriteAllText(System.IO.Path.Combine(Application.persistentDataPath, "Data"), jsonString.text);
```
**From Streaming Assets: (Need to use coroutine on android, as files in streaming assets folder are packed)**
```csharp
  public IEnumerator Load()
  {
    string _result = "";           
    using (UnityEngine.Networking.UnityWebRequest _download = UnityEngine.Networking.UnityWebRequest.Get(System.IO.Path.Combine(Application.streamingAssetsPath), "FileName.ext"))
    {
      yield return _download.SendWebRequest();                   
        while (!_download.isDone)
        {
          if (_download.isNetworkError || _download.isHttpError)
          {
            break;
          }
          
          yield return null;
        }
        
        if (_download.isNetworkError || _download.isHttpError)
        {
          Debug.Log(_download.error);
        }
        else
        {
          _result = _download.downloadHandler.text;
          // Write file to persistent data path
          File.WriteAllText(Path.Combine(Application.persistentDataPath, "FileName.ext"), _result );
        }
      }
  }           
```
