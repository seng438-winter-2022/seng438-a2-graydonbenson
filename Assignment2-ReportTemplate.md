**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#2 – Requirements-Based Test Generation**

| Group \#:       | 7 |
|-----------------|---|
| Student Names:  | Graydon Benson  |
|                 | Eli St. James   |
|                 | Seher Dawar     |
|                 | Maxwell Botham  |


# 1 Introduction

//To write

# 2 Detailed description of unit test strategy


Here are the five methods we chose to test for the class Range:
getCentralValue()
getLength() 
getUpperBound() 
getLowerBound() 
contains(double value) 

BlackBox

Equivalence Classes

Equivalence class testing involves dividing possible method inputs into partitions or “buckets” that would be considered similar to one another. In each test case, we will define a unique equivalence class that groups common inputs together. All of the methods we are testing take in integers or doubles as input, therefore we can group common integers within the same set together to avoid redundancy. For instance in getUpperBound(), a Range(0,1) object will have the same output as a Range(-1,1) object..   

The domain of getUpperBound() is all valid Range objects. Initially we will partition our possible inputs into Expected or Legal Inputs (E) and Unexpected or Illegal inputs (U). E will consist of the following sub-partitions - Negative Integer Ranges, Ranges including Zero, Positive Integer Ranges, Negative Double Ranges, and Positive Double Ranges. 
On the other hand, U will consist of the following sub-partitions - String Valued Ranges, Char Valued Ranges, and Float Valued Ranges.  

The domain of createNumberArray is all arrays made up of doubles.  We can partition our possible inputs into Expected or Legal Inputs (E) and Unexpected or Illegal inputs (U). E will consist of the following sub-partitions - Negative Integer Arrays, Arrays including Zero, Positive Integer Arrays, Negative Double Arrays, and Positive Double Arrays. 
On the other hand, U will consist of the following sub-partitions - String Valued Arrays, Char Valued Arrays, and Float Valued Arrays. 

Boundary Value Analysis

Boundary value testing was created because of the fact that programs often fail when arguments are provided that are at or near the boundaries of valid input, and are expected to fail when outside the boundaries. Some bugs can only be detected when programs are tested with values that are exactly on a boundary. For example, if a function expects input that is greater than 10 but less than 20, but the program actually accepts values greater than or equal to 10 but less than 20, a test that provides the value 9 will still pass. The only way to detect the fault is by providing an input of value 10. However, boundary value analysis does not only consider inputs that are equal to defined boundaries, but also those that are out of bounds (above maximum boundary, or below minimum boundary). A typical boundary value testing strategy involves 7 tests: one slightly above the upper bound, one at the upper bound, one slightly below the upper bound, one inside bounds, one slightly above the lower bound, one at the lower bound, and one slightly below the lower bound.

In the Range class, the contains(double value) method is the most suitable method to apply boundary value testing to. To begin testing it, we must first create a Range object. In one test case, we could create a range from values -5 to 5. Considering the contains(double value) function, the expected outputs are as follows: FALSE for double inputs < -5; TRUE for double inputs -5 to 5; FALSE for double inputs > 5. Applying the earlier strategy, we should test the contains(double value) method with the following values: -6 (slightly below minimum bound, expected output: FALSE). -5 (at minimum bound, expected output: TRUE). -4 (slightly above minimum bound, expected output: TRUE). 0 (a value solidly inside the range, expected output: TRUE). 4 (a value slightly below maximum bound, expected output: TRUE). 5 (a value at the maximum bound, expected output: TRUE). 6 (a value slightly above maximum bound, expected output: FALSE).

Another example would be for the calculateRowTotal method. This method takes in a Values2D object which is essentially a table of data, and an integer value representing the row at which all the values inside that row will be added together.  The way we plan to test this method is by mocking a Values2D object with a set amount of rows, then passing in, for the int row argument, a variety of values. To begin, we will pass in a value that is greater than the amount of rows. For example, if we mock a Values2D object with 9 rows (rows [0, 8]) and x columns, we would pass in 9 for the int row argument, which would be invalid given that the last row has an index of 8. We would also test at the boundaries of the number of rows in the Values2D object. For the example above (Values2D with 9 rows), we could pass in 8 (maximum boundary of rows) which should be valid, given index 8 is the last row. We can also pass in 0, given that the first row index is 0. We will also test this method by passing in a negative value for the ‘int row’ argument. Lastly, we will pass in a row index in the expected boundaries, such as 4.

