# Rust GraphQL API Sample

Rust, Juniper, Diesel, Postgres

## API's

- Sign up
- Sign in
- Change password
- Profile Update
- JWT authentication (json web token)

## Run

```shell
$ git clone https://github.com/benhsampson/rust_graphql_sample
$ cd rust_graphql_sample
$ echo DATABASE_URL=postgres://username:password@localhost/rust_graphql_DB > .env
$ diesel setup
$ diesel migration run
$ cargo run
```

> GraphiQL dashboard available at http://127.0.0.1:3030 Run your queries either here or in Postman

> API route = http://127.0.0.1:3030/query You can use Postman's new graphQl format to run the graphQl queries and mutations. Must use POST. After login, take the token and add it to the Authorization section as an API key (`key=authorization value={whateverjwttoken you got back}`)

## Schema

### Queries

> Note: JSON web token is needed to be sent as `authorization` in header.

> Query my user profile

```graphql
query {
  getMyProfile {
    ok
    error
    user {
      id
      email
      firstName
      lastName
      bio
      avatar
      cells
    }
  }
}
```

> Query my Cells

```graphql
query {
  getMyCells {
    ok
    error
    user {
      id
      lastName
      cells
    }
  }
}
```

### Mutations

> Sign Up

```graphql
mutation {
  signUp(
    email: "test@test.com"
    password: "12345678"
    firstName: "graphql"
    lastName: "rust"
  ) {
    ok
    error
    user {
      id
      email
      firstName
      lastName
      bio
      avatar
      cells
    }
  }
}
```

> Sign In

```graphql
mutation {
  signIn(email: "test@test.com", password: "12345678") {
    token
  }
}
```

> Change Password

Note: JSON web token is needed to be sent as `authorization` in header.

```graphql
mutation {
  changePassword(password: "87654321") {
    ok
    error
    user {
      id
      email
      firstName
      lastName
      bio
      avatar
      cells
    }
  }
}
```

> Change Profile

Note: JSON web token is needed to be sent as `authorization` in header.

```graphql
mutation {
  changeProfile(cells: "1 Nobody Street Anywhere VIC") {
    ok
    error
    user {
      id
      email
      firstName
      lastName
      bio
      avatar
      cells
    }
  }
}
```
