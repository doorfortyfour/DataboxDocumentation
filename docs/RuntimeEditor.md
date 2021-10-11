# Runtime editor  
The runtime editor allows you to access all of your data at runtime as long as your data is using the GUILayout API for drawing it's value.  
(EditorGUILayout API won't work for runtime builds)

## Create the runtime editor  

1. Simply create an empty game object in your scene and add a new `DataboxRuntimeEditor` component to it.  
2. Assign a Databox object manager to the runtime editor.  
3. Databox comes with a custom Databox GUI style which you can add to the Editor Skin property as well.  
4. The runtime editor is accessible at runtime from the gui button at the top.  
