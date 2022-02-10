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

# Aliases
- this is invalid
```gql
{
  hero(name: "Han"){
    id
    role
  }
  hero(name: "Luke"){
    id
    role
  }
}
```
- so use aliases
```gql
{
  hero1: hero(name: "Luke"){
    id
    role
  }
}
```
# Fragments
- in the above code without aliases. `id role` is duplicated, to minimize duplication, use fragments
```gql
{
  hero1: hero(name: "Han"){
    ...fragmentedFields
  }
  hero2: hero(name: "Luke"){
    ...fragmentedFields
  }
}

fragment fragmentedFields on FieldType {
  id
  name
}
```
- Fragments can be written inline as well
```gql
{
  hero(name: "Han"){
    name
    ... on Type1 {
      field1
    }
    ... on Type2 {
      field2
    }
  }
}
```

# Directives
- variables can allow fetching different data from same query
- to change the shape of query conditionally, can use Directives
- `@include & @skip`
```gql
query Name($var:Int, $flag: Boolean){
  hero(id:$var){
    name
    friends @include(if : $flag){
      name
      id
    }
  }
}
# will return name & friends's name+id if flag is set
```