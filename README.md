# LiquibaseWithSQL

## Introduction
This Demo is useful where we want DB versioning using Liquibase same as we have code versioning with GIT.


## Scenario
Liquibase is useful where many DEV's are working on same DB and we want to track and version changes on DB.


## Tech. Stack and Tools used
1.  Liquibase
2.  Maven
3.  MySQL


## Prepare Scripts
```
1. write your script changesets under src > main > resources >script folder
2. write your script changesets under src > main > resources >rollback-script folder 
3. Add `<validCheckSum></validCheckSum>` tag with checksum value, if you want to edit existing script changeset file.
    example:
        <changeSet id="Ticket-1-create-student-table.sql" author="Rahul">
            <validCheckSum>9:dsfsdf454fgf</validCheckSum>
            <sqlFile
                path="script/Ticket-1-create-student-table.sql"
                relativeToChangelogFile="true"/>
            <rollback>
            <sqlFile
                    path="rollback-script/Ticket-1-rollback-create-student-table.sql"
                    relativeToChangelogFile="true"/>
            </rollback>
        </changeSet>
4. Add `<validCheckSum>ANY</validCheckSum>` tag, if you want to skip checksum validation.
    example:
        <changeSet id="Ticket-1-create-student-table.sql" author="Rahul">
            <validCheckSum>ANY</validCheckSum>
            <sqlFile
                path="script/Ticket-1-create-student-table.sql"
                relativeToChangelogFile="true"/>
            <rollback>
            <sqlFile
                    path="rollback-script/Ticket-1-rollback-create-student-table.sql"
                    relativeToChangelogFile="true"/>
            </rollback>
        </changeSet>
    
5. Add `runAlwaysTrue` in the changeset. If you want to run a specific changeset always.
    -example : 
        <changeSet id="Ticket-1-create-student-table.sql" author="Rahul" runAlways="true">
6. write your changeset sequences under src > main > resources > liquibase_changelog.xml file     
```


## Get Started
```
1.  Clone this project
2.  Either Hard code username/password of DB inside POM.xml file or you can use command to provide username/password.
3.  If you are hard coding username/password inside POM.xml
    -to run script write below command on terminal
        - mvn verify
    -to run rollback script write bellow command on terminal
        - mvn liquibase:rollback -Dliquibase.rollbackCount=<count>
        or
        -mvn liquibase:rollback -Dliquibase.rollbackDate=<date>
        
    or
    
    If you want to give username/password on command(Preferred)
        -to run script write below command on terminal
        - mvn verify -Dliquibase.username=<username> -Dliquibase.password=<password>
    -to run rollback script write bellow command on terminal
        - mvn liquibase:rollback -Dliquibase.rollbackCount=<count> -Dliquibase.username=<username> -Dliquibase.password=<password>
        or
        -mvn liquibase:rollback -Dliquibase.rollbackDate=<date> -Dliquibase.username=<username> -Dliquibase.password=<password>
4.  You can change schema/DB name from Pom.xml file under <defaultSchemaName>xyz</defaultSchemaName> Tag.
```

## Note
-  example for script, rollback script and changelog.xml file are given under mentioned directory for references.

## References

1.  https://www.liquibase.org/
2.  https://docs.liquibase.com/tools-integrations/maven/using-liquibase-and-maven-pom-file.html