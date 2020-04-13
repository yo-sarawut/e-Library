# SQLite for Python

## Create Database

```python
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

To start working with the database, we must define a table schema on which we will write our further queries and perform operations. Here is the schema we will follow:

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/table-schema.png)

For the same schema, we will be writing related SQL Query next and these queries will be saved in book\_schema.sql:

```python
CREATE TABLE book (
    name        text primary key,
    topic       text,
    published   date
);

CREATE TABLE chapter (
    id           number primary key autoincrement not null,
    name         text,
    day_effort   integer,
    book         text not null references book(name)
);
```

Now let us use the connect\(\) function to connect to the database and insert some initial data using the executescript\(\) function:

```python
import os
import sqlite3

db_filename = 'journaldev.db'
schema_filename = 'book_schema.sql'

db_exists = not os.path.exists(db_filename)

with sqlite3.connect(db_filename) as conn:
    if db_exists:
        print('Creating schema')
        with open(schema_filename, 'rt') as file:
            schema = file.read()
        conn.executescript(schema)

        print('Inserting initial data')

        conn.executescript("""
        insert into book (name, topic, published)
        values ('JournalDev', 'Java', '2011-01-01');

        insert into chapter (name, day_effort, book)
        values ('Java XML', 2,'JournalDev');

        insert into chapter (name, day_effort, book)
        values ('Java Generics', 1, 'JournalDev');

        insert into chapter (name, day_effort, book)
        values ('Java Reflection', 3, 'JournalDev');
        """)
    else:
        print('DB already exists.')
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/create-schema-with-db-test.png)

## Cursor Select

```python
import sqlite3

db_filename = 'journaldev.db'

with sqlite3.connect(db_filename) as conn:
    cursor = conn.cursor()

    cursor.execute("""
    select id, name, day_effort, book from chapter
    where book = 'JournalDev'
    """)

    for row in cursor.fetchall():
        id, name, day_effort, book = row
        print('{:2d} ({}) {:2d} ({})'.format(
            id, name, day_effort, book))
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/fetch-data.png)

## Getting Metadata of Table

```python
import sqlite3

db_filename = 'journaldev.db'

with sqlite3.connect(db_filename) as connection:
    cursor = connection.cursor()

    cursor.execute("""
    select * from chapter where book = 'JournalDev'
    """)

    print('Chapter table has these columns:')
    for column_info in cursor.description:
        print(column_info)
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/table-metadata.png)

## Using Named Parameters

```python
import sqlite3
import sys

db_filename = 'journaldev.db'
book_name = sys.argv[1]

with sqlite3.connect(db_filename) as conn:
    cursor = conn.cursor()

    query = """
    select id, name, day_effort, book from chapter
    where book = :book_name
    """

    cursor.execute(query, {'book_name': book_name})
    for row in cursor.fetchall():
        id, name, day_effort, book = row
        print('{:2d} ({}) {:2d} ({})'.format(
            id, name, day_effort, book))
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/named-parameter.png)

## Transaction Management

```python
import sqlite3

db_filename = 'journaldev.db'

def show_books(conn):
    cursor = conn.cursor()
    cursor.execute('select name, topic from book')
    for name, topic in cursor.fetchall():
        print('  ', name)


with sqlite3.connect(db_filename) as conn1:
    print('Before changes:')
    show_books(conn1)

    # Insert in one cursor
    cursor1 = conn1.cursor()
    cursor1.execute("""
    insert into book (name, topic, published)
    values ('Welcome Python', 'Python', '2013-01-01')
    """)

    print('\nAfter changes in conn1:')
    show_books(conn1)

    # Select from another connection, without committing first
    print('\nBefore commit:')
    with sqlite3.connect(db_filename) as conn2:
        show_books(conn2)

    # Commit then select from another connection
    conn1.commit()
    print('\nAfter commit:')
    with sqlite3.connect(db_filename) as conn3:
        show_books(conn3)
```

![enter image description here](https://cdn.journaldev.com/wp-content/uploads/2018/04/transactions.png)

> Source : [journaldev.com](https://www.journaldev.com/20515/python-sqlite-tutorial).

