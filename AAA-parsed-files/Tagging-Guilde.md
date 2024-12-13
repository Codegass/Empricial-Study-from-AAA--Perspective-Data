# AAA Tagging Process Guidance

##  Tagging Process

###  Generate Tag-sheets
- Parser analyzes each test case based on Abstract Syntax Tree (AST)
- Expands each method invocation in the test case until it cannot be further expanded
- Production or external library methods are not expanded and should be tagged "atomically" as one of the "A"s (usually Arrange or Act)

### Manual Tagging
1. Review test case and class names
   - Good names help quickly grasp test intention
   - Typical test case name format: "test" + function under test + test scenario
   - Typical test class name format: "AlphaTest", where "Alpha" summarizes tested functions
   - Example: "testInvoker_normal" and "testInvoker_fail" under "ClusterInvokerTest" class

2. Analyze internal logic of the test case
   - Review code within the test case
   - Review expanded code from methods invoked by the test case
   - If necessary, review production functions called in the test case, especially for poorly named tests
   - Example: "testReleaseDedicatedGuestVlanRange" test case from CloudStack contains only three lines but calls a method with 9 expanded statements

3. Tag each statement
   - Use the generated tag-sheet
   - Annotate each statement as Arrange, Act, or Assert
   - Consider the overall structure and purpose of the test case

## Special Cases

### Assertion Helper Statements
- Functions that assist in data retrieval for assertion verification should also be tagged as Assertion. 

### Expected Exception Statements
- If a test case's fixture is in the form "@Test(expected = Exception.class)", consider it an expected exception test, and the Expected Exception statement should be tagged as Assert.

### Integration Test Cases
- If a test case name ends with "IT", consider it an integration test and exclude from the dataset

### Poorly Named Test Cases
- For test cases with uninformative names (e.g., "testX" where X is a number or letter), carefully review production code to determine the Act part