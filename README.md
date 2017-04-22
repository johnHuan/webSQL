# webSQL
WEB SQL By Javascript OOP
# websql笔记 #
>API手册的链接
[https://dev.w3.org/html5/webdatabase/#introduction](https://dev.w3.org/html5/webdatabase/#introduction "WEB SQL Database")
## note ##
A web sql database only works in the latest versions of Safari, google chrome and opera browsers.
### Core Method of web sql ###
The follow are the 3 core methods of web sql 

1. openDatabase			`这个方法使用现有数据库或新建数据库来创建数据库对象`
2. transaction			`这个方法允许我们根据情况控制事务提交或回滚`
3. executeSql			`这个方法用于执行真实的 SQL 查询`

### Creating and Open Databases ###
Using the openDatabase method we can create an object for the database, if the database doesn't exist then it will be create and then an object for that database will be created. We also don't worry about closing the connection with the database.

To create and open the database we need to use the follow syntax.

	var dbObj = openDatabase('[Database_Name]', '[Versuib_Number]', '[Text_Description]', '[size]', '[Creation_Callback]')
#### Example ####
	<!DOCTYPE html>  
	<html>  
		<head>  
    	<title>Open DataBase</title>  
	    <script>  
	        function CreateDB() {  
	            var Database_Name = 'MyDatabase';  
	            var Version = 1.0;  
	            var Text_Description = 'My First Web-SQL Example';  
	            var Database_Size = 2 * 1024 * 1024;  
	            var dbObj = openDatabase(Database_Name, Version, Text_Description, Database_Size, OnSuccessCreate());  
	        }  
	        function OnSuccessCreate() {  
	            alert('Database Created Sucessfully');  
	        }  
	    </script>  
		</head>  
		<body>  
		    <button id="btn1" onclick="CreateDB()">Create Database</button>  
		</body>  
	</html> 

#### 创建完成之后可以在浏览器点击f12查看 ####
>Application > WebSQL

1. chrome
2. safari
3. opera
>IE,firefox 不认识

Since we can saw how to create and open the database in Web SQL, so by using the openDatabase function we can create a database in Web SQL and open the database. There are 5 parameters that are accepted by this openDatabase function that are:

1. **Database name:** This argument provides the name of the database that is mandatory to be provided, otherwise you will get an exception. 
2. **Version number:** Version number is also required; some database may be in version 2.0 and may be in 1.0 so if you know the version number of the database then only you can open it.
3. **Text Description:** This argument describes the database and provides information about the database.
4. **Size of databse:** This argument decides the size of the database.
5. **Creation callback** This argument is optional, if you do not provide any value then the database will also be created but if you want to perform some action after creation of the database then you can use this, so if the database is created successfully then this work will be done.

**Transaction**

After opening our database we can create transactions. This provides the rollback and commit facility. This means inside the transaction we can fire more than one query. If a transaction fails at any point of time or a query has an error then it will be rolled back including all the queries and if all the queries successfully executed then the transaction will be committed.

A transaction is the same as a function that contains more than one query statement.

**Example**
	
    function CreateDB() {  
                var Database_Name = 'MyDatabase';  
                var Version = 1.0;  
                var Text_Description = 'My First Web-SQL Example';  
                var Database_Size = 2 * 1024 * 1024;  
                var dbObj = openDatabase(Database_Name, Version, Text_Description, Database_Size);  
                dbObj.transaction(function (tx) {  
                    //Code of the transaction  
                    //will goes here  
                });  
            }   
**executeSql**

This method performs a very important role for the Web SQL database. This method is used to execute read and write statements which include SQL injection projection and provides a call back method to process the result of any queries. Once if we have a transaction object then we can call the executeSql method.

**Example**
	
    <!DOCTYPE html>  
    <html>  
    <head>  
        <title>Open DataBase</title>  
        <script>  
            function CreateDB() {  
                var Database_Name = 'MyDatabase';  
                var Version = 1.0;  
                var Text_Description = 'My First Web-SQL Example';  
                var Database_Size = 2 * 1024 * 1024;  
                var dbObj = openDatabase(Database_Name, Version, Text_Description, Database_Size);  
                dbObj.transaction(function (tx) {  
                    tx.executeSql('CREATE TABLE IF NOT EXISTS Employee_Table (id unique, Name, Location)');  
                });  
            }  
        </script>  
    </head>  
    <body>  
        <button id="Create_DB_n_Table" onclick="CreateDB()">Create Database & Table</button>  
    </body>  
    </html>   
**how to insert the data into web SQL table**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>web sql insert</title>
	</head>
	<body>
		<form id="form1">
		    <table>
		        <tr>
		            <td>ID:</td>
		            <td><input type="text" id="tbID"></td>
		        </tr>
		        <tr>
		            <td>Name:</td>
		            <td><input type="text" id="tbName"></td>
		        </tr>
		        <tr>
		            <td>Location:</td>
		            <td><input type="text" id="tbLocation"></td>
		        </tr>
		        <tr>
		            <td><button id="btnInsert" onclick="Insert();">insert</button></td>
		        </tr>
		    </table>
		</form>

	<script>
	    var Database_Name = "MyDatabase";
	    var Version = 1.0;
	    var Text_Description = "My First Web-SQL Example";
	    var Database_size = 2 * 1024 * 1024;
	    var dbObj = openDatabase(Database_Name, Version, Text_Description, Database_size);
	    dbObj.transaction(function (tx) {
	        tx.executeSql("CREATE TABLE IF NOT EXISTS Employee_Table(id UNIQUE , Name, Location)");
	    });
	    function Insert() {
	        var id = document.getElementById('tbID').value;
	        var name = document.getElementById('tbName').value;
	        var location = document.getElementById('tbLocation').value;
	        dbObj.transaction(function (tx) {
	            tx.executeSql('INSERT INTO Employee_Table(id, Name, Location) VALUES ('+id+',"'+name+'","'+location+'")');
	        });
   		 }
	</script>
	</body>
	</html>

**how to read the data form the web SQL**

	<!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="UTF-8">
	    <title>web sql insert</title>
	</head>
	<body>
		<p id="hh"></p>
		<form id="form1">
		    <table>
		        <tr>
		            <td>ID:</td>
		            <td><input type="text" id="tbID"></td>
		        </tr>
		        <tr>
		            <td>Name:</td>
		            <td><input type="text" id="tbName"></td>
		        </tr>
		        <tr>
		            <td>Location:</td>
		            <td><input type="text" id="tbLocation"></td>
		        </tr>
		        <tr>
		            <td><button id="btnInsert" onclick="Insert();">insert</button></td>
		        </tr>
		    </table>
		</form>
		<table id="tblGrid" cellpadding="10px" cellspacing="0" border="1">
		    <tr style="background: black; color: #fff; font-size: 18px;">
		        <td>ID</td>
		        <td>Name</td>
		        <td>Location</td>
		    </tr>
		</table>
	
	<script>
	    var Database_Name = "MyDatabase";
	    var Version = 1.0;
	    var Text_Description = "My First Web-SQL Example";
	    var Database_size = 2 * 1024 * 1024;
	    var dbObj = openDatabase(Database_Name, Version, Text_Description, Database_size);
	    dbObj.transaction(function (tx) {
	        tx.executeSql("CREATE TABLE IF NOT EXISTS Employee_Table(id UNIQUE , Name, Location)");
	    });
	    function Insert() {
	        var id = document.getElementById('tbID').value;
	        var name = document.getElementById('tbName').value;
	        var location = document.getElementById('tbLocation').value;
	        dbObj.transaction(function (tx) {
	            tx.executeSql('INSERT INTO Employee_Table(id, Name, Location) VALUES ('+id+',"'+name+'","'+location+'")');
	        });
	    }
	    dbObj.transaction(function (tx) {
	        tx.executeSql('SELECT * FROM Employee_Table', [], function (tx, results) {
	            var len = results.rows.length;
	            var i;
	            var str = '';
	            for (i = 0; i < len; i++) {
	                str += "<tr>";
	                str += "<td>"+results.rows.item(i).id + "</td>";
	                str += "<td>"+results.rows.item(i).Name + "</td>";
	                str += "<td>"+results.rows.item(i).Location + "</td>";
	                str += "</tr>";
	                document.getElementById('tblGrid').innerHTML += str;
	                str = '';
	            }
	
	        }, null);
    	});
	</script>
	</body>
	</html>

**Web SQL DataBase**
在 W3C 的 Web SQL Database 规范中有这样的描述：Web SQL Database 引入了一套使用 SQL 来操纵客户端数据库（client-side database）的 API，这些 API 是异步的（asynchronous），所以在使用这套 API 时会发现匿名函数非常有用。规范中所使用的 SQL 语言为 SQLite 3.6.19。

其中 SQLite 是一款轻型的数据库，是遵循 ACID 的关系型数据库管理系统。它的设计目标是嵌入式的，它占用资源非常低，只需要几百 K 字节的内存就可以了。它能够支持 Windows/Linux/Unix 等主流操作系统，同时能够跟很多程序语言相结合，如 C#，PHP，Java，JavaScript 等，还有 ODBC 接口，比起 Mysql，PostgreSQL 这两款开源的数据库管理系统来说，它的处理速度更快。

**HTML5 Web SQL Database API**

1.Databse

每个域都有一组相关的数据库，每个数据库有名字和当前的版本号。这套 API 并不提供遍历或删除域中的某个数据库的功能。每个数据库一时间只能有一个版本号，不能一时间拥有多个版本号，版本号用来保护数据库不被写入脏数据。

**清单1. Database API**

	 [Supplemental, NoInterfaceObject] 
	 interface WindowDatabase { 
	 	Database openDatabase(
			in DOMString name, 
			in DOMString version, 
			in DOMString displayName,
	  		in unsigned long estimatedSize, 
			in optional DatabaseCallback creationCallback
		);
	 }; 
	 Window implements WindowDatabase; 
	
	 [Supplemental, NoInterfaceObject] 
	 interface WorkerUtilsDatabase { 
	 	Database openDatabase(
			in DOMString name, 
			in DOMString version, 
			in DOMString displayName,
	  		in unsigned long estimatedSize, 
			in optional DatabaseCallback creationCallback
		);
	 	DatabaseSync openDatabaseSync(
			in DOMString name, 
			in DOMString version,
	  		in DOMString displayName, 
			in unsigned long estimatedSize,
	  		in optional DatabaseCallback creationCallback
		);
	 }; 
	 WorkerUtils implements WorkerUtilsDatabase; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface DatabaseCallback { 
	 	void handleEvent(in Database database);
	 };

接口 Window、WorkerUtils 的 openDatabase() 方法和接口 WorkerUtils 的 openDatabaseSync() 方法接受以下参数：一个数据库名字（name），一个数据库版本号（version），一个显示名字（displayName），数据库将要保存数据的大小（estimatedSize，以字节为单位 )，一个可选的回调函数（createionCallback，如果数据库没有被创建，这个函数将会被调用 )。如果提供了回调函数，回调函数用以调用 changeVersion() 函数，不管给定什么样的版本号，回调函数将把数据库的版本号设置为空；如果没有提供回调函数，则以给定的版本号创建数据库。

