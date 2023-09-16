# A short introduction to testing: Building Reliable Software

This short chapter dives into a topic that's often overlooked but absolutely essential in the world of coding - testing. Testing is an essential part of programming and software engineering. It helps to ensure that the code is correct, reliable, and efficient. Testing also helps to find and fix errors, bugs, and vulnerabilities that may compromise the functionality, security, or performance of the software. Testing can be done at different levels of abstraction, from individual units of code to entire systems or applications. However, at our level, we will be focusing on testing individual units of code, and more specifically functions that we have implemented.

## The Essence of Software Testing

Software testing is the systematic process of evaluating a software application or system to identify defects, errors, or inconsistencies. It encompasses a wide range of activities aimed at assessing the software's behavior, performance, and compliance with specified requirements. Testing is not merely a phase; it's an ongoing discipline that runs parallel to development, guiding the software towards maturity and excellence.

## Test Driven Development

One of the aspects of testing that is relevant for software design and implementation is the concept of test-driven development (TDD). TDD is a methodology that involves writing tests before writing the actual code. The tests define the expected behaviour and output of the code, and serve as a guide for the development process. The code is then written to pass the tests, and refactored as needed to improve its quality and readability. TDD helps to ensure that the code meets the requirements and specifications, and that it is easy to maintain and modify.

### The Software Testing Lifecycle

Software testing is not a single, isolated task; it follows a structured lifecycle that aligns with the software development process. This lifecycle typically includes the following phases:

1. **Test Planning**: Defining the testing objectives, scope, resources, and schedule.
2. **Test Design**: Creating test cases, test scripts, and test data based on requirements and use cases.
3. **Test Execution**: Running the tests, capturing results, and identifying defects.
4. **Defect Reporting**: Documenting and reporting identified defects to the development team for resolution.
5. **Defect Retesting**: Verifying that reported defects have been fixed correctly.
6. **Regression Testing**: Ensuring that changes or enhancements do not introduce new defects.
7. **Test Closure**: Summarizing testing activities, evaluating the exit criteria, and generating test reports.

## The `assert` statement

A simple technique that a novice programmer can use for testing is the `assert` statement in Python. The `assert` statement checks if a given condition is true, and raises an `AssertionError` if it is false. The `assert` statement can be used to verify that the input, output, or intermediate values of a function or a program are correct, or that certain invariants or preconditions are satisfied. For example, the following code uses assert statements to test a function that calculates the factorial of a positive integer: In this example, the second line of code tests if the function’s precondition is true, that is the argument provided is positive.

{% code lineNumbers="true" %}
```python
def factorial(n):
    assert n >= 0, "n must be non-negative"
    if n == 0 or n == 1:
        return 1
    output = 1
    for i in range(2, n+1)
        output *= i
    return output

assert factorial(0) == 1, “factorial(0) must return 1”
assert factorial(1) == 1
assert factorial(2) == 2
assert factorial(3) == 6
assert factorial(4) == 24
assert factorial(5) == 120
```
{% endcode %}

The assert statements after the function definition check the post condition of the function, that is the returned value is the factorial of the argument.

The `assert` statements will raise an `AssertionError` if any of the conditions are false, indicating that there is an error in the code or the input. The assert statement can also take an optional second argument that provides a message to explain why the assertion failed.

## A more advanced tool called `unittest`

The `assert` statement is a useful tool for testing, but it has some limitations. It can only check for simple conditions, and it does not provide a comprehensive report of the test results. It also stops the execution of the program when an assertion fails, which may not be desirable in some cases.&#x20;

For more advanced testing, Python provides a module called `unittest` that supports automated testing with more features and flexibility. Unittest allows writing test cases as classes that inherit from `unittest.TestCase`, and using various methods to check for different types of assertions, such as `assertTrue`, `assertFalse`, `assertEqual`, `assertNotEqual`, `assertRaises`, etc. `unittest` also provides a test runner that can run all the test cases in a module or a package, and generate a detailed report of the test outcomes, such as passed, failed, skipped, or errored.

We will revisit this concept later, when we are familiar with implementing classes in Python.

## Conclusion

In conclusion, testing is not an afterthought but a crucial aspect of programming. It ensures your software's reliability, saves time, and enhances your code's quality. Testing can also improve the design and implementation of the software, by making it clearer, more concise, and consistent.

Testing is a vital skill for any programmer or software engineer., and as a novice programmer, start with the simple yet effective `assert` statement. As you progress, consider exploring the power of `unittest` for more comprehensive testing.

Remember, in the world of coding, testing isn't just about finding errors; it's about building robust, dependable software.&#x20;

\
