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

When you insert a record, the system assigns an ID to each record.
Let's get this new value and set it into debug:
```Apex
// Create the account sObject 
Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
// Insert the account by using DML
insert acct;
// Get the new ID on the inserted sObject argument
ID acctID = acct.Id;
// Display this ID in the debug log
System.debug('ID = ' + acctID);
// Debug log result example
// DEBUG|ID = 001D000000JmKkeIAF
```

Also you can bulk a list of sObjects 

```Apex
// Create a list of contacts
List<Contact> conList = new List<Contact> {
    new Contact(FirstName='Joe',LastName='Smith',Department='Finance'),
        new Contact(FirstName='Kathy',LastName='Smith',Department='Technology'),
        new Contact(FirstName='Caroline',LastName='Roth',Department='Finance'),
        new Contact(FirstName='Kim',LastName='Shain',Department='Education')};
            
// Bulk insert all contacts with one DML call
insert conList;
// List to hold the new contacts to update
List<Contact> listToUpdate = new List<Contact>();
// Iterate through the list and add a title only
//   if the department is Finance
for(Contact con : conList) {
    if (con.Department == 'Finance') {
        con.Title = 'Financial analyst';
        // Add updated contact sObject to the list.
        listToUpdate.add(con);
    }
}
// Bulk update all contacts with one DML call
update listToUpdate;
```


