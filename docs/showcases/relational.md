Relational Physical stores can be modelled in legend.

Specifying Relational Store is not supported in Form mode currently, so we need to switch to text mode.

First switch the parser to Relational using the keyword `###Relational`.

In the next line onwards, we can create the database model, define schemas, tables, views and filters. 

```
###Relational
Database store::TradeAccountDb
(
  Schema productSchema
  (
    Table productTable
    (
      ID INTEGER PRIMARY KEY,
      PROD_CLASSIFICATION_ID INTEGER,
      NAME VARCHAR(200)
    )
    Table productClassificationTable
    (
      ID INTEGER PRIMARY KEY,
      TYPE VARCHAR(200),
      DESCRIPTION VARCHAR(200)
    )     
  )

  Table accountTable
  (
    ID INTEGER PRIMARY KEY,
    NAME VARCHAR(200),
    "CREATE DATE" DATE,
    "CLOSE DATE" DATE
  )
  

  Join Product_Classification(productSchema.productTable.PROD_CLASSIFICATION_ID = productSchema.productClassificationTable.ID)

  Filter AccountActiveFilter(accountTable."CLOSE DATE" is not null)
  
  View ActiveAccountsView
  (
    ~filter AccountActiveFilter
    id: accountTable.ID,
    name: accountTable.NAME,
    create_date: accountTable."CREATE DATE"  
  )
)
```

- Schema: A schema is simply a collection of related tables and views.
- View: A view allows us to create preconfigured queries on the database.
- Filter: Commonly used conditions can be used to create filters. A filter can then be used in views or mappings, as we'll see later. 


