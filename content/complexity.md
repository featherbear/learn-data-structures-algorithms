---
title: "Complexity"
layout: "bundle"
outputs: ["Reveal"]
date: 2020-05-19T23:34:32+10:00
---

{{< slide class="center" >}}

## Complexity

---

## Complexity

{{% section %}}

To develop efficient programs, it is important to analyse the complexity of our programs and its code.  

{{% fragment %}}Complexity is an average measure of how well a program performs.{{% /fragment %}}

{{% fragment %}}The main measures of complexity, is **time complexity** and **space complexity**{{% /fragment %}}

---

We express complexity in Big-O notation.

For example - `O(n)`  
Where `n` represents the number of items in a data set

{{% /section %}}

---

{{< slide class="center" >}}

## Time Complexity

---

## Time Complexity

{{% section %}}

Time complexity is the average measure of how long an algorithm will take to complete. Often we assess time complexity on searching and sorting algorithms.  

{{%fragment%}}With small data sets, any searching/sorting algorithm will be virtually instant, but with large data sets it can take a long time.{{%/fragment%}}

{{%fragment%}}_There is no 'best' searching/sorting algorithm, as it will depend on the nature of the data._{{%/fragment%}}

---

To calculate the time complexity of an algorithm, we take the average of the best and worst case scenarios.

{{% fragment %}}<u>Example - Linear Search</u><br/>Best case (first item was the match) - 1 access - O(1)<br/>Worst case (last item was the match) - n accesses - O(n){{% /fragment %}}

{{% fragment %}}The average is $\frac{n+1}{2}$ accesses.<br/>We then look at only the largest contributing terms, and discard the rest - giving us O(n){{% /fragment %}}

<!-- ```c
int numbers[5] = {3, 1, 2, 4, 5};

int linear_search(int* array, int n_items, int value) {
    for (int i = 0; i < n_items; i++) {
        if (numbers[i] == value) return i;
    }
    return -1;
}

linear_search(numbers, 5, 3);
``` -->

{{% /section %}}

---


{{< slide class="center" >}}

## Space Complexity

---

## Space Complexity

Space complexity is a measure of how much space a data structure, or an algorithm requires.  
Generally, time complexity contributes more towards a program's efficiency than its space complexity.  

For most data structures, `n` items will naturally have a space complexity of O(n).  

---

### More

You can find a list of the complexities of many data structures and algorithms here

> [www.bigocheatsheet.com](https://www.bigocheatsheet.com)