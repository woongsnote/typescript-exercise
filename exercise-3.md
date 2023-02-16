# Exercise 3

## Link

<https://typescript-exercises.github.io/#exercise=3&file=%2Findex.ts>

## Intro

Since we already have some of the additional
    information about our users, it's a good idea
    to output it in a nice way.

## Exercise

Fix type errors in logPerson function.
logPerson function should accept both User and Admin and should output relevant information according to the input: occupation for User and role for Admin.

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

export type Person = User | Admin;

export const persons: Person[] = [
    {
        name: 'Max Mustermann',
        age: 25,
        occupation: 'Chimney sweep'
    },
    {
        name: 'Jane Doe',
        age: 32,
        role: 'Administrator'
    },
    {
        name: 'Kate Müller',
        age: 23,
        occupation: 'Astronaut'
    },
    {
        name: 'Bruce Willis',
        age: 64,
        role: 'World saver'
    }
];

export function logPerson(person: Person) {
    let additionalInformation: string;
    if (person.role) {
        additionalInformation = person.role;
    } else {
        additionalInformation = person.occupation;
    }
    console.log(`- ${person.name}, ${person.age}, ${additionalInformation}`);
}

persons.forEach(logPerson);
```

## Solution

> why?

- Person은 User 와 Admin 의 합집함이어서, logPerson 함수에서 타입 가드가 필요한 상황

> how?

- 타입 가드를 위해 in 연산자를 사용
- `person.role` 을 `'role' in person` 으로 변경하여 해결.

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
        name: 'Max Mustermann',
        age: 25,
        occupation: 'Chimney sweep'
    },
    {
        name: 'Jane Doe',
        age: 32,
        role: 'Administrator'
    },
    {
        name: 'Kate Müller',
        age: 23,
        occupation: 'Astronaut'
    },
    {
        name: 'Bruce Willis',
        age: 64,
        role: 'World saver'
    }
];

export function logPerson(person: Person) {
    let additionalInformation: string;
    if ('role' in person) {
        additionalInformation = person.role;
    } else {
        additionalInformation = person.occupation;
    }
    console.log(`- ${person.name}, ${person.age}, ${additionalInformation}`);
}

persons.forEach(logPerson);
```

### hint

 <https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing>
