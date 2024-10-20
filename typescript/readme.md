# TypeScript Documentation

TypeScript is a strongly typed, object-oriented, compiled language. It's a superset of JavaScript, meaning all valid JavaScript code is also valid TypeScript code. TypeScript helps catch common errors at compile time, offering better tooling for large-scale applications.

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [TypeScript vs JavaScript](#typescript-vs-javascript)
4. [Basic Concepts](#basic-concepts)
   - [Types](#types)
   - [Functions](#functions)
   - [Classes](#classes)
   - [Interfaces](#interfaces)
   - [Generics](#generics)
5. [Advanced Concepts](#advanced-concepts)
   - [Namespaces](#namespaces)
   - [Modules](#modules)
   - [Decorators](#decorators)
6. [TypeScript Configuration](#typescript-configuration)
7. [Compilation](#compilation)
8. [Conclusion](#conclusion)
9. [Resources](#resources)

## Introduction

TypeScript extends JavaScript by adding static types. By defining types, you can catch errors earlier in the development process, leading to more robust codebases. TypeScript integrates well with JavaScript libraries and frameworks, providing a smooth learning curve for JavaScript developers.

## Installation

To install TypeScript, you'll need Node.js and npm (Node Package Manager) installed on your machine.

1. Install TypeScript globally:
   ```bash
   npm install -g typescript
   ```

2. Check the installation:
   ```bash
   tsc --version
   ```

3. Initialize a TypeScript project:
   ```bash
   tsc --init
   ```

This creates a `tsconfig.json` file, which you can customize for your project.

## TypeScript vs JavaScript

### JavaScript:
- Dynamic typing (types are resolved at runtime).
- No type checking at compile time.
- Errors can go unnoticed until execution.

### TypeScript:
- Static typing (types are declared).
- Compile-time type checking.
- Helps catch type-related errors early.
- Supports modern JavaScript features.

## Basic Concepts

### Types

TypeScript provides several built-in types that help enforce strict type checking in your code. Here's an overview of the most common types:

1. **Primitive Types**:
   - `string`
   - `number`
   - `boolean`
   - `any`
   - `void`
   - `null` and `undefined`

#### Examples:

- **string**:
  ```typescript
  let username: string = "JohnDoe";
  ```

- **number**:
  ```typescript
  let age: number = 25;
  ```

- **boolean**:
  ```typescript
  let isLoggedIn: boolean = true;
  ```

- **any**: (use with caution as it disables type checking)
  ```typescript
  let randomValue: any = 10;
  randomValue = "Hello";
  randomValue = true;
  ```

- **void**: (usually used in functions with no return value)
  ```typescript
  function logMessage(message: string): void {
    console.log(message);
  }
  ```

- **null and undefined**:
  ```typescript
  let n: null = null;
  let u: undefined = undefined;
  ```

2. **Array and Tuple**:

- **Array**:
  ```typescript
  let numbers: number[] = [1, 2, 3, 4, 5];
  ```

- **Tuple**: (an array with fixed types for each index)
  ```typescript
  let person: [string, number] = ["Alice", 30];
  ```

3. **Enum**:

Enums are a way of defining a set of named constants.

```typescript
enum Direction {
    Up,
    Down,
    Left,
    Right
}

let move: Direction = Direction.Up;
```

### Functions

TypeScript enforces typing on both the input parameters and the return value of a function.

#### Examples:

1. **Typed Parameters and Return Value**:
   ```typescript
   function add(x: number, y: number): number {
       return x + y;
   }

   const result = add(5, 10);
   ```

2. **Optional Parameters**:
   You can mark a function parameter as optional by using `?`.

   ```typescript
   function greet(name: string, greeting?: string): string {
       return `${greeting || "Hello"}, ${name}!`;
   }

   greet("Alice");          // Output: "Hello, Alice!"
   greet("Bob", "Hi");      // Output: "Hi, Bob!"
   ```

3. **Default Parameters**:
   ```typescript
   function multiply(a: number, b: number = 2): number {
       return a * b;
   }

   console.log(multiply(5));  // Output: 10
   ```

### Classes

TypeScript supports object-oriented programming with classes. You can define classes with properties, constructors, and methods.

#### Example:
```typescript
class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }

    makeSound(): void {
        console.log(`${this.name} is making a sound.`);
    }
}

const dog = new Animal("Dog");
dog.makeSound();  // Output: Dog is making a sound.
```

### Interfaces

Interfaces in TypeScript are used to define the shape of an object or enforce a contract for classes.

#### Example:
```typescript
interface Student {
    name: string;
    age: number;
    enroll(courseName: string): void;
}

const student: Student = {
    name: "John",
    age: 21,
    enroll: (courseName: string) => console.log(`Enrolled in ${courseName}`),
};
```

### Generics

Generics allow you to create reusable, type-safe components.

#### Example:
```typescript
function identity<T>(arg: T): T {
    return arg;
}

let output1 = identity<string>("Hello, TypeScript");
let output2 = identity<number>(42);
```

## Advanced Concepts

### Namespaces

Namespaces are used to organize code into logical groups and avoid name collisions.

#### Example:
```typescript
namespace MathUtils {
    export function add(a: number, b: number): number {
        return a + b;
    }
}

console.log(MathUtils.add(2, 3));  // Output: 5
```

### Modules

Modules allow you to split code into separate files and import/export functionality between them.

#### Example:

- **math.ts**
  ```typescript
  export function multiply(a: number, b: number): number {
      return a * b;
  }
  ```

- **app.ts**
  ```typescript
  import { multiply } from './math';

  console.log(multiply(2, 3)); // Output: 6
  ```

### Decorators

Decorators are used to modify the behavior of classes or their members.

#### Example:
```typescript
function log(target: any, key: string) {
    console.log(`${key} was called`);
}

class Calculator {
    @log
    add(a: number, b: number): number {
        return a + b;
    }
}

const calculator = new Calculator();
calculator.add(2, 3); // Output: add was called
```

## TypeScript Configuration

TypeScript can be configured using the `tsconfig.json` file. This file allows you to customize how TypeScript should behave during compilation.

#### Example `tsconfig.json`:
```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```

## Compilation

To compile TypeScript into JavaScript, use the `tsc` command:

1. Compile a single file:
   ```bash
   tsc filename.ts
   ```

2. Compile a project (with `tsconfig.json`):
   ```bash
   tsc
   ```

3. Watch for file changes:
   ```bash
   tsc --watch
   ```

TypeScript will output the compiled JavaScript into the specified directory (e.g., `./dist`).

## Conclusion

TypeScript is a powerful language for large-scale applications, providing features like static typing, interfaces, and modern JavaScript support. It enhances the development experience by catching errors early, improving code readability, and enabling better tooling support.

## Resources

- [Official TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [TypeScript GitHub Repository](https://github.com/microsoft/TypeScript)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)