# Example exam

The following questions are designed to determine your mastery of implementing the Fibonacci sequence using JavaScript.

```masteryls
{"id":"28241de3-d9e7-487c-bb59-48ca2b448d5a", "title":"Recursive Fibonacci - Base Cases", "type":"multiple-choice", "body":"Consider the following recursive JavaScript function for calculating the Fibonacci sequence:\n\n```javascript\nfunction fibonacciRecursive(n) {\n  // Base cases missing\n  return fibonacciRecursive(n - 1) + fibonacciRecursive(n - 2);\n}\n```\n\nWhat base cases are necessary to ensure the function terminates correctly and returns the proper Fibonacci numbers for `n = 0` and `n = 1`?" }
- [ ] `if (n === 0) return 1; if (n === 1) return 1;`
- [x] `if (n === 0) return 0; if (n === 1) return 1;`
- [ ] `if (n <= 0) return 0; if (n === 1) return 1;`
- [ ] `if (n === 0) return 0; if (n <= 1) return 1;`
```

```masteryls
{"id":"4266ab38-e2da-4650-8ec9-32cbd42b59cd", "title":"Iterative Fibonacci - Loop Condition", "type":"multiple-choice", "body":"You are implementing an iterative Fibonacci function in JavaScript.  You have initialized an array `fib` with the first two Fibonacci numbers: `fib = [0, 1];`.  What is the correct loop condition to calculate the Fibonacci sequence up to the `n`th number?" }
- [ ] `for (let i = 0; i <= n; i++)`
- [x] `for (let i = 2; i <= n; i++)`
- [ ] `for (let i = 2; i < n; i++)`
- [ ] `for (let i = 1; i <= n; i++)`
```

```masteryls
{"id":"982875c9-0dac-4e80-b201-a839a9a9563c", "title":"Memoization - Purpose", "type":"multiple-choice", "body":"What is the primary purpose of using memoization when implementing the Fibonacci sequence?" }
- [ ] To reduce memory usage by storing only the last two calculated Fibonacci numbers.
- [x] To improve performance by storing previously calculated Fibonacci numbers and reusing them, avoiding redundant calculations.
- [ ] To make the code more readable and easier to understand.
- [ ] To prevent stack overflow errors in iterative implementations.
```

```masteryls
{"id":"baa7aa1f-e9f7-49aa-9e02-995bb09e9f2e", "title":"Time Complexity - Recursive vs. Iterative", "type":"multiple-choice", "body":"What is the typical time complexity of a naive recursive Fibonacci implementation compared to an iterative implementation?" }
- [ ] Recursive: O(n), Iterative: O(n)
- [ ] Recursive: O(log n), Iterative: O(n)
- [ ] Recursive: O(n), Iterative: O(log n)
- [x] Recursive: O(2^n), Iterative: O(n)
```

```masteryls
{"id":"97817e15-4912-44e1-bd5a-179e66cd8b88", "title":"Space Complexity - Memoization", "type":"multiple-choice", "body":"How does memoization affect the space complexity of a recursive Fibonacci implementation?" }
- [ ] It reduces the space complexity to O(1).
- [x] It increases the space complexity to O(n) due to storing calculated values.
- [ ] It has no impact on the space complexity.
- [ ] It reduces the space complexity to O(log n).
```

```masteryls
{"id":"1666c355-477e-4841-b9c7-02b32a859b8a", "title":"Recursive Fibonacci - Optimization", "type":"essay", "body":"Explain why the naive recursive implementation of the Fibonacci sequence is inefficient.  Describe how memoization can be used to optimize the recursive implementation and explain why memoization improves performance." }
```

```masteryls
{"id":"3c316e13-1b35-42cf-a456-d46c9c78d5f0", "title":"Iterative Fibonacci - Code Implementation", "type":"essay", "body":"Write a JavaScript function called `fibonacciIterative(n)` that calculates the nth Fibonacci number using an iterative approach. Provide comments to explain your code." }
```

```masteryls
{"id":"6d09e4f4-b058-4717-8f93-7a98b788f8c9", "title":"Tail Recursion", "type":"essay", "body":"Explain the concept of tail recursion.  Can JavaScript implementations of the Fibonacci sequence be easily optimized using tail call optimization? Why or why not?" }
```

```masteryls
{"id":"4b00b6dc-5d2b-40b2-a405-e9f3bba3bc7c", "title":"Fibonacci Sequence - Definition", "type":"multiple-choice", "body":"Which of the following accurately describes the Fibonacci sequence?" }
- [ ] A sequence where each number is the sum of the previous three numbers.
- [x] A sequence where each number is the sum of the two preceding numbers, starting with 0 and 1.
- [ ] A sequence where each number is double the previous number.
- [ ] A sequence where each number is the square of the previous number.
```

```masteryls
{"id":"7e05258a-e4cb-413d-928e-faf406e6160f", "title":"Error Handling", "type":"essay", "body":"Discuss how you would implement error handling in a Fibonacci function (either recursive or iterative) to handle invalid input (e.g., negative numbers, non-integer values).  Provide example code snippets demonstrating your approach." }
```