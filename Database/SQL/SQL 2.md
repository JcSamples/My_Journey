
# SQL Commands

## DML Commands (Data Manipulation Language)
These commands are used for data manipulation, such as viewing, inserting, deleting, and updating data in tables.

## DDL Commands (Data Definition Language)
These commands are used to change table structures, such as creating, altering, and dropping tables.

### Display All Records and Columns
There are four main commands: `SELECT`, `INSERT`, `DELETE`, and `UPDATE`.

1. **SELECT \<Column\>**  
2. **FROM \<Table\>**

Example:
```sql
SELECT *
FROM Movies;
```

### Display Specific Columns
Example:
```sql
SELECT Name, Year, Genre 
FROM Movies;
```

### Performing Calculations
The table is rated from 0 to 10; if we want to scale it from 0 to 20:
```sql
SELECT Name, Rating, Rating * 2 AS Scale20
FROM Movies;
```

### Query to Show the Name of Each Movie and How Old the Movie Is
```sql
SELECT Name, Year, 2024 - Year AS Age
FROM Movies;
```

### Assign Temporary Names to Columns (Aliases)
```sql
SELECT Name, Year, 2024 - Year AS Duration
FROM Movies;
```

### Manipulating Columns with Spaces
```sql
SELECT Name AS [Movie Name], [Duration (MIN)] AS [Movie Duration]
FROM Movies;
```

### Sorting Records
Sort records with `ORDER BY` in ascending or descending order. `ORDER BY` is always the last optional command.
```sql
SELECT Name, Year
FROM Movies
ORDER BY Year DESC;
```

You can also sort by column position:
```sql
SELECT Name, Year
FROM Movies
ORDER BY 2 DESC;
```

### Eliminating Duplicates with `DISTINCT`
```sql
SELECT DISTINCT Country
FROM Actors;
```

### Filtering Records with `WHERE`
The `WHERE` clause is the first optional clause used to filter rows.
```sql
SELECT *
FROM Movies
WHERE Year = 2000;
```

### Using `AND` / `OR` Operators
Example:
```sql
SELECT *
FROM Movies
WHERE Year >= 2000 AND Year <= 2005;
```

### Using `BETWEEN`
The `BETWEEN` clause is inclusive.
```sql
SELECT Name, Year
FROM Movies
WHERE Year BETWEEN 2000 AND 2005;
```

### Negating with `NOT`
```sql
SELECT Year
FROM Movies
WHERE Year NOT BETWEEN 2000 AND 2005;
```

### Text Manipulation with `LIKE`
Wildcards:
- `%` = 0 or more characters
- `_` = exactly one character
```sql
SELECT *
FROM Movies
WHERE Genre LIKE '%Drama%';
```

### Aggregation Functions
Examples:
- `MIN()`
- `MAX()`
- `AVG()`
- `SUM()`
- `COUNT()`
```sql
SELECT MAX(Year), MIN(Year)
FROM Movies;
```

### Subqueries
A subquery can be used to retrieve data used in the main query.
```sql
SELECT *
FROM Movies
WHERE Year = (SELECT Year FROM Movies WHERE Name = 'Example Movie');
```

### Working with Multiple Tables (Joins)
Example: Show the movie name and the respective main actor.
```sql
SELECT Movies.Name, Actors.Name
FROM Movies, Actors, Participation
WHERE Movies.ID = Participation.MovieID AND Participation.ActorID = Actors.ID;
```

### `INSERT` Command
Inserting a new movie:
```sql
INSERT INTO Movies (ID, Name, Year)
VALUES (161, 'Example Movie', 2023);
```

### `UPDATE` Command
Updating records:
```sql
UPDATE Movies
SET Rating = 5
WHERE Year = 2000;
```

### `DELETE` Command
Deleting records:
```sql
DELETE FROM Movies
WHERE DirectorID IS NULL;
```
