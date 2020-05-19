---
title: "Abstract Data Types"
layout: "bundle"
outputs: ["Reveal"]
date: 2020-05-19T23:15:30+10:00
---

{{< slide class="center" >}}

## Abstract Data Types (ADT)

---

## Abstract Data Types (ADT)

An abstract data type is a `struct`, whose definition is not exposed to the user.  

{{% fragment %}}This is useful for a couple of different reasons

* Prevents internal data from being modified unsafely
* Provides functions which safely use the struct
* Allows implementation without affecting the user
{{% /fragment %}}

---

## Abstract Data Types

To define an ADT we `typedef` our `struct` definition.

> `typedef OLD_TYPE ALIAS;`

{{% fragment %}}For example, `typedef struct Person Person`.  
This will make `Person` an alias of `struct person`.{{% /fragment %}}

{{% fragment %}}By doing so, we have successfully abstracted the `Person` type. We would use `Person` for future uses.  
```c
Person p = { ... };
```
{{% /fragment %}}

---

## ADT to Pointers

As it is very common to pass <u>data by reference</u>, it is recommended to make ADT definitions a pointer.

> ```c
typedef struct Person *Person;
```

This way whenever we use `Person`, we are defining a pointer to a `struct Person`.

{{% fragment %}}If we do not use a pointer type, we must ensure to manually pass reference to our data type in functions, and dereference them when accessing values{{% /fragment %}}

---

## Better ADTs

{{% section %}}
To make an ADT truly abstract, we want to put all ADT code in their own `.h` header and `.c` source files.

`Person.h`
```c
#ifndef _PERSON_H_
#define _PERSON_H_
typedef struct Person *Person; // Define Person as a pointer
#endif                         // to a struct Person
```

`Person.c`
```c
struct Person {
    char* name;
    int age;
    char* address;
};
```

---

We put the function prototypes in the `.h` header, and implementation in the `.c` source.

```c
/* Person.h */
typedef struct Person *Person;
char *get_name(Person p);
int get_age(Person p);
```

```c
/* Person.c */
#include <string.h>

char *get_name(struct Person *p) {
    return (p == NULL || p->name == NULL)
           ? NULL : strdup(p->name0);
}
int get_age(struct Person *p) {
    return p->age;
}
```

---

Without knowing the content of the `.c` source file, we can use the functions declared in the header.

> ```c
/* Person.h */
typedef struct Person *Person;
char *get_name(Person p);
int get_age(Person p);
```

```c
#include <Person.h>

int main(void) {
    Person p = ...;

    printf("Age: %d\n", get_age(p));
}
```

{{% /section %}}