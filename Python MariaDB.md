
#### SQLAlchemy
https://mariadb.com/resources/blog/using-sqlalchemy-with-mariadb-connector-python-part-1/<br>
https://mariadb.com/resources/blog/using-sqlalchemy-with-mariadb-connector-python-part-2/
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




