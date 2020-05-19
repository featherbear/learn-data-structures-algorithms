---
title: "Custom Data Types (Structs)"
layout: "bundle"
outputs: ["Reveal"]
date: 2020-05-19T23:12:48+10:00
---

{{< slide class="center">}}

## Custom Data Types (Structs)

---

{{< slide transition="fade" >}}

## Custom Data Types (Structs)

All forms of digital data (strings, integers, chars, floats, etc...) are ultimately all just 1s and 0s in the system.  

Their _data type_ is what allows their binary information to be interpreted in different meanings.

{{% fragment %}}It would be very useful if we were able to define and use our own type definitions{{% /fragment %}}

---

{{< slide transition="fade" >}}

## Custom Data Types (Structs)

Let's consider some things to define a Person.  

{{% section %}}

We would need a name, age, and perhaps an address.

```c
char name[] = "John Citizen";
int age = 30;
char address[] = "1234 Street St";
```

---

What if we had to define two people?

```c
char name_1[] = "John Citizen";
int age_1 = 30;
char address_1[] = "1234 Street St";

char name_2[] = "Jane Smith";
int age_2 = 25;
char address_2[] = "555 Main St";
```

{{% fragment %}}This looks like it can grow out of hand...{{% /fragment %}}

{{% /section %}}

---

{{< slide transition="fade" >}}

## Custom Data Types (Structs)

We can create a data structure in C using a `struct`.

> ```c
struct structure_name {
    char your;
    int data;
    char here[];
};
```

{{% fragment %}}For example
```c
struct Person {        // Create a type 'struct Person'
    char name[30];     // Create a string variable
    int age;           // Create an age variable
    char address[100]; // Create an address variable
};
```

---

## Aside: Structs vs Class

> `struct != class`

In languages that implement the Object Oriented Programming (OOP) paradigm, a struct may look similar to a `class` or an `object`.  

A `struct` is purely a data structure whereas an object is 'alive' and can perform functions. With `struct`s, it is up to external code to access and modify the data.

---

## Using structs

> ```c
struct Person {
    char name[30];
    int age;
    char address[100];
};
```

{{% section %}}To define a variable with our Person data type

> ```c
struct Person p;

// We can then initialise values  
p.name = "John Citizen";
p.age = 30;
p.address= "1234 Street St";
```

---

We can also define and assign our values together

> ```c
struct Person p = {
    .age = 30,
    .name = "John Citzen",
    .address = "1234 Street St"
};
```

Note: We prepend a `.` before each variable name

---

If our data values are declared in the same order as they are defined, then we can do this

> ```c
struct Person p = {
    "John Citzen", 30, "1234 Street St"
};
```

{{% /section %}}

---

## Accessing structs

> ```c
struct Person p = {
    .name = "John Citzen",
    .age = 30,
    .address = "1234 Street St"
};
```

We can access a values from the struct

```c
printf("Name: %s\n", p.name); // Output => Name: John Citizen
printf("Age: %d\n", p.age);   // Output => Age: 30
printf("Name: %s\n", p.name); // Output => Address: 1234 Str
```

---

## Struct Size

The size of a struct is the sum of its component sizes.

{{% section %}}

> ```c
struct Person {
    char name[30];
    int age;
    char address[100];
};
```

What is the size of `struct Person`?
{{%fragment%}}`sizeof(struct Person) == 134`{{%/fragment%}}

---

> ```c
struct Person {
    char* name;
    int age;
    char* address;
};
```

What is the size of `struct Person`?
{{%fragment%}}`sizeof(struct Person) == 12`{{%/fragment%}}

{{% /section %}}

---

## Struct Operations

When creating functions that <u>modify</u> `struct`s, we must remember to <u>pass it by reference</u>.  
Otherwise changes will not be saved.

```c
// Pass by reference
void set_age(struct Person *person, int new_age) {
    person->age = new_age;   // This is fine
    (*person).age = new_age; // This is also fine
}
```

```c
// Pass by value
void set_age(struct Person person, int new_age) {
    //                     ^ This is NOT fine!
    person.age = new_age;
}
```