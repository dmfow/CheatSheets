## Shell / using

#### Mongo Shell
```
mongosh
```

#### Authenticate yourself before running commands
```
db.auth("admin")
```

## Data

#### Create database
```
# There is no “create” command in the MongoDB Shell. In order to create a database, you will first need to switch the context to a non-existing database using the use command:
# Then insert any data (create a collection)
```

#### Commands
```
db.createCollection("myFirstCollection");
db.myFirstCollection.insertOne({ firstName : 'John' , surname: 'Doe' , department: 'HR' });
db.user.insert({name: "Some person", age: 205})
db.inventory.find( { qty: { $gt: 20 } } )
db.inventory.find( { qty: { $in: [ 5, 15 ] } } )
db.inventory.find( { $and: [ { price: { $eq: 2.00 } }, { price: { $exists: true } } ] } )

db.products.update(
{ _id: 100 },
  { $set:
    {
      quantity: 500
    }
  }
)



{
_id: 100,
sku: "abc123",
quantity: 250,
instock: true,
reorder: false,
details: { model: "14Q2", make: "xyz" },
tags: [ "apparel", "clothing" ],
ratings: [ { by: "ijk", rating: 4 } ]
}

```


## Show Structures

#### Show databases
```
show dbs
# OR
db.adminCommand( { listDatabases: 1 } )
db.adminCommand( { listDatabases: 1, nameOnly: true} )
db.adminCommand( { listDatabases: 1, filter: { "name": /^rep/ } } )
# Show current database
db
```



## Users

#### Show users
```
db.getUsers() 
db.getUsers({ filter: { mechanisms: "SCRAM-SHA-256" } })
```

#### Create users
```
# Admin user, see below

use demo
db.createUser(
  {
    user: "justAUser",
    pwd:  passwordPrompt(),   // or cleartext password
    roles: [ { role: "readWrite", db: "demo" },
             { role: "read", db: "finances" } ]
  }
)


# Create a user named accountAdmin01 on the products database:

db.getSiblingDB("products").runCommand( {
   createUser: "accountAdmin01",
   pwd: passwordPrompt(),
   customData: { employeeId: 12345 },
   roles: [ { role: 'readWrite', db: 'products' } ]
} )

db.getSiblingDB("products").getUsers( { showCustomData: false } )
```

#### Remove User
```
db.removeUser()

```

#### Update user
```
use products
db.updateUser( "appClient01",
{
   customData : { employeeId : "0x3010"},
   roles : [
      { role : "read", db : "assets"  }
   ]
} )


use Auth
db.updateUser( "admin",
{
   user: "Admin",
   pwd: "myNewPassword",
} )


use test
db.updateUser(
   "user123",
   {
      pwd: passwordPrompt(),  // or cleartext password
      customData: { title: "Senior Manager" }
   }
)

```



## User Roles

#### Grant roles to a user
```
use products
db.grantRolesToUser(
   "accountUser01",
   [ "readWrite" , { role: "read", db: "stock" } ],
   { w: "majority" , wtimeout: 4000 }
)
```

#### Create roles
```
db.createRole(
   { role: "changeOwnPasswordCustomDataRole",
     privileges: [
        { 
          resource: { db: "", collection: ""},
          actions: [ "changeOwnPassword", "changeOwnCustomData" ]
        }
     ],
     roles: []
   }
)
db.createUser(
   {
     user:"user123",
     pwd: passwordPrompt(),  // or cleartext password
     roles:[ "readWrite", { role:"changeOwnPasswordCustomDataRole", db:"admin" } ] 
   }
)
```

## Secure your Mongodb

#### Security - at least
```
# https://www.digitalocean.com/community/tutorials/how-to-secure-mongodb-on-ubuntu-20-04
# https://www.digitalocean.com/community/tutorial_series/mongodb-security-best-practices-to-keep-your-data-safe

mongosh

use admin

db.createUser(
{
user: "Admin",
pwd: "myNewPassword",
roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
}
)

# Locate the following code in the mongod configuration file (/etc/mongod.conf).
security:
authorization: "disabled"

# Change authorization disabled to enabled and save the file.

security:
authorization: "enabled"

# Restart MongoDB using the following code.
sudo service mongodb restart


# OR


db.createUser({user:'siteUserAdmin', pwd: '<secure password #1>', 
               roles:['userAdminAnyDatabase']})
# Validate the password               
db.auth('siteUserAdmin', '<secure password #1>')

db.createUser({user:'spandan', pwd: '<secure password #2>', 
               roles:[{db:'binstar', role:'readWrite'}]})


Add the auth key to /etc/mongod.conf if you’re using the classic MongoDB configuration format:
auth=true

Add the security.authorization key to /etc/mongod.conf if you’re using the current MongoDB configuration format:
security:
    authorization: enabled
    
sudo service mongod restart    

```



