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

#### Upserting Records
If you have a mix list with new and existing records, yo ucan process isertions and updates to all records using ***upsert***.
```Apex
// Insert the Josh contact
Contact josh = new Contact(FirstName='Josh',LastName='Kaplan',Department='Finance');       
insert josh;
// Josh's record has been inserted
//   so the variable josh has now an ID
//   which will be used to match the records by upsert
josh.Description = 'Josh\'s record has been updated by the upsert operation.';
// Create the Kathy contact, but don't persist it in the database
Contact kathy = new Contact(FirstName='Kathy',LastName='Brown',Department='Technology');
// List to hold the new contacts to upsert
List<Contact> contacts = new List<Contact> { josh, kathy };
// Call upsert
upsert contacts;
// Result: Josh is updated and Kathy is created.
```

#### Deleting Records
´´´Java
Contact[] contactsDel = [SELECT Id FROM Contact WHERE LastName='Smith']; 
delete contactsDel;
´´´

#### DML statment Exception
If DML Operation fails, it returns an exception of type ***DmlException***.
´´´Java
try {
    // This causes an exception because 
    //   the required Name field is not provided.
    Account acct = new Account();
    // Insert the account 
    insert acct;
} catch (DmlException e) {
    System.debug('A DML exception has occurred: ' +
                e.getMessage());
}
´´´

### Database Methods
1. Database.insert()
2. Database.update()
3. Database.upsert()
4. Database.delete()
5. Database.undelete()
6. Database.merge()

