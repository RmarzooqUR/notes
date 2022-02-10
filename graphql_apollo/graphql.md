# Why graphql
- graphql allows us to write queries to fetch data, 
  - rather than visit multiple endpoints multiple times(like REST)
    - query1 gives a user_id for supplied username
    - user_id is used to fetch user's purchases using query2
- You can fetch any data with just 1 query.


# Queries
```gql
query QueryName( $variable: String!){
  table(id: $variable) {
    attr1
    attr2 {
      nestead_attr(id: $variable)
    }
  }
}

# specifying QueryName is optional, 
# specifying variables is optional, but then wouldn't be able to use variables in query
query {
  book {
    title
    author {
      books {
        name
      }
    }
  }
}
```

# Mutations
```gql
# specifying FendMutationName is optional
# specifying variables is optional, but then wouldn't be able to use variables in query
mutation FendMutationName( $variable:String! $var: Integer ){
  BendMutationName( data1: $variable, data2: $var) {
    return_data1
    return_data2
  }
}
```
- specifying return data allows us to fetch modified DB instantly