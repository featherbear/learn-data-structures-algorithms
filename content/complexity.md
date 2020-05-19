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

{{% fragment %}}Complexity is a measure of how well a program performs.{{% /fragment %}}

{{% fragment %}}The main measures of complexity, is **time complexity** and **space complexity**{{% /fragment %}}

---

We express complexity in Big-O notation.

Constant (BEST) - $O(1)$  
Logarithmic - $O(log\ n)$  
Linear - $O(n)$  
n-log-n - $O(n\ log\ n)$  
Quadratic - $O(n^2)$  
Cubic - $O(n^3)$  
Exponential - $O(2^n)$  
Factorial - $O(n!)$  
Tetratial (WORST) - $O(n^n)$

<!-- Where `n` represents the number of items in a data set -->

{{% /section %}}

---

{{< slide class="center" >}}

## Time Complexity

---

## Time Complexity

{{% section %}}

Time complexity is the measure of how long an algorithm will take to complete. Often we assess time complexity on searching and sorting algorithms.  

{{%fragment%}}With small data sets, any searching/sorting algorithm will be virtually instant, but with large data sets it can take a long time.{{%/fragment%}}

{{%fragment%}}_There is no 'best' searching/sorting algorithm, as it will depend on the nature of the data._{{%/fragment%}}

---

To calculate the time complexity of an algorithm, we find the number of operations performed in its worst case scenario.

{{% fragment %}}<u>Example - Linear Search</u><br/>Best case (first item matched) - 1 access - $O(1)$<br/>Worst case (last item matched) - n accesses - $O(n)${{% /fragment %}}

{{% fragment %}}The worst case is $O(n)$ accesses.<br/>We look at the highest power of `n`, without any coefficients. In our case, it is just $O(n)${{% /fragment %}}

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

For most data structures, `n` items will naturally have a space complexity of $O(n)$.  

---

### More

You can find a list of the complexities of many data structures and algorithms here

> [www.bigocheatsheet.com](https://www.bigocheatsheet.com)