## SQLconnector
https://mariadb.com/resources/blog/using-sqlalchemy-with-mariadb-connector-python-part-1/<br>
https://mariadb.com/resources/blog/using-sqlalchemy-with-mariadb-connector-python-part-2/

#### Autocommit
```
import mysql.connector as mariadb
connection = mariadb.connect(user='testdb', password='testdb', database='testdb', host='127.0.0.1')
connection.autocommit=True
# OR
connection = mariadb.connect(user='testdb', password='testdb', database='testdb', host='127.0.0.1',autocommit=True)

```
#### Example (from a link above)
```
import mariadb
import sys

# Connect to MariaDB Platform
try:
    conn = mariadb.connect(
        user="db_user",
        password="db_user_passwd",
        host="192.0.2.1",
        port=3306,
        database="employees"

    )
except mariadb.Error as e:
    print(f"Error connecting to MariaDB Platform: {e}")
    sys.exit(1)

# Get Cursor
cur = conn.cursor()
cur.execute(
    "SELECT first_name,last_name FROM employees WHERE first_name=?", 
    (some_name,))
# Print Result-set
for (first_name, last_name) in cur:
    print(f"First Name: {first_name}, Last Name: {last_name}")

# If insert, update or delete have been done
conn.commit()

# Close Connection
conn.close()

```


## SQLAlchemy

#### Example
```
import sqlalchemy
from sqlalchemy.ext.declarative import declarative_base

# Define the MariaDB engine using MariaDB Connector/Python
engine = sqlalchemy.create_engine("mariadb+mariadbconnector://app_user:Password123!@127.0.0.1:3306/company")

# Mapping to data
Base = declarative_base()
class Employee(Base):
    __tablename__ = 'employees'
    id = sqlalchemy.Column(sqlalchemy.Integer, primary_key=True)
    first_name = sqlalchemy.Column(sqlalchemy.String(length=100))
    last_name = sqlalchemy.Column(sqlalchemy.String(length=100))
    active = sqlalchemy.Column(sqlalchemy.Boolean, default=True)
    
    
# Create a session
Session = sqlalchemy.orm.sessionmaker()
Session.configure(bind=engine)
Session = Session()

# Insert data
newEmployee = Employee(firstname=”Rob”, lastname=”Hedgpeth”)
session.add(newEmployee)
session.commit()
# Selecting data
employees = session.query(Employee).all()
employee = session.query(Employee).get(1)
employee = session.query(Employee).filter_on(firstname=”Rob”)
# Updating
employee = session.query(Employee).get(1)
employee.firstname = “Robert”
session.commit()
# Deleting
session.query(Employee).filter(Employee.id == id).delete()
session.commit()

```


#### Installation
```
# SQLAlchemy
pip3 install mariadb SQLAlchemy


```




