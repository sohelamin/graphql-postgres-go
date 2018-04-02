
# GraphQL with Golang
> A GraphQL complete example using Golang & PostgreSQL

## Installation
Install the dependencies
```
go get github.com/graphql-go/graphql
go get github.com/graphql-go/handler
go get github.com/lib/pq
```

Install & create postgres database
```
brew install postgres
createuser graphql --createdb
createdb graphql -U graphql
psql graphql -U graphql
```
Note: Non-Mac users follow official doc to install the `PostgreSQL`

Create the tables
```sql
CREATE TABLE IF NOT EXISTS authors
(
    id serial PRIMARY KEY,
    name varchar(100) NOT NULL,
    email varchar(150) NOT NULL,
    created_at date
);

CREATE TABLE IF NOT EXISTS posts
(
    id serial PRIMARY KEY,
    title varchar(100) NOT NULL,
    content text NOT NULL,
    author_id int,
    created_at date
);
```

 ## Usage
 Query to get the all authors
```
query {
  authors {
    id
    name
    email
    created
  }
}
```

Query to get a specific author
```
query {
  author(id: 1) {
    id
    name
    email
  }
}
```

Create new author using mutation
```
mutation {
  createAuthor(name: "Sohel Amin", email: "sohelamincse@gmail.com") {
    id
    name
    email
  }
}
```

Update an author using mutation
```
mutation {
  updateAuthor(id: 2, name: "Sohel Amin Shah", email: "sohel@sohelamin.com") {
    id
    name
    email
  }
}
```

Delete an author using mutation
```
mutation {
  deleteAuthor(id: 2) {
    id
  }
}
```

Query to get the posts with its relation author
```
query {
  posts {
    id
    title
    content
    author {
      id
      name
      email
    }
  }
}
```
