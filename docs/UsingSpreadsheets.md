# Using Spreadsheets
To make sure Databox recognizes the correct data types you will need to setup the spreadsheet correctly.  
  
Use following keys to mark the appropriate fields:  
`DB_FIELD_NAMES`  
The actual name of the value/variable
`DB_FIELD_TYPES`  
The type of the value. Use the exact name of the data class. (FloatType, IntType...)
`DB_IGNORE`  
Mark rows and cells you don't want to import with this key.  
  
All basic types are supported. You can add additional support by adding your own convert method to your custom DataboxType class.

## Formats
Make sure to separate values by comma. For example:  

`Vector3` 0.3, 2.0, 4.0  
`Color` 255, 220, 120, 255  
`String list` A, B, C, D, E, F  
