# Library Management System

The Library Management System is a PostgreSQL database project designed to manage a library's books, authors, and patrons.

The system allows users to:

- Add books and authors
- View all books
- Search for books by title or ID
- Find books by a specific author
- View available books
- Borrow and return books
- Track books borrowed by patrons
- Delete books and authors
- Perform advanced SQL queries

**Database:** PostgreSQL  
**Tool Used:** pgAdmin 4  

---

##  Project Setup

### Create the Database

In pgAdmin 4, create a database named `LibraryDB`.

Connect to `LibraryDB`, open the **Query Tool**, and run the following commands.

### Create Authors Table

```sql
CREATE TABLE authors (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    nationality VARCHAR(100),
    birth_year INT,
    death_year INT
);
```

### Create Books Table

```sql
CREATE TABLE books (
    id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author_id INT NOT NULL,
    genres TEXT[],
    published_year INT,
    available BOOLEAN DEFAULT TRUE,

    CONSTRAINT fk_books_authors
        FOREIGN KEY (author_id)
        REFERENCES authors(id)
);
```

### Create Patrons Table

```sql
CREATE TABLE patrons (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    borrowed_books INT[] DEFAULT ARRAY[]::INT[]
);
```

---