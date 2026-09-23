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

##  Insert Data

### Insert Authors

```sql
INSERT INTO authors (
    id, name, nationality, birth_year, death_year
) VALUES
    (1, 'George Orwell', 'British', 1903, 1950),
    (2, 'Harper Lee', 'American', 1926, 2016),
    (3, 'F. Scott Fitzgerald', 'American', 1896, 1940),
    (4, 'Aldous Huxley', 'British', 1894, 1963),
    (5, 'J.D. Salinger', 'American', 1919, 2010),
    (6, 'Herman Melville', 'American', 1819, 1891),
    (7, 'Jane Austen', 'British', 1775, 1817),
    (8, 'Leo Tolstoy', 'Russian', 1828, 1910),
    (9, 'Fyodor Dostoevsky', 'Russian', 1821, 1881),
    (10, 'J.R.R. Tolkien', 'British', 1892, 1973);
```

### Insert Books

```sql
INSERT INTO books (
    id, title, author_id, genres, published_year, available
) VALUES
    (1, '1984', 1,ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
    (2, 'To Kill a Mockingbird', 2,ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
    (3, 'The Great Gatsby', 3,   ARRAY['Tragedy'], 1925, TRUE),
    (4, 'Brave New World', 4,ARRAY['Dystopian', 'Science Fiction'], 1932, TRUE),
    (5, 'The Catcher in the Rye', 5,ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
    (6, 'Moby-Dick', 6,ARRAY['Adventure Fiction'], 1851, TRUE),
    (7, 'Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
    (8, 'War and Peace', 8,ARRAY['Historical Novel'], 1869, TRUE),
    (9, 'Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866,TRUE),
    (10, 'The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);
```

### Insert Patrons

```sql
INSERT INTO patrons (
    id, name, email, borrowed_books
) VALUES
    (1, 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
 (2, 'Bob Smith', 'bob@example.com', ARRAY[1, 2]),
    (3, 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
    (4, 'David Brown', 'david@example.com', ARRAY[3]),
    (5, 'Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
    (6, 'Frank Moore', 'frank@example.com',ARRAY[4, 5]),
    (7, 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
    (8, 'Hank Wilson', 'hank@example.com', ARRAY[6]),
    (9, 'Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
    (10, 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);
```

---