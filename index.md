CSE 15L Lab Report 5

```
# Create your grading script here
EXAMPLE_FILE_NAME="ListExamples.java"
CLASS_NAME="class ListExamples"

echo "Code Grader"
echo "Target URL: $1"
echo ""

rm -rf student-submission
git clone $1 student-submission -q

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Cloned successfully."
else
  echo "[FAILED] Clone failed. Check the submit URL."
  exit 1
fi

cd student-submission

if [[ -f $EXAMPLE_FILE_NAME ]]
then
  echo "[PASSED] File Found ($EXAMPLE_FILE_NAME)"
else
  echo "[FAILED] File Not Found ($EXAMPLE_FILE_NAME)"
  exit 1
fi

grep -q "$CLASS_NAME" ./$EXAMPLE_FILE_NAME

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Text Found ($CLASS_NAME)"
else
  echo "[FAILED] Text Not Found ($CLASS_NAME)"
  exit 1
fi

CP=".:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"

cp ../TestListExamples.java .
javac -cp $CP *.java 2> compile_error.txt

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Compiled successfully."
else
  MSG=`cat compile_error.txt | head -1`
  echo "[FAILED] Compile Failed. ($MSG)"
  exit 1
fi

rm -rf test_result.txt
java -cp $CP org.junit.runner.JUnitCore TestListExamples > test_result.txt

JUNIT_EXIT_CODE=$?


if [[ $JUNIT_EXIT_CODE -eq 0 ]]
then
  RESULT=`cat test_result.txt | grep "OK"`
  echo "[PASSED] jUnit result: " $RESULT
else
  RESULT=`cat test_result.txt | grep "Tests run:"`
  echo "[FAILED] jUnit result: " $RESULT
  exit 1
fi
```

Submission 1
https://github.com/ucsd-cse15l-f22/list-methods-lab3
(Same code as starter from lab 3)

Submission 2
https://github.com/ucsd-cse15l-f22/list-methods-corrected
(Has methods corrected (Full or near-to-full credit)

Submission 3
https://github.com/ucsd-cse15l-f22/list-methods-filename
(Has great implementation saved in file with the wrong name)

First, make sure your grading script from Lab 7 can successfully give feedback on all of the sample student submissions. You might make some judgment calls about which ones get “credit” or not! But there should be something meaningfully reported for all of them. You should confirm that this works through the browser interface as well as the command line.

To demonstrate this, include in your lab report:

Your grade.sh in a code block
Screenshots of three different student submissions and their reported grade as loaded in the browser (URL like https://localhost:4000/grade?repo=https://github.com...)
Then, choose one of the examples you showed in screenshot, and describe a trace of what your grade.sh does on that example.

To trace the script, describe:

For each line with a command, what its standard output and standard error are for this run, and whether its return code was zero or nonzero
For each line with an if statement, whether the condition was true or false, and why
Indicate each line that does not run (maybe because it is in an if branch that doesn’t evaluate, or after an early exit)
Submit your report to the Lab Report 5 (week 9) on Gradescope, due Monday, November 28 at 12pm (noon).
