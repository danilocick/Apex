# sObjects
## Last modification 21/11/03
<br>
[Link](https://trailhead.salesforce.com/es-MX/content/learn/modules/apex_database/apex_database_sobjects)


As Apex is integrated with the DB, it can access to the Saleforce registries and his fields.
Ex: 

|  Campo de cuenta | Valor  |
|---|---|
| Id (id.)  |  001D000000JlfXe |
| Nombre  | Acme  |
| Telefono  | (415)555-1212  |

### Creation variables sObjects
```Apex
Account acct = new Account(Name='Acme');
Account acct = new Account(Name='Acme', Phone='(415)555-1212', NumberOfEmployees=100);
```

### Generic sObject 
To get a generic object you can use the field itself but if you want to access to a personalized object you have to use __c. 
For example

```Apex
Account acct = new Account(Name='Acme');
Account acct = new Book__c(Name='BookPersonalized');
```

