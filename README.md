# lab-2-MergeSort
MergeSort
General Learning Objectives

Use a modern operating system and utilities.

Use an integrated development environment to develop a program.

Solve problems and develop programs using the control structures of sequence, selection, and repetition, following a disciplined approach.

Goals
Practice coding on your own with TDD.
Practice using recursion in C#.
Deeply understand a very fast and intuitive sorting algorithm.
Overview

When things are in sorted order, it can be much faster to locate the position of an object. In this lab you are going to write a very fast sorting function that uses a recursive algorithm called MergeSort.

Before starting, take a look at this visualization of the algorithm and make sure to read through the rest of the instructions: https://www.hackerearth.com/practice/algorithms/sorting/merge-sort/visualize/

Steps
Environment Setup
Accept the GitHub Classroom Assignment.
Open a terminal.
If you don't have a code directory already:
Run e.g. mkdir my-code-dir to make a new directory named 'my-code-dir'.
Navigate to your code directory (hint: cd my-code-dir).
Run git clone {yourUrl} to make a local copy of your repository. (hint: don't include the curly braces in your command---those are just there to indicate that you should replace {yourUrl} with your actual repository url.)
Run code {nameOfYourRepo} to open that directory in VS Code.
Open the integrated terminal in VS Code (Ctrl+`, or the Terminal menu -> New Terminal).
Run dotnet new console to create a new project in the current folder.
Run dotnet run to compile and execute your code.
Part One: Non-Recursive Merging

I can easily combine two lists that are in increasing order by repeatedly looking at the next value of each list and moving whichever is smaller to be the next value in the combined list (if we get to the end of one of the lists, we automatically take the value from the other). The resulting combined list will have all the values in sorted order and the process of merging only needed to do as many comparisons and moves as there were total values.

In this step, use TDD to implement a function int[] CombineSortedArrays(int[] a, int[] b) that accepts two already sorted lists and then returns a sorted list that includes all of the values (including duplicates) from a and b but in sorted order. Do not use recursion on this function. After all of your tests pass, print "All tests passed." to the console. Make sure to commit after each new test passes.

Here are a couple of example test cases that you should pass:

System.Diagnostics.Debug.Assert(Enumerable.SequenceEqual(
    CombineSortedArrays(new int[]{1, 3, 5}, new int[]{-5, 3, 6, 7}),
    new int[]{-5, 1, 3, 3, 5, 6, 7});

System.Diagnostics.Debug.Assert(Enumerable.SequenceEqual(
    CombineSortedArrays(new int[]{-5, 2, 5, 8, 10}, new int[]{1, 2, 5}),
    new int[]{-5, 1, 2, 2, 5, 5, 8, 10});

PSEUDOCODE:
def CombineSortedArrays(a, b):
   combined = empty array of size a.Length + b.Length
   aIndex = 0
   bIndex = 0
   for combinedIndex from 0 to combined.Length:
       if bIndex is at the end of b yet or (aIndex is not at the end of a and a[aIndex] < b[bIndex]):
          copy from a[aIndex] to combined[combinedIndex]
          increment aIndex
       else
          copy from b[bIndex] to combined[combinedIndex]
          increment bIndex
   return combined

Part Two: Recursive Sorting

Based on the above merging idea, Mergesort is a very fast sorting algorithm that is easily remembered and understood by thinking recursively: if I want to sort a list of length $n$, I'm already done if $n < 2$. Otherwise, I can split my list in half and, recursively, sort each half and then merge them together into a combined sorted list using the process described above. That's all there is to Mergesort! And despite its simplicity, it is able to sort arbitrary lists of thirty billion items about a billion times faster than selection sort, bubble sort, or insertion sort can!

In this step, use recursion to implement the above algorithm and to use your CombineSortedArrays function from the previous problem. Make sure that you pass the following test cases:

System.Diagnostics.Debug.Assert(Enumerable.SequenceEqual(
    SortViaMergesort(new int[]{6, 1, -5, 3, 5, 3, 7}),
    new int[]{-5, 1, 3, 3, 5, 6, 7});

System.Diagnostics.Debug.Assert(Enumerable.SequenceEqual(
    SortViaMergesort(new int[]{1, 10, -5, 2, 5, 2, 5, 8}),
    new int[]{-5, 1, 2, 2, 5, 5, 8, 10});


Here is a pseudocode description of the algorithm:

PSEUDOCODE:
def SortViaMergesort(values):
   if values.Length < 2:
      return copy of values
   else:
      return CombineSortedArrays(SortViaMergeSort(first half of values), SortViaMergeSort(second half of values))


Hint: The following code splits an array int[] values in half:

int middle = values.Length / 2;
int[] firstHalf = values[0..middle];
int[] secondHalf = values[middle..values.Length]

Rubric
[
    {"label": "Comment at top of Program.cs giving your name(s), the date, and the name of the lab", "points": 5},
    {"label": "At least 4 commits each containing an additional test and corresponding code to make the test pass.", "points": 15},
    {"label": "CombineSortedArrays tested", "points": 15},
    {"label": "CombineSortedArrays correct", "points": 20},
    {"label": "SortViaMergesort tested", "points": 15},
    {"label": "SortViaMergesort correct", "points": 20},
    {"label": "Well-chosen identifiers", "points": 5},
    {"label": "Clean and consistent vertical whitespace.  Leave one line between functions, leave blank lines between logically grouped blocks of code, etc.", "points": 5}
]
