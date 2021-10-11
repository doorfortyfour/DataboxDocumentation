# Cloud
The cloud feature basically allows you to sync/download and upload the complete data of a Databox Object to a MySQL database.  
Please follow these instructions carefully to install the Databox cloud to your webserver.  

> You will need a MySQL database also your server must support PHP. Please refer to your webhosting company if you are not sure how to setup a MySQL database.  

## Configuration

1. Navigate to the `CloudSerivce` folder inside of the Databox unity project folder.  
2. Open the `config.php` file with your default text editing tool.  
3. You will see following text:
```csharp
$dbhost = 'localhost';
$dbuser = 'MySQL user';
$dbpass = 'MySQL password';
$dbname = 'MySQL database';
$dbtable = 'Databox';
```  
Please add the string information according to your MySQL database setup. The `dbtable` name will be used during the Databox cloud setup you can leave it like this or change it.  

4. Save the `config.php` file  
5. Connect to your webserver via FTP and create a new folder.  
6. Upload all files located in the `CloudService` folder to your newly created folder via FTP.  
7. Open your default web browser and navigate to the `setup.php` file which is located in the newly created folder. So if you have uploaded all files to a folder called "databox", navigate to: http://mywebserver.com/databox/setup.php  
8. You should now see the databox setup screen.
[IMAGE]
9. Click on install.  
10. Databox Cloud has been installed on your server.  
11. You can now use the server url in the unity databox object. (the folder where you have uploaded all files) Example: http://mywebserver.com/databox  
[IMAGE]

## Unique ID
> You can use the Unique id in the configuration to create different upload versions for different Databox Objects or for different team members.