calculateColumnTotal, calculateRowTotal, getCumulativePercentages all require mocking, as Values2D and KeyedValues are Interfaces and cannot be instantiated as objects. Once we have created a mock object, we can apply the same type of boundary or equivalence class testing on the objects to confirm expected output. The benefits of using mocking is we can replicate realistic data, and how our application will respond to a variety of scenarios, and how these results are achieved. The downsides of this process are the teardown and cleanup process. There is a small level of additional setup, and as well refactoring code with Mocking is slightly more difficult. 

# 3 Test cases developed

getCentralValue()
Test central values of positive, and negative integers, and positive and negative doubles. Also test 0 as central value, and invalid range exceptions. A range with size 1 (-1,-1) for example can also be tested. 

getLength() 
Range from a to a
Range is null
Range -ve to +ve
Range is large
Range is large and in doubles
Range is defined incorrectly larger to smaller


getUpperBound() 
Test upper-bounds with ranges of values of positive, and negative integers, and positive and negative doubles. Also test when the upper bound is 0, positive or negative, and when it is an integer or a double. Test with range size 1, (upper and lower bounds are the same). Upper and lower bounds same == range size 0

getLowerBound() 
Test lower-bounds with ranges of values of positive, and negative integers, and positive and negative doubles. Also test when the lower bound is 0, positive or negative, and when it is an integer or a double. Test with range size 1, (upper and lower bounds are the same). 


contains(double value)
Apply boundary limit testing on upper and lower boundaries of ranges to ensure values are correctly indicated as present or not present. Test on and above/below these boundary levels. Test ranges with integers and doubles, both positive and negative. 


calculateColumnTotal(Values2D data, int column) 
Test with null input for Values2D data
Test with null input for int column
Test with column at minimum boundary (0)
Test with column at maximum boundary (index 4, in 5 column Values2D)
Test with column just below maximum boundary (index 3, in 5 column Values2D)
Test with column just above minimum boundary (index 1)
Test with column just below minimum boundary (out of bounds, index -1)
Test with column just above maximum boundary (out of bounds, index 5 in 5 column Values2D)
Test with a large number of rows
Test summing negative integers in a large number of rows

calculateRowTotal(Values2D data, int row)
Test with null input for Values2D data
Test with null input for int row
Test with row at minimum boundary (0)
Test with row at maximum boundary (index 4, in 5 row Values2D)
Test with row just below maximum boundary (index 3, in 5 row Values2D)
Test with row just above minimum boundary (index 1)
Test with row just below minimum boundary (out of bounds, index -1)
Test with row just above maximum boundary (out of bounds, index 5 in 5 row Values2D)
Test with a large number of columns
Test summing negative integers in a large number of columns

createNumberArray(double[] data) 
Test with regular double[] input
Test with empty double[] input
Test with null input

createNumberArray2D(double[][] data)
Test with regular double[][] input
Test with empty double[][] input
Test with null input
Test with populated double[][] with an empty double[] input
Test with populated double [][] with a null double[] input

getCumulativePercentages(KeyedValues data) 
Test with null input for the KeyedValues keys
Test with null input for KeyedValues object
Test with 3 values 
The keyedvalue object has 3 values
The values are 0
The values are a mix of positive and negatives
The keyedvalue object has 7 values

# 4 How the team work/effort was divided and managed

To complete this lab, we began by each setting up our Eclipse IDE individually. This included importing all of the JAR files provided for the lab, running an example of the range class, and running an example unit test. Next, we met up as a group, and developed our test plan. We chose which five functions from Range.class we would test, and split up the 10 methods to test evenly between all team members. We split off again, and each wrote our test cases individually. After every member had completed writing tests, we met up and reviewed each other’s work, ensuring each team member fully understood the process of mocking with JMock. Lastly, we all worked together to write and complete the lab report. Since this was our second lab as a team, we have learned each other’s strengths better, and were able to split up the work based on this. 

# 5 Difficulties encountered, challenges overcome, and lessons learned

The usage of JMock and the discrepancies in the versions of JFree uploaded to Github were a few difficulties we faced while writing this report and these test suites. For JMock, we were stumped by the mocking cases that called the same function multiple times since “one-will” expectation does not cater to this case. We had to read the JavaDocs to learn about the “atleast-pair” expectation pair. 

# 6 Comments/feedback on the lab itself

The assignment was interesting, interactive, and at times challenging. It really gave us a taste of what it is like to test a program, and develop thoughtful test cases. It was a great learning opportunity to apply what we learned in class about equivalence and boundary testing. One thing we noticed was that two different packages were distributed with different Jar’s. This made it confusing as some tests passed, and others failed, using the same test cases.  It took us a while to figure out that this was the case, as we had to compare different versions of the repository that existed. Overall, it was a good assignment.
