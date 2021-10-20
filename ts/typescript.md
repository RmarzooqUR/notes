# Conversion
- Compile ts to js
- `tsc sandbox.ts sandbox.js -w` OR `tsc sandbox.ts -w` - for same names
- `-w` is for watch, automatically compile on change to ts file


# Types
- ts can implicity infer the type of a variable
- in functions, implicit checking of parameters is not done, so pass type explicitly
```js
    const circ = (dia: number)=>dia*Math.PI
```
- CAN NOT redeclare an array/obj as another primitive type
- if arr/obj contains only one type - different type can't be added to it
- for OBJECTS - cant add additional properties

## special explicit types
- arrays
 ```ts
    let arr : string[]
    let arr: string[] = [] //initialize with empty to use array methods
```

- union types
```ts
    let mixed: (string|num)[] = []
    let uid: string|num
    let obj: object;    //declare as any kind of object

    // declaration of this type of objs must have the defined properties
    let obj2: {
        name:string,
        num:number,
    }
```
- any type
    - revert to js functionality

# ts config

- create conf with `tsc --init`
- important settings - rootDir, outDir, include, target
- `tsc -w` - to watch and compile all files in rootDir

# Function type
- can explicitly define a variable as a `Function` type in func exprs
```ts
const greet:Function;
greet = () => console.log('hellos')

// this is a function SIGNATURE
const add = (a: number, b:number, c?:string, d:number=23):void =>{
    console.log(a+b)
}
```
- in above snippet
    - params can have defined types
    - ? is added for optional params
    - default values for params can be used
    - return type can be defined
    - ts also infers return type based on type of value returned

# type aliases
- define type aliases with `type` keyword
```ts
type stringOrNum = string|number;
type objwithName = {name:string, age:stringOrNum}
```

# DOM and HTML type casting

- make a dom request with `let a = document.querySelector('a')` - if tags are passed ts knows the type of the var
- `let elem = document.querySelector('a')!`, ! lets ts compiler know that elem would contain some value

## type casting
- cast types with `as` keyword, you can set the type returned 
```js
let a = document.querySelector('.form_element') as HTMLFormElement
```

# Classes
- in ts you need to define the `constructor()` method
- available access modifiers => public, private, readonly (properties and methods are by default public)
- can define properties within constructor only (no need to define explicitly) `see app.ts`
- if a classname is `Invoice`
```ts
let InvoiceOne:Invoice;
```

# Interfaces
- interfaces are defn of structure of new ts types
- you can set any interface as type of a variable `let variable:interfaceName`
```ts
interface Payment{
    sayHi():void,
    greeting: string
}

class Invoice implements Payment{
    greeting:string = 'hi';
    sayHi():void { console.log('HI')}
}
```

***for an implementation of a react like render function see src/classes/ListTemplate.ts***

- `extends` keyword (extends types)
```ts
interface User extends {name:string}
```

# Generics, Enums and Tuples
## Generics
- with generics `<T>` can capture types
- captured types can be used in functions and interfaces/classes to define behiviour/data of objects respectively
```ts
function <T extends {name:string}>idea(data:T){
    console.log(...data)
}

interface withGeneric<T>{
    name:string,
    data:T
}

const instanceWithGeneric: withGeneric<string[]>  = {
    name:'hello',
    data:['how', 'are','you']
}
//see app.ts for class implementation
```
## Enums
- with keyword `enum`
```ts
enum resourceType { BOOK, APPLE, NEW};
console.log("BOOK-",resourceType.BOOK)
```
- enums can be numerical and string constants and computed
- in above example typescript assigns incremental values to each enum type (0,1,2)
- if the first enum had an initialization the others will have incremental values
- **non initialized enums can't come after computed enums.**
```ts
enum newEnum {
    book = 1,               //constant
    data = getEnumVal(),    //computed enums
    new,                    //constant
    read = 2 << 1;          //computed enums
    len = "const".length    //computed enums
}
```
- useful when using as a switch case.
## Tuples
- with tuples we can define the types of items at specific positions in array
```ts
let newTuple: [string, number, boolean]
```