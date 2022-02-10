# Setup
- create a new client with 
```js
const client = new ApolloClient({
  uri:'www.graphql_server_.uri',
  cache : new InMemoryCache(),
})
```
- provide it as `<ApolloProvider client={client} >...</ApolloProvider>`

# useQuery Hook
- the useQuery hook allows to query the graphql server using queries defined by a gql statement
```js
const LOAD_STUDENT = gql`query Name($variable: String!) {
  student(id:$variable){
    name
    dob
  }
}`

const { loading, error, data } = useQuery(LOAD_STUDENT, {
  variables : { breed }
})
```
- the useQuery hook is executed on render of the component which contains it.

## useLazyQuery
- for event based(button click) exec of a query
```js
const [ get_student, {loading, error, data }] = useLazyQuery(LOAD_STUDENT)

const handleClick(e => {
  get_student({variables: {breed: 'bulldog'}})
});
```

## Refetching and Polling for cache
- can set a polling config in query
- useQuery also returns `refetch()` method, can be used in event handler to refetch query
```js
const { loading, error, data, refetch } = useQuery(LOAD_STUDENT,{
  variables: { breed },
  pollingInterval:500
})
```
# useMutation Hook
- similarly like query useMutation is to execute mutations
```js
const [ set_student, {loading, error, data}] = useMutation(SET_STUDENT)

handleClick(e => {
  set_student({variables:{ name: name, dob: dob}})
})
```
