<h1>Last of Array <img src="https://img.shields.io/badge/-medium-eaa648" alt="medium"/> <img src="https://img.shields.io/badge/-%23array-999" alt="#array"/></h1>

## Challenge

> TypeScript 4.0 is recommended in this challenge

Implement a generic `Last<T>` that takes an Array `T` and returns it's last element's type.

For example

```ts
type arr1 = ['a', 'b', 'c']
type arr2 = [3, 2, 1]

type tail1 = Last<arr1> // expected to be 'c'
type tail2 = Last<arr2> // expected to be 1
```

## Solution

When you want to get the last element from the array, you need to get all the elements starting from the head until we find the last element.
It is the flag to use [variadic tuple types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-0.html#variadic-tuple-types); we have an array and we need to work with its elements.

Knowing about variadic tuple types, the solution is pretty obvious.
We need to take anything in the head and the last element.
Combining it with the [type inference in conditional types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-inference-in-conditional-types) makes it easy to infer the last element:

```ts
type Last<T extends any[]> = T extends [...infer X, infer L] ? L : never;
```