# SOQL Queries
## Last modification 21/11/09

[SOQL Queries](https://trailhead.salesforce.com/en/content/learn/modules/apex_database/apex_database_soql)

#### Write SoQL Queries
´´´SQL
Account[] accts = [SELECT Name,Phone FROM Account];
´´´

You can also use the Query Editor in "***Query editor***".

#### Basic SoQL Syntax:
´´´SQL
SELECT fields FROM ObjectName [WHERE Condition]
´´´

#### Ordering Query Result
´´´SQL
SELECT Name,Phone FROM Account ORDER BY Name
SELECT Name,Phone FROM Account ORDER BY Name ASC
SELECT Name,Phone FROM Account ORDER BY Name DESC
´´´

#### Limit records returned
´´´SQL
SELECT Name,Phone FROM Account 
                   WHERE (Name = 'SFDC Computing' AND NumberOfEmployees>25)
                   ORDER BY Name
                   LIMIT 10
´´´

#### Accessing variables in SOQL Queries
You can access to access to Apex variables and expressions preceded by a colon (:). It is called ***bind***.

´´´SQL
String targetDepartment = 'Wingo';
Contact[] techContacts = [SELECT FirstName,LastName 
                          FROM Contact WHERE Department=:targetDepartment];
´´´

#### Quering related records
To access to an associated object in SoQL to another, you can access to it with the parent querie.
For example, Contact has a relationship to Account. Then, you can access like:

**Select name and last name of contats de les comptes amb el nom de SFDC Computing.**

´´´SQL
SELECT Name, (SELECT LastName FROM Contacts) FROM Account WHERE Name = 'SFDC Computing'
´´´

#### Create loops to get values
´´´Java
for (variable : [soql_query]) {
    code_block
}
´´´

Example:
´´´Java
insert new Account[]{new Account(Name = 'for loop 1'), 
                     new Account(Name = 'for loop 2'), 
                     new Account(Name = 'for loop 3')};
// The sObject list format executes the for loop once per returned batch
// of records
Integer i=0;
Integer j=0;
for (Account[] tmp : [SELECT Id FROM Account WHERE Name LIKE 'for loop _']) {
    j = tmp.size();
    i++;
}
System.assertEquals(3, j); // The list should have contained the three accounts
                       // named 'yyy'
System.assertEquals(1, i); // Since a single batch can hold up to 200 records and,
                       // only three records should have been returned, the 
                       // loop should have executed only once
´´´
