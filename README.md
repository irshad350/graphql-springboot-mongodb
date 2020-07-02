# graphql-java-spring-boot-mongodb-example
Sample app for building graphql app with spring boot and mongodb. 

You'll need 
[Java 11](https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_windows-x64_bin.zip), 
[MongoDB](https://fastdl.mongodb.org/win32/mongodb-win32-x86_64-2012plus-4.2.6-signed.msi)


Use [http://localhost:9092/graphiql](http://localhost:8080/graphiql) to start executing queries. For example:
```
{
  findAllBooks {
    id
    isbn
    title
    pageCount
    author {
      firstName
      lastName
    }
  }
}
```

Or:
```
mutation {
  newBook(
    title: "Java: The Complete Reference, Tenth Edition", 
    isbn: "1259589331", 
    author: 1) {
      id title
  }
}
```

```
######################################## Query for New Author ########################################
mutation ($one:String!, $two:String!) {
  newAuthor (firstName:$one, lastName:$two) {
    firstName
    lastName
    id
  }
}
# INPUT #
{
  "one":"author_firstname",
  "two":"author_lastname"
}

######################################## Query for New Book ########################################
mutation ($title:String!, $isbn:String!, $pageCount:Int!) {
  newBook(title: $title, isbn: $isbn, pageCount:$pageCount, author: "5ec2245fed342909d54abc2a") {
    title
  }
}

# INPUT #
{
  "title":"Best Java Book",
  "isbn":"i don't know",
  "pageCount":2000
}

######################################## Query for New Book with New Author ########################################
mutation ($title:String!, $isbn:String!, $pageCount:Int!, $authorInput:AuthorInput!) {
  newBookWithNewAuthor(title: $title, isbn: $isbn, pageCount:$pageCount, authorInput: $authorInput) {
    title, 
    author {
      firstName
    }
  }
}

# INPUT #
{
  "title":"newbook",
  "isbn":"newbook-isbn",
  "pageCount":2000,
  "authorInput": {
    "firstName": "isd",
    "lastName": "mhd"
  }
}

######################################## Query for Update Book ########################################

mutation {
  updateBookPageCount(pageCount: 1344, id: "5ec2306600c92e6eb6cc0fee") {
    id pageCount
  }
}

######################################## Query for Delete Book ########################################

mutation {
  deleteBook(id: "5ec2306600c92e6eb6cc0fee")
}
```
