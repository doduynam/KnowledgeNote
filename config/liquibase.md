# Configuration Liquibase with Multiple .sql file

To run with command line `> gradle update`. in `SpringBoot` project

### 1. `build.gradle`

- Add buildscript to build plugin liquibase gradle

```
buildscript {
    ...
	dependencies {
		classpath "org.liquibase:liquibase-gradle-plugin:2.0.4"
	}
    ...
}
```

- Add plugin id of liquibase gradle 
```
plugins {
	...
	id 'org.liquibase.gradle' version '2.0.4'
    ...
}
```

- Apply plugin
```
apply plugin: 'org.liquibase.gradle'
```

- Add liquibaseRuntime and dependency
```
dependencies {
    ...
	liquibaseRuntime(
			'org.liquibase:liquibase-core:4.19.0',
			'org.postgresql:postgresql:42.5.3'
	)

	implementation 'org.liquibase:liquibase-core:4.19.0'
    ...
}
```

- Add liquibase main to run command line
```
liquibase {
	activities {
		main {
			changeLogFile '{classpath to changelog file}/changelog.xml'
			classpath '{classpath to changelog file}'
			url '{url to database}'
			username '{username of database}'
			password '{password}'
		}
	}
}
``` 

### 2. `changelog.xml`
```
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
		http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-latest.xsd">

</databaseChangeLog>
```

### 2. `Changeset`
- Add define of changeset im `changelog.xml` file
```
...
<changeSet
    id="202302112244_initial_database"
    labels="202302112244_initial_database"
    author="duynam.do">
    <sqlFile
      path="sql/202302112244_initial_database.sql"
      dbms="postgresql"
      endDelimiter=";"
      relativeToChangelogFile="true"
      splitStatements="true"
      stripComments="true"/>
  </changeSet>
...
```

-Add .sql changeset file 

file name: `202302112244_initial_database.sql`
```
-- Liquibase formatted sql
-- Datetime: 2023-02-11 22:44 GMT+7
-- Changeset: 202302112244_initial_database
-- Author: duynam.do

{SQL Script}
```
