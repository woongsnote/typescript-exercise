# Exercise 8

## Link

<https://typescript-exercises.github.io/#exercise=8&file=%2Findex.ts>

## Intro

Project grew and we ended up in a situation with some users starting to have more influence.
Therefore, we decided to create a new person type called PowerUser which is supposed to combine
everything User and Admin have.

## Exercise

Define type PowerUser which should have all fields from both User and Admin (except for type),
and also have type 'powerUser' without duplicating all the fields in the code.

## Question

```ts
interface User {
  type: "user";
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  type: "admin";
  name: string;
  age: number;
  role: string;
}

type PowerUser = unknown;

export type Person = User | Admin | PowerUser;

export const persons: Person[] = [
  {
    type: "user",
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  { type: "admin", name: "Jane Doe", age: 32, role: "Administrator" },
  { type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut" },
  { type: "admin", name: "Bruce Willis", age: 64, role: "World saver" },
  {
    type: "powerUser",
    name: "Nikki Stone",
    age: 45,
    role: "Moderator",
    occupation: "Cat groomer",
  },
];

function isAdmin(person: Person): person is Admin {
  return person.type === "admin";
}

function isUser(person: Person): person is User {
  return person.type === "user";
}

function isPowerUser(person: Person): person is PowerUser {
  return person.type === "powerUser";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  if (isPowerUser(person)) {
    additionalInformation = `${person.role}, ${person.occupation}`;
  }
  console.log(`${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

console.log();

console.log("Power users:");
persons.filter(isPowerUser).forEach(logPerson);
```

## Solution

> why?

- PowerUser의 type이 unknown이어서 생긴 문제

> how?

- PowerUser의 type을 선언함으로써 해결.
- 중복된 코드를 사용하지 않는 조건이 있었으므로, `Omit`과 `&`을 활용해서 선언함.

```ts
interface User {
  type: "user";
  name: string;
  age: number;
  occupation: string;
}

interface Admin {
  type: "admin";
  name: string;
  age: number;
  role: string;
}

type PowerUser = {
  type: "powerUser";
} & Omit<User, "type"> &
  Omit<Admin, "type">;

export type Person = User | Admin | PowerUser;

export const persons: Person[] = [
  {
    type: "user",
    name: "Max Mustermann",
    age: 25,
    occupation: "Chimney sweep",
  },
  { type: "admin", name: "Jane Doe", age: 32, role: "Administrator" },
  { type: "user", name: "Kate Müller", age: 23, occupation: "Astronaut" },
  { type: "admin", name: "Bruce Willis", age: 64, role: "World saver" },
  {
    type: "powerUser",
    name: "Nikki Stone",
    age: 45,
    role: "Moderator",
    occupation: "Cat groomer",
  },
];

function isAdmin(person: Person): person is Admin {
  return person.type === "admin";
}

function isUser(person: Person): person is User {
  return person.type === "user";
}

function isPowerUser(person: Person): person is PowerUser {
  return person.type === "powerUser";
}

export function logPerson(person: Person) {
  let additionalInformation: string = "";
  if (isAdmin(person)) {
    additionalInformation = person.role;
  }
  if (isUser(person)) {
    additionalInformation = person.occupation;
  }
  if (isPowerUser(person)) {
    additionalInformation = `${person.role}, ${person.occupation}`;
  }
  console.log(`${person.name}, ${person.age}, ${additionalInformation}`);
}

console.log("Admins:");
persons.filter(isAdmin).forEach(logPerson);

console.log();

console.log("Users:");
persons.filter(isUser).forEach(logPerson);

console.log();

console.log("Power users:");
persons.filter(isPowerUser).forEach(logPerson);
```

### hint

<https://www.typescriptlang.org/docs/handbook/utility-types.html>
