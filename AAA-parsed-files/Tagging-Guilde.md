# AAA Tagging Process Guidance

##  Tagging Process

###  Generate Tag-sheets
- Parser analyzes each test case based on Abstract Syntax Tree (AST)
- Expands each method invocation in the test case until it cannot be further expanded
- Note: Production or external library methods are not expanded and should be tagged "atomically" as one of the "A"s (usually Arrange or Act)

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
   - Example: "testReleaseDedicatedGuestVlanRange" from CloudStack contains only three lines but calls a method with 9 expanded statements

3. Tag each statement
   - Use the generated tag-sheet
   - Annotate each statement as Arrange, Act, or Assert
   - Consider the overall structure and purpose of the test case

### Encode Test Case Layout
- Encode tagging results as a sequence of Arrange, Act, and Assert in any order

## Special Cases

### Integration Tests
- If a test case name ends with "IT", consider it an integration test and exclude from the dataset

### Poorly Named Test Cases
- For test cases with uninformative names (e.g., "testX" where X is a number or letter), carefully review production code to determine the Act part
- Example: "test2" from Accumulo requires understanding of production code for proper tagging

## Cross-validation

- All taggers work independently
- For disagreements, conduct group discussions to reach consensus

## Result Compilation

### Organize Tagging Results
- Compile tagging results for each test case in tag-sheets within the "AAA parsed files/" directory

### AAA Pattern Identification
- Use regex matching to identify test cases following the AAA pattern

### Manual Inspection
- Manually inspect cases not matching the pattern to separate:
  a) Special AAA cases
  b) True AAA-Deviation cases

### AAA-Deviation Analysis
- Summarize recurring AAA-Deviation patterns
- Identify design issues within A blocks