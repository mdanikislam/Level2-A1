
## 🔹 Interfaces এবং Types এর মধ্যে পার্থক্য

TypeScript-এ interface এবং type দুটোই ডেটার গঠন বা structure নির্ধারণ করতে ব্যবহৃত হয়। তবে তাদের মধ্যে কিছু গুরুত্বপূর্ণ পার্থক্য আছে।

### **1. Interface মূলত object-এর shape নির্ধারণে ব্যবহৃত হয়**
একই নামের interface একাধিকবার declare করা যায় এবং TypeScript সেগুলো merge করে।  
এটাকে বলা হয় “declaration merging”.

### **2. Type alias আরও flexible**
Type শুধু object-ই নয়—  
primitive, union, tuple, function type—প্রায় সবকিছু represent করতে পারে।

### **3. Interface extend করা সহজ**
```ts
interface A { name: string }
interface B extends A { age: number }
Type-এ extend করতে হয় intersection দিয়ে:

ts
Copy code
type A = { name: string }
type B = A & { age: number }
সারসংক্ষেপ
Interface → structure focused

Type → general-purpose alias, আরও flexible

🔹 keyof কীওয়ার্ডের ব্যবহার
keyof কোনো object type-এর সমস্ত property নামকে union আকারে বের করে আনে।

উদাহরণ:
ts
Copy code
type User = {
  id: number;
  name: string;
  email: string;
};

type Keys = keyof User;
// ফলাফল: "id" | "name" | "email"
এটি তখন খুবই উপকারী হয় যখন dynamic property access করতে হয়।

🔹 any, unknown এবং never এর মধ্যে পার্থক্য
any
যে কোনো কিছু assign করা যায়

TypeScript type-checking বন্ধ করে দেয়

ভুল হওয়ার সম্ভাবনা বেশি

unknown
সব ধরনের ডেটা রাখা যায়

কিন্তু ব্যবহার করার আগে type-check বাধ্যতামূলক

নিরাপদ any বলা যায়

never
কখনোই ঘটে না এমন value

যেমন: যেসব function কখনো return করে না (error throw করে)

🔹 enums কি কাজে লাগে? উদাহরণসহ
Enum হচ্ছে related value-এর একটি গ্রুপকে readable এবং meaningful নাম দিয়ে উপস্থাপন করা।

Numeric Enum
ts
Copy code
enum Direction {
  North = 1,
  South,
  East,
  West
}
String Enum
ts
Copy code
enum Status {
  Active = "ACTIVE",
  Pending = "PENDING",
  Disabled = "DISABLED"
}
Enums কোডকে আরও readable এবং maintainable করে।

🔹 Union এবং Intersection Types উদাহরণসহ ব্যাখ্যা
Union Type
একটি ভেরিয়েবল একাধিক ধরনের মান রাখতে পারে।

ts
Copy code
let value: string | number;
value = "Hello";
value = 20;
Intersection Type
দুই বা তার বেশি type merge করা হয়।

ts
Copy code
type Person = { name: string }
type Employee = { id: number }

type Staff = Person & Employee;
// { name: string; id: number }
