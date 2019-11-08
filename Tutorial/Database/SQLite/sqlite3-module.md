
Python SQLite
===

## Create Database

```py
import os
import sqlite3

db_filename = 'journaldev.db'

db_exists = not os.path.exists(db_filename)
connection = sqlite3.connect(db_filename)

if db_exists:
    print('No schema exists.')
else:
    print('DB exists.')
connection.close()
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/create-database.png)

## Create Table


![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/table-schema.png)








> Source : [journaldev.com](https://www.journaldev.com/20515/python-sqlite-tutorial).
<!--stackedit_data:
eyJoaXN0b3J5IjpbODAzMjQwMzU0LDE2MjY3NTkwNzhdfQ==
-->