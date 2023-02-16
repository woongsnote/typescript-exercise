# Exercise 1

## Link

<https://typescript-exercises.github.io/#exercise=1&file=%2Findex.ts>

## Intro

We are starting a small community of users.
For performance reasons we have decided to store all users right in the code.
This way we can provide our developers with more user-interaction opportunities. With user-related data, at least.
All the GDPR-related issues will be solved some other day.
This would be the base for our future experiments during these exercises.

## Exercise

Given the data, define the interface "User" and use it accordingly.

## Question

```ts
export type User = unknown;

export const users: unknown[] = [
  {
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  {
    name: "Kate Müller",
    age: 23,
    occupation: "Astronaut",
  },
];

export function logPerson(user: unknown) {
  console.log(` - ${user.name}, ${user.age}`);
}

console.log("Users:");
users.forEach(logPerson);
```

## Solution

> why?

- User에 대한 Interface가 없어서 생긴 문제

> how?

- 해당 Interface를 정의하여 해결

```ts
export interface User = {
    name: string;
    age: number;
    occupation: string;
}

export const users: User[] = [
    {
        name: 'Max Mustermann',
        age: 25,
        occupation: 'Chimney sweep'
    },
    {
        name: 'Kate Müller',
        age: 23,
        occupation: 'Astronaut'
    }
];

export function logPerson(user: User) {
    console.log(` - ${user.name}, ${user.age}`);
}

console.log('Users:');
users.forEach(logPerson);

```

### hint

<https://www.typescriptlang.org/docs/handbook/2/objects.html>