包括空字符串在内的所有字符串都可以作为有效地数据库名称，数据库名称区分大小写，且可以比较。

2.异步数据库 API（Asynchronous Database API）

**清单2. 异步数据库API**
	
	interface Database { 
		void transaction(
			in SQLTransactionCallback callback, 
			in optional SQLTransactionErrorCallback errorCallback, 
	  	 	in optional SQLVoidCallback successCallback
		);
	  	void readTransaction(
			in SQLTransactionCallback callback, 
	     	in optional SQLTransactionErrorCallback errorCallback, 
	 	 	in optional SQLVoidCallback successCallback
		);
	  readonly attribute DOMString version;
	  void changeVersion(in DOMString oldVersion, 
	   		in DOMString newVersion, 
			in optional SQLTransactionCallback callback,
	    	in optional SQLTransactionErrorCallback errorCallback,
	    	in optional SQLVoidCallback successCallback);
	 }; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface SQLVoidCallback { 
	 	void handleEvent();
	 }; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface SQLTransactionCallback { 
	  	void handleEvent(in SQLTransaction transaction);
	 }; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface SQLTransactionErrorCallback { 
	  	void handleEvent(in SQLError error);
	 };

方法 transaction() 和 readTransaction() 有一个到三个参数，后两个参数为可选的，分别表示错误回调函数和成功回调函数。transaction() 方法为 read/write 模式，readTransaction() 方法为只读模式；获取属性 version 必须返回数据库的当前版本号；方法 changeVersion 允许脚本自动地检查版本号，并修改它。

