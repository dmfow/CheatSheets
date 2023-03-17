#### Mongo Shell
```
mongosh
```


#### Commands
```
db.createCollection(‘myFirstCollection’);
db.myFirstCollection.insertOne({ firstName : 'John' , surname: 'Doe' , department: ‘HR’ });
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

```


#### Fix security - Authentication
```
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



