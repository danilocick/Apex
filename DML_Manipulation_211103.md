# DML Manipulation
## Last modification 21/11/03

[Link](https://trailhead.salesforce.com/es-MX/content/learn/modules/apex_database/apex_database_dml)

To create and modify registries in Salesforce by using the Data Manipulation Language, abbreviated as DML. DML provides a 
straightforward way to manage records by providing simple statements to insert, update, merge, delete, and restore records. 

```Apex
// Create the account sObject 
Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
// Insert the account by using DML
insert acct;
```

There are DML statements available:
1. insert
2. update
3. delete
4. undelete
5. merge

