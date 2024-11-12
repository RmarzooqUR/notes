- [Misc](#misc)
  - [Remarks](#remarks)
  - [Babel](#babel)
- [Matchers](#matchers)
- [Async](#async)
  - [Callbacks](#callbacks)
  - [Promises, Async/Await](#promises-asyncawait)
    - [Promises](#promises)
    - [resolves/rejects Matchers](#resolvesrejects-matchers)
    - [Async/Await](#asyncawait)
- [Setup/Teardown](#setupteardown)
  - [Order of execution](#order-of-execution)
- [Mocking](#mocking)
  - [Return values and mock functions](#return-values-and-mock-functions)
  - [Modules](#modules)

# Misc
## Remarks
- testing with es6 syntax requires babel/webpack to be configured for jest.
  - no native es6 modules/ arrow functions etc support
- run single test with `test.only` to check whether test fails on its own or when run along with the whole test suite

## Babel
- install babel with `npm install babel-jest @babel/core @babel/preset-env`
- create babel.config.js
- add following
```js
module.exports={
    presets:[
        ['@babel/preset-env',{targets:{node:'current'}}],
        // for typescript support in testing
        // npm install @babel/preset-typescript
        ['@babel/preset-typescript']
    ]
}
```

# Matchers
- `it`, `test` do same thing
- `toBe`, `toEqual` etc are matchers
  - [api ref of all matchers](https://jestjs.io/docs/expect)
- ***for testing exceptions with*** `toThrow`
  - `expect(()=>testingfunc()).toThrow('Error message')`
  - use of wrapping function
- by default tests pass when there is no assumption in a test

# Async
Jest isn't aware by default that a test should run async, so if assertion runs asynchronously,
the assertion would run after the test has already executed.
## Callbacks
- use a `done` param in callback of `it`, this indicates to jest that test is async & it doesn't end the test until `done()` is called,
- call it after expect
- wrap in try/catch to handle failing tests, exception thrown by `expect` is caught
```js
it('test callback', done=>{
  setTimeout(() => {
    try {
      expect(true).toBe(false)
      done()
    } catch (error) {
      done(error)
    }
  }, 1000);
})
```

## Promises, Async/Await
### Promises
- `return` the function which returns the promise and `expect` in the `then`/`catch` block.
  - when using `catch`(i.e. promise was rejected) add `expect.assertions(n)`
    - since a fulfilled promise will not fail the test.
```js
it('promise', ()=>{
  expect.assertions(1)
  return returnsPromise().then((data)=>{
    expect(data).toBe('something');
  }).catch((error)=>{
    expect(error).toBe('error')
  })
})
```
### resolves/rejects Matchers
- `expect` has `resolves/rejects` matcher for cleaner understanding.
```js
return expect(returnsPromise())
  .resolves
  .toBe('resolved')
```

### Async/Await
- use `async` keyword in callback for `it`/`test`. And store the `await` for the `returnsPromise()` in `var`.
  - then use the `var` with `expect()`
- async/await doesnt require use of `return`

# Setup/Teardown
- using `beforeEach(), afterEach(), beforeAll(), afterAll()`.
```js
// user return for Promises
beforeEach(()=>{
  return initializeDB();
})
```
- global `before` & `after` blocks apply to all tests in file by default
- `before, after` in `describe` apply to tests inside the `describe`

## Order of execution
- the `describe` are executed first
- then the `test` run serially
- (up) - reason for running test setup/teardown in `before`/`after` blocks. (since previous setups/teardowns may interfere with later tests' setups and teardowns)

# Mocking
- mock `parameters`, `return values`, `modules` and `implementations`
- mocking a function/module is done by creating a `__mocks__` dir as a sibling of the module to be mocked
  - then create a file of same name as the module to be mocked, inside the `__mocks__` dir
  - use `jest.fn` to mock the functions that are required to be mocked  
- use when -
  - the test uses long running blocks like network calls. which may make the test fragile
  - the code that the current test tests uses other functions which we dont want to run and therefore mock it.
- various properties.
  - `mock.instances`
  - `mock.calls`
- matchers
  - `toHaveBeenCalled`, `toHaveBeenCalledWith()`
  - `expect(mockFunc).toHaveBeenLastCalledWith()`
## Return values and mock functions
- create using `jest.fn()`
- mock return values with `mockReturnValue()` and `mockReturnValueOnce()`
```js
test('mock', ()=>{
  const fnUsedBytestingFn = jest.fn(x=>x+2)
  
  //mock return values as true for first instance and false for all other instances
  fnUsedBytestingFn.mockReturnValueOnce(true).mockReturnValue(false)

  const result = functionBeingtested(x=>{
    // ...
    fnUsedBytestingFn(x)
    // ...
  })

  expect(result).toBe('result')
})
```
## Modules
- using `jest.mock('../path/to/module')`
- example - mocking axios
  - construct expected response.
  - import & mock axios with `jest.mock('axios')`
  - set `mockResolvedValue()` as expected response
  - perform test on the function which uses axios. Jest will use the mocked axios instance rather than actually sending the request via axios.
- **Jest has config *automock* where all imported modules are autmatically mocked**
