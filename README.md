# Rust GraphQL API Sample

Rust, Juniper, Diesel, Postgres

## API's

- Sign up
- Sign in
- Change password
- Profile Update
- JSON web token authentication

## Run

```shell
$ git clone https://github.com/benhsampson/rust_graphql_sample
$ cd rust_graphql_sample
$ echo DATABASE_URL=postgres://username:password@localhost/rust_graphql_DB > .env
$ diesel setup
$ diesel migration run
$ cargo run
```

## Docker build

```shell
$ docker build -t rust_gql .
$ docker run --rm -d -p 3030:3030 --name my_rust_gql rust_gql
```

> Change the listening port from `127.0.0.1` to `0.0.0.0` in `main.rs`. Because rust GraphQL API in docker container needs to listen to `0.0.0.0` instead of local interfase in order for host to access to the API.

> GraphiQL dashboard available at http://127.0.0.1:3030

> API route = 127.0.0.1:3030/query You can use postman to run the graphQl queries and mutations. Must use POST. After login, take the token and add it to the Authorization section as an API key (`key=authorization value={whateverjwttoken you got back}`)

## Schema

### Query

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
    }
  }
}
```

> Note: JSON web token is needed to be sent as `authorization` in header.

### Mutation

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
    }
  }
}
```

> Change Profile

Note: JSON web token is needed to be sent as `authorization` in header.

```graphql
mutation {
  changeProfile(bio: "Rust fan") {
    ok
    error
    user {
      id
      email
      firstName
      lastName
      bio
      avatar
    }
  }
}
```
