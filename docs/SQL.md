# SQL database

Mashtree saves distances in an SQLite database in the temporary folder.
This folder is automatically deleted at the end of the run unless `--tempdir` is supplied.
This database can be read using SQLite if saved.

## SQLite3

SQLite is a local database management system. To install SQLite on most systems, one of these commands would work.

    yum install sqlite

    apt-get install sqlite

## Reading the database

The database file is `distances.sqlite`. The scheme is very simple with three fields: GENOME1, GENOME2, DISTANCE.

### Sample query

    sqlite3 ./mashtree.tmp/distances.sqlite "SELECT * FROM DISTANCE LIMIT 10"
    PNUSAL003713|PNUSAL003713|0
    PNUSAL003713|PNUSAL002726|0.0340471
    PNUSAL003713|PNUSAL002715|0.0734255
    PNUSAL003713|PNUSAL002259|0.0762603
    PNUSAL003713|PNUSAL002950|0.0687541
    PNUSAL003713|PNUSAL002087|0.0394988
    PNUSAL003713|PNUSAL003138|0.0593789
    PNUSAL003713|PNUSAL003152|0.0234137
    PNUSAL003713|PNUSAL003568|0.0764902
    PNUSAL003713|PNUSAL003827|0.0819654

## Writing to the database

Not recommended but what the heck

### Sample query

    sqlite3 ./mashtree.tmp/distances.sqlite "INSERT INTO DISTANCE VALUES('somegenome1','othergenome',0.01);"
    
This query should work with no error.  However, running it again will yield an error
    
    sqlite3 ./mashtree.tmp/distances.sqlite "INSERT INTO DISTANCE VALUES('somegenome1','othergenome',0.01);"
    Error: UNIQUE constraint failed: DISTANCE.GENOME1, DISTANCE.GENOME2
    