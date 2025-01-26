# Implement a Simple Static Taint Analysis for Python Code

Your goal in this challenge is to build a tool that performs basic static taint analysis for a Python program. The tool should track user inputs (tainted data) as they propagate through assignments and function calls, and identify potential security risks when tainted data reaches sensitive functions.

## What is Static Taint Analysis?

Static taint analysis is a method used to find security vulnerabilities in software by tracking how data flows through the code without actually running it. It helps identify unsafe data sources (user inputs) and determines whether they reach security-sensitive functions ("sinks") such as `exec()`.

### Example Scenario

Consider the following Python code:

```python
import os

user_input = input("Enter command: ")  # tainted source
cmd = "ls " + user_input  # propagated from user_input to cmd
ret = foo(cmd) # propagated from cmd to ret
exec(ret)  # reached to sink

def foo(x):
    return x
```

### Step-by-Step Walkthrough

1. **Identifying tainted sources:**

   - The `input("Enter command: ")` function call on line 3 introduces tainted data.
   - The variable `user_input` now contains potentially unsafe data.

2. **Tracking propagation:**

   - On line 4, `user_input` is used to create a new variable `cmd`. Since `cmd` is constructed using `user_input`, it is also tainted.
   - On line 5, the function `foo(cmd)` is called. Since `cmd` is tainted, `foo`'s return value is also tainted.

3. **Sensitive sink detection:**

   - The `exec(ret)` function call on line 6 is a sensitive sink. Since `ret` contains tainted data, this represents a potential vulnerability.

## Task Requirements

To complete this challenge, you need to analyze the following elements:

- **Tainted Sources:** Data inputs that come from `input()` in this case.
- **Propagation:** How tainted data spreads through assignments and function calls.
- **Sensitive Sinks:** Functions that can execute tainted data, with `exec()` being the focus in this challenge.
The output should clearly specify the line numbers of each detected element.


Your program should:
1. Identify the line numbers where tainted sources (i.e., `input()`) appear.
2. Track and list the variables that get tainted.
3. Identify the locations of sink functions like `exec()`.
4. Determine whether tainted data reaches each sink and report potential vulnerabilities.

You can use your favoriate programming langauge as you want.
Please update a single program to [this Google Form](https://forms.gle/PrSDDMJPNTAgn1Ei6).

## Hints

- Parsing the code: Use Python's ast module to parse and analyze the code structure if you are using Python.
- Tracking taint: Maintain a dictionary to track variables and their taint status.
- Propagation: Follow assignments and ensure that tainted data is properly traced across variables.
- Function calls: Consider function arguments and return values as potential propagation paths.
- Identifying sinks: Search for function calls such as exec() and verify if their arguments are tainted.

You might consider other language features such as branches/conditional statements, loops, etc.

Feel free to contact Penghui Li (pl2689@columbia.edu) if you need further clarifications. You can also write down your own assumptions in comments. Good luck, and have fun with the challenge! 

