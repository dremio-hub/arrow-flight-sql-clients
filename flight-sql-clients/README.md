# Examples of Sending Requests Through the Sample Client

Dremio supports the subset of the Arrow Flight SQL requests that in this section. These examples demonstrate what is returned for each of the supported requests.

Before running the example requests, ensure that you have met these prerequisites:

* Ensure that you have an instance of Dremio 21.0 or later configured and running.
* Ensure that you have a user account on that instance of Dremio.
* Add the Samples data lake to that instance of Dremio by clicking the plus (+) icon in the **Data Lakes** section of the Datasets page.
* Ensure that Java 8 is installed on the system on which you run the example commands.

In all of these example commands, `<Dremio-coordinator-node>` is the hostname or IP address of the coordinator node in your Dremio instance.


### Flight SQL Request: CommandGetDbSchemas

This command submits a `CommandGetDbSchemas` request to list the schemas in a catalog.

#### Example Request

```
java -jar flight-sql-sample-client-application.jar -host <Dremio-coordinator-node> -port 32010 -username myUserName -password myPassword -command GetSchemas   
```

#### Example Output

```
catalog_name	db_schema_name
null	      $scratch
null	      @myUserName
null	      INFORMATION_SCHEMA
null	      Samples
null	      sys
```

### Flight SQL Request: CommandGetTables

This command submits a `CommandGetTables` request to list the tables that are in a catalog or schema.

#### Example Request

```
java -jar flight-sql-sample-client-application.jar -host <Dremio-coordinator-node> -port 32010 -username myUserName -password myPassword -command GetTables -schema INFORMATION_SCHEMA
```

If you have a space in your schema, you can escape it like this:

```
java -jar flight-sql-sample-client-application.jar -host <Dremio-coordinator-node> -port 32010 -username myUserName -password myPassword -command GetTables -schema "Samples\ (1).samples.dremio.com"
```

#### Example Output

```
catalog_name  db_schema_name	        table_name	table_type
null	      INFORMATION_SCHEMA	CATALOGS	SYSTEM_TABLE
null	      INFORMATION_SCHEMA	COLUMNS         SYSTEM_TABLE
null	      INFORMATION_SCHEMA	SCHEMATA	SYSTEM_TABLE
null	      INFORMATION_SCHEMA	TABLES          SYSTEM_TABLE
null	      INFORMATION_SCHEMA	VIEWS           SYSTEM_TABLE
```

### Flight SQL Request: CommandGetTableTypes

This command submits a `CommandTableTypes` request to list the table types supported.

#### Example Request

```
java -jar flight-sql-sample-client-application.jar -host <Dremio-coordinator-node> -port 32010 -username myUserName -password myPassword -command GetTableTypes 
```

#### Example Output

```
table_type
TABLE
SYSTEM_TABLE
VIEW
```

### Flight SQL Request: CommandStatementQuery

This command submits a `CommandStatementQuery` request to run a single SQL statement.

#### Example Request

```
java -jar flight-sql-sample-client-application.jar -host <Dremio-coordinator-node> -port 32010 -username myUserName -password myPassword -command Execute -query 'SELECT * FROM Samples."samples.myUserName.com"."NYC-taxi-trips" limit 10'
```

#### Example Output

```
pickup_datetime	passenger_count	trip_distance_mi fare_amount tip_amount total_amount
2013-05-27T19:15              1             1.26         7.5        0.0          8.0
2013-05-31T16:40              1             0.73         5.0        1.2          7.7
2013-05-27T19:03              2             9.23        27.5        5.0        38.33
2013-05-31T16:24              1             2.27        12.0        0.0         13.5
2013-05-27T19:17              1             0.71         5.0        0.0          5.5
2013-05-27T19:11              1             2.52        10.5       3.15        14.15
2013-05-31T16:41              5             1.01         6.0        1.1          8.6
2013-05-31T16:37              1             1.25         8.5        0.0         10.0
2013-05-31T16:39              1             2.04        10.0        1.5         13.0
2013-05-27T19:02              1            11.73        32.5       8.12        41.12
```

---

# Known Issues

* Personal Access Token (PAT) is not supported by Dremio Software 21.0 yet.
