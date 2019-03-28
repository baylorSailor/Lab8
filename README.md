Tasks to answer in your own README.md that you submit on Canvas:

1.  See logger.log, why is it different from the log to console?
- The logger.log only captures those errors that are specifically added to the log file whereas the log to console would 
capture everything.
1.  Where does this line come from? FINER org.junit.jupiter.engine.execution.ConditionEvaluator logResult Evaluation of 
condition [org.junit.jupiter.engine.extension.DisabledCondition] resulted in: ConditionEvaluationResult [enabled = true,
 reason = '@Disabled is not present']
- From the TimerException() { super(); } defined in TimerException.java. Logged as a result of the void failOverTest() JUnit test.
1.  What does Assertions.assertThrows do?
- Asserts that execution of the supplied executable throws
  	 an exception of the expectedType and returns the exception. If no exception is thrown, or if an exception of a 
  	 different type is thrown, this method will fail. In the case of the call in Tester.java, TimerException is expected.
1.  See TimerException and there are 3 questions
    1.  What is serialVersionUID and why do we need it? (please read on Internet)
    - The serialization runtime associates with each serializable class a version number, called a serialVersionUID, which 
    is used during deserialization to verify that the sender and receiver of a serialized object have loaded classes for that object that are compatible with respect to serialization.
    2.  Why do we need to override constructors?
    - We want the ability to customize the messages and behavior of the TimerException class to match out logger.
    3.  Why we did not override other Exception methods?	
    - We only override the checked exceptions necessary for the program.
1.  The Timer.java has a static block static {}, what does it do? (determine when called by debugger)
- The static block is code that is executed when the class is initialized in the application. In this case, the static member variable logger is 
is initialized with the properties declared in the logger.properties file.
1.  What is README.md file format how is it related to bitbucket? (https://confluence.atlassian.com/bitbucketserver/markdown-syntax-guide-776639995.html)
- It is a markdown language file that is used to be a brief description or "how to" guide for using the software.
1.  Why is the test failing? what do we need to change in Timer? (fix that all tests pass and describe the issue)
- The test is failing because it expects a TimerException returned from timeMe() but receives a NullPointerException instead. This 
is because the value of timeNow is never initialized if it enters if() statement that checks that the time is non-negative. To 
fix this we could simply move the initialization from outside of the try block to its initial declaration, or we could check for 
a null value in the finally block, or move the initialization of timeNow within the try block before the if statement that checks
if the value passed into the function is < 0.
1.  What is the actual issue here, what is the sequence of Exceptions and handlers (debug)
- TimerException is thrown first since the value passed into it is < 0 which triggers the if statement within the first try block.
After that exception is caught, the code skips down to the finally block which returns the log message and the value for timeNow. timeNow's 
returned value is null because it was never initialized because it's initialization exists outside of the initial try block, and because it
catches the TimerException without checking for null, the value returned to failOverTest is a NullPointerException and not a TimerException
as expected. 
1.  Make a printScreen of your eclipse JUnit5 plugin run (JUnit window at the bottom panel) 
1.  Make a printScreen of your eclipse Maven test run, with console
1.  What category of Exceptions is TimerException and what is NullPointerException
- NullPointerException is a Runtime Exception and (unchecked expection) and TimerExecution is a checked exception.
1.  Push the updated/fixed source code to your own repository.