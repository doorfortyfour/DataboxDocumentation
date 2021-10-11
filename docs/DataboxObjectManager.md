# Databox Object Manager  
Databox comes with a Databox Object Manager which helps you to keep track of all separate Databox objects.

## Create a Databox object manager  

1. Right click in the project view and select `Create -> Databox -> New Databox Object Manager`
[IMAGE]
2. You can now drag and drop all of your Databox objects in the drag field of the Databox object manager. 
3. Each Databox object can be accessed by it's name from the manager. Simply use:
```csharp
  public DataboxObjectManager manager;
  DataboxObject databoxObject = manager.GetDatabox("MyData");
```

> The Manager is great if you are using multiple Databox objects in your game. For example: **Configuration, GameData, SaveGame** 