2.1 执行SQL语句
**清单3执行SQL语句API**
	 typedef sequence<any> ObjectArray; 

	 interface SQLTransaction { 
	 	void executeSql(
			in DOMString sqlStatement, 
			in optional ObjectArray arguments,
	    	in optional SQLStatementCallback callback,
	    	in optional SQLStatementErrorCallback errorCallback
	  	);
	 }; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface SQLStatementCallback { 
	 	void handleEvent(in SQLTransaction transaction, in SQLResultSet resultSet);
	 }; 
	
	 [Callback=FunctionOnly, NoInterfaceObject] 
	 interface SQLStatementErrorCallback { 
	 	boolean handleEvent(in SQLTransaction transaction, in SQLError error);
	 };

这个函数具有四个参数：表示查询的字符串（sqlStatement）；插入到查询语句中问号所在处的字符串数据（arguments)；一个可选的成功时执行函数（callback）；一个可选的失败时执行函数（errorCallback）。

3.数据库查询结果（Database Query Result）

**清单 4. 查询结果集 API**

	interface SQLResultSet { 
		readonly attribute long insertId;
		readonly attribute long rowsAffected;
		readonly attribute SQLResultSetRowList rows;
	 };

如果插入数据库一行数据，insertId 代表这个行号；如果插入多行数据，insertId 代表插入数据的最后一行行号。

