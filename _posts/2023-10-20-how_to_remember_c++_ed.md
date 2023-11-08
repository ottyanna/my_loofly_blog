---
title: "avoid silly mistakes! c++ LOG"
date: 2023-10-20
#image: /assets/images/logo.png
#categories:
#    - Coding
tags:
    - c++
excerpt: " "
---

Trying to implement a list:

[stack vs heap](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)


[smart pointers](http://labmaster.mi.infn.it/Laboratorio2/serale/l8/index.html)

#### 1 - If you declare a local variable (in a function) it is doomed to die outside the scope.

For example:

```c++
void list::insert (int item, bool headChose){ //Initialize a list

listElem new_list_el(item);

//Then create the list (supposing it's empty)
    if ( this->head == nullptr && this->tail == nullptr ) {
        this->head = new_list_el; // The head and the tail point to the same element
        this->tail = new_list_el;

}
```

The `new_list_element` won't survive outside the function, just the address, so in the `main` the head points to the right address, but that is empty. WHYYYYYYY???

**Note: `this` refers to the list variable**
like I don't need a `baseList` in `void list::insert(list* baseList, int item, int position);` because `this` is the `list* baseList`.

In the `main` you call it as `lista.insert(item,pos)`.

**Note: why is the constructor like this?**

#### 2. If you pass it to the `main` as a value it goes crazy when you add another value as it overwrites the item value

#### 3. If you pass it as an address it goes crazy ... WHYYYY?

#### 4. You could define the listElem in the main so every element has its address and item, but it's not elegant

#### 5. Use the `new listElem(item)` as it creates a new element in the heap where it should be. If you don't need to pass it to the main, you should remember to use the `delete` on the element, as it could lead to a memory leak(?). In this case it is better to delete the list at the end in the main.