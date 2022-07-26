# rory
Typescript Standart Library

## Goals
- Perfomance (through types-aware code-generation)
- Type safety

## Features
- [ ] Getter/Setter code generations (Possible composition through lenses?)
```ts
type User = {
  age: UInt32;
  name: string;
}

export const { age, setAge, name, setName } = _rory<User>();
```
- [ ] Safer primitive types, UInt32, Int32, etc
- [ ] Array buffer / JSON endcoders/decoders 
```ts
export const { toArrayBuffer, fromArrayBuffer } = _rory<User>();
```
- [ ] Type class implementations/Traits
```ts

type User = {
  age: UInt32;
  name: string;
}

export const { Ord } = _instance<Ord, User>();

Array.sort(users); // implicitly use User's Ord instance, warn if no Ord instance
```
- [ ] Strctural equality generation
```ts
export { equals } = _rory<User>(); // left === right || left.age === right.age && left.name === right.name
```
- [ ] Sum types guards, contructors, matchers
```ts
type Registered = {
  age: UInt32;
  name: string;
}

// Utility generic to avoid type Anonymous = Data<{ userAgent: string; }> for branding?
type Anonymous = {
  userAgent: string;
}

type User = Sum<Anonymous, Registered>;


export { isRegistered, isAnonymous, match } = _rory<User>();

pipe(user, User.match({
  Registered: ({age}) => `age is ${age}`,
  Anonymous: () => 'hi anon'
}))

```
- [ ] Option, Result, Task
- [ ] As many Iterator helpers as possible (LINQ, more-itertools, etc)
- [ ] Finite/Infinite Iterators