SQL 语句执行后改变的行数用 rowsAffected 表示，如果 SQL 语句没有改变任何行，则 rowsAffected 为 0，对于“SELECT”语句，rowsAffected 就为 0.

rows 为一个 SQLResultSetRowList 对象，代表数据库按顺序返回的行。如果没有返回任何行，则这个对象为空。


**再看试一个例子**
	
	<!DOCTYPE html>
	<html lang="en">
	<head>
   		<meta charset="UTF-8">
    	<title>web sql demo</title>
	</head>
	<body>
		<div id="status" name="status">Status Message</div>	
	<script>
	    var db = openDatabase('mydb', 1.0, 'Test DB', 2 * 1024 * 1024 );
	    var msg ;
	    db.transaction(function (tx) {
	        tx.executeSql('CREATE TABLE IF NOT EXISTS  LOGS(id UNIQUE , log)');
	        tx.executeSql('INSERT INTO LOGS(id, log) VALUES (1, "foobar")');
	        tx.executeSql('INSERT INTO LOGS(id, log) VALUES (2, "logmsg")');
	        msg = '<p>Log Message created and row inserted.</p>'
	        document.querySelector('#status').innerHTML = msg;
	    });
	    db.transaction(function (tx) {
	        tx.executeSql('SELECT * FROM LOGS', [], function (tx, results) {
	            var len = results.rows.length;
	            var i;
	            msg = "<p>Found rows:"+len+"</p>";
	            document.querySelector('#status').innerHTML += msg;
	            for (i = 0; i < len; i++) {
	                msg = "<p><b>"+results.rows.item(i).log+"</b></p>";
	                document.querySelector('#status').innerHTML += msg;
	            }
	        }, null);
	    });
	</script>
	</body>
	</html>

第五行的 `var db = openDatabase('mydb', '1.0', 'Test DB', 2 * 1024 * 1024);`

建立一个名称为 mydb 的数据库，它的版本为 1.0，描述信息为 Test DB，大小为 2M 字节。openDatabase 方法打开一个已经存在的数据库，如果数据库不存在则创建数据库，创建数据库的语法如下：

	Database openDatabase(
		in DOMString name, 
		in DOMString version,
		in DOMString displayName, 
		in unsigned long estimatedSize, 
		in optional DatabaseCallback creationCallback
	);
方法用到五个参数：

1. 数据库名	
2. 版本号
3. 描述
4. 数据库大小
5. 创建回调函数

最后一个参数创建回调函数，在创建数据库的时候调用，但即使没有这个参数，一样可以运行时创建数据库。

	var db = window.openDatabase(
	    name,           // 数据库名
	    version,        // 数据库版本号
	    displayName,    // 数据库显示名
	    estimatedSize,  // 存储大小，以字节为单位
	    creationCalback // 可选回调函数，在创建数据库时回调
	);

	db.transaction(
	    SQLTransactioncallback,     // SQL 事务处理回调函数
	    errorCallback,              // 可选，错误回调函数
	    successCallback             // 可选，成功回调函数
	);
	
	function SQLTransactioncallback(transaction) {  // 参数为一个事务对象，可用来执行 SQL 语句。
	    transaction.executeSql(
	        sqlStatement,       // 需执行的 SQL 语句字符串
	        arguments,          // 可选，查询语句中 `?` 指代的字符串数据数组
	        callback,           // 可选，成功回调函数
	        errorCallback       // 可选，失败回调函数
	    );
	}

## HTML5的WEB SQL DatabaseAPI ##

**Example**

	<script>
		var webDb = function(dbname)
	</script>
