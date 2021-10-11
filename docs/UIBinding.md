# UI Binding
[IMAGE]  
Databox has a very simple but powerful UI Binding component which allows you to bind Unity UI elements - Text, InputFields, Sliders, Toggles... - to a specific Databox object.
  
Simply add the `DataboxUIBinding` component to a UI Element, define the table, entry and value id and you're done.  
Make sure to set the Bind On Database Load to true if you want to bind the ui as soon as the Databox object has been loaded. That requires that you load the database on runtime by script. If you set the On Database Load to false you will need to call the Bind method manually.  
Please see the example scene for more information.
