**CSE 15L Lab Report 5**

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
<img width="706" alt="Screen Shot 2022-11-28 at 8 40 58 AM" src="https://user-images.githubusercontent.com/114449002/204332770-156f72c7-ddb4-486f-82c4-02721388c28c.png">
Grade 4/5


Submission 2
https://github.com/ucsd-cse15l-f22/list-methods-corrected
(Has methods corrected (Full or near-to-full credit)
<img width="754" alt="Screen Shot 2022-11-28 at 8 41 01 AM" src="https://user-images.githubusercontent.com/114449002/204332787-c6a86004-482e-41ff-9b8e-bce880bceffc.png">
Grade 5/5


Submission 3
https://github.com/ucsd-cse15l-f22/list-methods-filename
(Has great implementation saved in file with the wrong name)
<img width="749" alt="Screen Shot 2022-11-28 at 8 41 06 AM" src="https://user-images.githubusercontent.com/114449002/204332798-7b18f73c-2125-4cc0-a331-eb03d3b8e0de.png">
Grade 1/5

When Submission 3, `https://github.com/ucsd-cse15l-f22/list-methods-corrected` was called the following echo command lines are each ran once, displaying the link of the repository that is currently being tested. 

```
echo "Code Grader"
echo "Target URL: $1"
echo ""       
```

Then, the following is ran with both returning 0. 
```
rm -rf student-submission
git clone $1 student-submission -q
```

Since the returning were 0, the if statement `[[ $? -eq 0 ]]` is true and the "[PASSED] Cloned successfully." is echoed. The else statement would not run. 
```
if [[ $? -eq 0 ]]
then
  echo "[PASSED] Cloned successfully."
else
  echo "[FAILED] Clone failed. Check the submit URL."
  exit 1
fi
```

Change directory to student-submission to search for the file.
```
cd student-submission
```

The if statement `if [[ -f $EXAMPLE_FILE_NAME ]]` is ran to check for existence of ListExamples.java file in the current directory. When the file is found, it should echo "[PASSED] File Found ($EXAMPLE_FILE_NAME)". 
However, since the implementation for submission 3 was saved under the a wrong file name, the command is unable to find a file named ListExamples.java in the current directory and echos "[FAILED] File Not Found ($EXAMPLE_FILE_NAME)" and `exit 1` is ran, exiting the command lines early. 

```
if [[ -f $EXAMPLE_FILE_NAME ]] 
then
  echo "[PASSED] File Found ($EXAMPLE_FILE_NAME)" 
else
  echo "[FAILED] File Not Found ($EXAMPLE_FILE_NAME)"
  exit 1
fi
```
