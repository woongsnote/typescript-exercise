# Exercise 2

## Link

<https://typescript-exercises.github.io/#exercise=2&file=%2Findex.ts>

## Intro

All 2 users liked the idea of the community.
We should go forward and introduce some order. We are in Germany after all.
Let's add a couple of admins.

Initially we only had users in the in-memory database.
After introducing Admins, we need to fix the types so that everything works well together.

## Exercise

Type "Person" is missing, please define it and use it in persons array and logPerson function in order to fix all the TS errors.

## Question

```ts
interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = unknown;

export const persons: User[] /*<- Person[]*/ = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(user: User) {
  console.log(`- ${user.name}, ${user.age}`);
}

persons.forEach(logPerson);
```

## Solution

> why?

- Person의 type 정의가 필요

> how?

- Person은 User 와 Admin 의 합집함이므로 **|** 으로 해결 가능함

```ts
interface User {
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  name: string;
  age: number;
  role: string;
}

export type Person = User | Admin;

export const persons: Person[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Jane Doe",
    age: 32,
    role: "Administrator",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
  {
    name: "Bruce Willis",
    age: 64,
    role: "World saver",
  },
];

export function logPerson(user: Person) {
  console.log(`- ${user.name}, ${user.age}`);
}

persons.forEach(logPerson);
```

### hint

<https://www.typescriptlang.org/docs/handbook/2/types-from-types.html>
