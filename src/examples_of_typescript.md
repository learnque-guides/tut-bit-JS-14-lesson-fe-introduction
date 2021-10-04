# Example of TypeScript

```ts
interface Person {
  firstName: string;
  lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName;
} 
```

* Note the :Person type parameter in the argument of the function.
* We can define the structure of our classes in TS. The idea is the same - validation of fields!
* It means that if a value of a different type is given to the function, TS will throw an error!
