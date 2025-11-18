# Prisma CRUD Operations Guide (সহজ বাংলা ব্যাখ্যা)

এই README.md ফাইলটিতে তুমি যে Prisma ফাংশনগুলো ব্যবহার করেছো সেগুলোর খুবই সহজ ভাষায় ব্যাখ্যা দেওয়া হলো — যাতে **যে কেউ সহজে বুঝতে পারে**। তুমি চাইলে এগুলো তোমার Prisma প্রজেক্টের ডকুমেন্টেশন হিসেবে ব্যবহার করতে পারবে।

---

## 📌 Prisma কি?

Prisma হচ্ছে একটি ORM (Object Relational Mapper) — যেটা তোমাকে ডাটাবেসের সঙ্গে সহজে কাজ করতে সাহায্য করে। SQL লিখতে না হয়, বরং JavaScript/TypeScript দিয়ে ডাটাবেসের কাজ করা যায়।

এই ডকুমেন্টেশনে আমরা দেখবো:

* ডাটা **Create** করা
* ডাটা **Read** করা
* ডাটা **Update** করা
* ডাটা **Delete** করা
* ডাটা **Search** করা
* ডাটা **Sort** করা

তোমার টেবিলের নাম: **userFriend**

---

# 📚 প্রতিটি Prisma Function এর সহজ ব্যাখ্যা

## 1️⃣ সব ইউজার পাওয়া (findMany)

```ts
const getAllUserFriend = async () => {
    const result = await prisma.userFriend.findMany({
        where: { id: 2 }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.findMany()` ব্যবহার করা হয় **অনেকগুলো রো** পাওয়ার জন্য।
* এখানে তুমি শুধু এমন ইউজার নিচ্ছো যার **id = 2**।
* সাধারণত সব ইউজার পেতে findMany() *without where condition* ব্যবহার করা হয়।

---

## 2️⃣ নতুন ইউজার তৈরি (create)

```ts
const createUserFriend = async () => {
    const result = await prisma.userFriend.create({
        data: {
            neme: "Anisha",
            email: "mj.dev.jihad@gmail.com"
        }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.create()` দিয়ে ডাটাবেসে **নতুন একটি রেকর্ড** যোগ করা হয়।
* `data` এর ভিতরে যেসব ফিল্ড দেবে সেগুলো ডাটাবেসে সেভ হবে।

---

## 3️⃣ আইডি দিয়ে ইউজার খুঁজে পাওয়া (findUnique)

```ts
const findUserFridndById = async () => {
    const result = await prisma.userFriend.findUnique({
        where: { id: 5 }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.findUnique()` **একটি নির্দিষ্ট রো** ফেরত দেয়।
* Unique ফিল্ড (যেমন — id) দিয়ে সার্চ করার জন্য ব্যবহার হয়।

---

## 4️⃣ একটি ইউজার আপডেট করা (update)

```ts
const updateOne = async () => {
    const result = await prisma.userFriend.update({
        where: { id: 2 },
        data: {
            neme: "Hossain Mohammad Earsad",
            email: "earsad.prime@gmail.com"
        }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.update()` দিয়ে **একটি নির্দিষ্ট ইউজার** আপডেট করা হয়।
* `where` এ unique value দিতে হয় (যেমন — id)।

---

## 5️⃣ অনেকগুলো ইউজার আপডেট করা (updateManyAndReturn)

```ts
const updateMany = async () => {
    const result = await prisma.userFriend.updateManyAndReturn({
        where: { address: null },
        data: { address: "Not Provided" }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* এটা একসাথে **অনেকগুলো রো** আপডেট করতে ব্যবহার হয়।
* এখানে address যাদের null তাদের address সেট করা হচ্ছে — **"Not Provided"**।

> ⚠️ *নোট:* `updateManyAndReturn()` Prisma-এর কোর ফাংশন নয়, এটি একটি extension।

---

## 6️⃣ একটি ইউজার ডিলিট করা (delete)

```ts
const deleteOne = async () => {
    const result = await prisma.userFriend.delete({
        where: { id: 1 }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.delete()` দিয়ে **একটি নির্দিষ্ট ইউজার** ডিলিট করা হয়।
* এখানেও `where` এ unique মান (id) দিতে হয়।

---

## 7️⃣ অনেকগুলো ইউজার ডিলিট করা (deleteMany)

```ts
const deleteMany = async () => {
    const result = await prisma.userFriend.deleteMany({
        where: {
            id: { gte: 3 }
        }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* `.deleteMany()` দিয়ে **একসাথে অনেকগুলো রেকর্ড** ডিলিট করা হয়।
* এখানে id যাদের 3 বা তার বেশি — তাদের ডিলিট হবে।

---

## 8️⃣ ডাটা Sort করা (orderBy)

```ts
const sortingData = async () => {
    const result = await prisma.userFriend.findMany({
        orderBy: {
            id: "desc"
        }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* ডাটাকে Ascending/Descending ভাবে সাজানোর জন্য ব্যবহার করা হয়।
* এখানে **id অনুযায়ী descending** ভাবে সাজানো হয়েছে।

---

## 9️⃣ ইউজার সার্চ করা (contains + OR)

```ts
const searchaingUser = async () => {
    const result = await prisma.userFriend.findMany({
        where: {
            OR: [
                { neme: { contains: "Anisha", mode: "insensitive" } },
                { neme: { contains: "Anisha", mode: "insensitive" } }
            ]
        },
        orderBy: { neme: "asc" }
    });
    console.log(result);
};
```

### 👉 ব্যাখ্যা:

* এখানে `contains` ব্যবহার করে **substring search** করা হচ্ছে।
* `mode: "insensitive"` মানে **A = a**, case sensitive নয়।
* `OR` মানে — যে কোন একটি শর্ত সত্য হলেই রো ফিরে আসবে।
* শেষে `orderBy` দিয়ে নাম অনুযায়ী সাজানো হয়েছে।

---

# ✅ Summary Table

| Function   | কাজ                   |
| ---------- | --------------------- |
| findMany   | অনেক ইউজার পাওয়া      |
| create     | নতুন ইউজার যোগ করা    |
| findUnique | নির্দিষ্ট ইউজার পাওয়া |
| update     | এক ইউজার আপডেট        |
| updateMany | অনেক ইউজার আপডেট      |
| delete     | এক ইউজার ডিলিট        |
| deleteMany | অনেক ইউজার ডিলিট      |
| orderBy    | ডাটা সাজানো           |
| contains   | সার্চ করা             |

---

