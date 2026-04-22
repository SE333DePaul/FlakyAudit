## Background

Order-dependent (OD) tests are tests that pass or fail depending on the order in which they are executed. They often arise when tests share state (e.g., static variables, cached data, global configuration). Other issues:

- They can **mask real bugs** (a test passes only if another test runs first).
- They create **flakiness**.
- They slow down debugging because failures are **hard to reproduce** and we do not know if this is because of bug in source code or test code.

## Setup

1. Clone the archived project:
    
    ```bash
    git clone https://github.com/SE333DePaul/fastjson.git
    cd fastjson
    git checkout a7f1f5c4ac52503cc95bf1d27498098b3093a0df
    ```
    
2. Run the default test suite:
    
    ```bash
    mvn test
    ```
    
    - **Q1: Do any tests fail?**

## Step 1: Reverse Execution Order

1. Run the suite in **reverse order**:
    
    ```bash
    mvn test -Dsurefire.runOrder=reversealphabetical
    ```
    
2. Observe failures.
    - **Q2: Which test(s) fail, and what is the failure message?**

## Step 2: Random Execution Order

1. Run the suite with **random order**:
    
    ```bash
    mvn test -Dsurefire.runOrder=random
    ```
    
2. Repeat 2–3 times to see variability.
    - **Q3:  What does this command do? Which tests fail under randomization? List them and their error messages.**

## Step 3: Run in Parallel

Enable parallel execution:

```bash
mvn test -Dsurefire.parallel=all -Dsurefire.threadCount=4
```

- **Q4: What does this command do? Do any tests fail under parallel execution? Which ones?**

## Step 4: Isolate Each Test

Write a small **Bash Script** to run each test class in isolation:

- **Q5: Which test(s) fail when run in complete isolation? Why is this significant?**

## Discussion

1. Why do some tests pass when run as part of the full suite, but fail when isolated or reordered?
2. How might order-dependent tests impact:
    - Developer productivity?
    - Software reliability?
3. **Bonus**: How would you fix this bug?

## Deliverables

- A short report (`report.md`) containing:
    - **Q1–Q5 answers** with copy-pasted failure logs.
    - Reflection answers.
- Your **Bash script** used in Step 4
- Discussion about how you fixed the bug (bonus)
