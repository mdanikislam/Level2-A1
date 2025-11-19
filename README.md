# TypeScript Interview QnA  

---

## **1. What are some differences between interfaces and types in TypeScript?**

TypeScript-এ `interface` এবং `type` দুটোই কোনো object-এর structure নির্ধারণে ব্যবহৃত হয়, কিন্তু তাদের মধ্যে কিছু পার্থক্য আছে।

###  Interface
- মূলত object-এর shape নির্ধারণে ব্যবহৃত হয়।
- এক নামের একাধিক interface declare করলে TypeScript সেগুলো **merge** করে (declaration merging)।
- সহজে `extends` দিয়ে inherit করা যায়।

###  Type
- আরও flexible—primitive, union, tuple, function type সবকিছু represent করতে পারে।
- declaration merging সমর্থন করে না।
- extend করতে হলে intersection ব্যবহার করতে হয়।

### **Examples**
```ts
// Interface extend
interface A { name: string }
interface B extends A { age: number }

// Type intersection extend
type AType = { name: string }
type BType = AType & { age: number }
```

---

## **2. What is the use of the keyof keyword in TypeScript? Provide an example.**

`keyof` কোনো object type-এর সমস্ত property নামকে একটি union আকারে বের করে আনে।

### **Example**
```ts
type User = {
  id: number;
  name: string;
  email: string;
};

type Keys = keyof User;
// "id" | "name" | "email"
```

এটি dynamic property access, generic constraint ইত্যাদিতে খুবই উপকারী।

---

## **3. Explain the difference between any, unknown, and never types in TypeScript.**

###  **any**
- যেকোনো কিছু assign করা যায়।
- TypeScript type-checking বন্ধ হয়ে যায়।
- ভুল হওয়ার ঝুঁকি বেশি।

###  **unknown**
- যে কোনো value assign করা যায়।
- কিন্তু ব্যবহার করার আগে type-check করতে হয়।
- এটি safer version of `any`।

###  **never**
- এমন value যা কখনই ঘটে না।
- যেমন error throw করা function বা infinite loop।

### **Example**
```ts
let a: any = "Hello";
let b: unknown = "Hello";

function error(): never {
  throw new Error("Something went wrong");
}
```

---

## **4. What is the use of enums in TypeScript? Provide an example of a numeric and string enum.**

Enum হল related constant value-এর একটি গ্রুপ। এটি কোডকে আরও readable এবং maintainable করে।

###  Numeric Enum
```ts
enum Direction {
  North = 1,
  South,
  East,
  West
}
```

###  String Enum
```ts
enum Status {
  Active = "ACTIVE",
  Pending = "PENDING",
  Disabled = "DISABLED"
}
```

---

## **5. Provide an example of using union and intersection types in TypeScript.**

###  Union Type
একটি ভেরিয়েবল একাধিক ধরনের মান রাখতে পারে।

```ts
let value: string | number;
value = "Hello";
value = 20;
```

###  Intersection Type
দুটি type merge করে একটি নতুন type তৈরি করা হয়।

```ts
type Person = { name: string }
type Employee = { id: number }

type Staff = Person & Employee;
// { name: string; id: number }
```

---
