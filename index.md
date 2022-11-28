**CSE 15L Lab Report 5**


```
# Create your grading script here
FILE_NAME="ListExamples.java"
CLASS_NAME="class ListExamples"
SCORE=0

echo "Code Grader"
echo "Target URL: $1"
echo ""

rm -rf student-submission
git clone $1 student-submission

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Cloned successfully."
  ((score++))
else
  echo "[FAILED] Cloning failed. Check the submit URL."
  echo "Final Grade: [$score/5]"
  exit 1
fi

cd student-submission

if [[ -f $FILE_NAME ]]
then
  echo "[PASSED] File Found [$FILE_NAME]"
  ((score++))
else
  echo "[FAILED] File Not Found [$FILE_NAME]"
  echo "Final Grade: [$score/5]"
  exit 1
fi

grep -q "$CLASS_NAME" ./$FILE_NAME

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Text Found [$CLASS_NAME]"
  ((score++))
else
  echo "[FAILED] Text Not Found [$CLASS_NAME]"
  echo "Final Grade: [$score/5]"
  exit 1
fi

CPATH=".:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"

cp ../TestListExamples.java .
javac -cp $CPATH *.java 2> compile_error.txt

if [[ $? -eq 0 ]]
then
  echo "[PASSED] Compiled Successfully."
  ((score++))
else
  MSG=`cat compile_error.txt | head -1`
  echo "[FAILED] Compilation Failed. ($MSG)"
  echo "Final Grade: [$score/5]"
  exit 1
fi

rm -rf test_result.txt
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > test_result.txt

JUNIT_EXIT_CODE=$?


if [[ $JUNIT_EXIT_CODE -eq 0 ]]
then
  RESULT=`cat test_result.txt | grep "OK"`
  echo "[PASSED] jUnit result: " $RESULT
  ((score++))
else
  RESULT=`cat test_result.txt | grep "Tests run:"`
  echo "[FAILED] jUnit result: " $RESULT
  echo "Final Grade: [$score/5]"
  exit 1
fi
```

Submission 1
https://github.com/ucsd-cse15l-f22/list-methods-lab3
(Same code as starter from lab 3)
<img width="682" alt="Screen Shot 2022-11-28 at 11 34 23 AM" src="https://user-images.githubusercontent.com/114449002/204365074-200e596d-61b8-4d0d-a8cc-cb40b3565d9f.png">


Submission 2
https://github.com/ucsd-cse15l-f22/list-methods-corrected
(Has methods corrected (Full or near-to-full credit)
<img width="683" alt="Screen Shot 2022-11-28 at 11 32 42 AM" src="https://user-images.githubusercontent.com/114449002/204364788-b912b39b-b932-474c-b99d-8abd505a03c9.png">


Submission 3
https://github.com/ucsd-cse15l-f22/list-methods-filename
(Has great implementation saved in file with the wrong name)
<img width="681" alt="Screen Shot 2022-11-28 at 11 33 37 AM" src="https://user-images.githubusercontent.com/114449002/204364931-f3c8099e-67de-4100-a9fe-d0e66b383396.png">


When Submission 3, `https://github.com/ucsd-cse15l-f22/list-methods-corrected` was called the following echo command lines are each ran once. First initializing the string variables and initializing score as zero. Then, displaying the link of the repository that is currently being tested. 

```
FILE_NAME="ListExamples.java"
CLASS_NAME="class ListExamples"
SCORE=0
echo "Code Grader"
echo "Target URL: $1"
echo ""       
```

Then, the following is ran with both returning 0. 
```
rm -rf student-submission
git clone $1 student-submission -q
```

Since the returning were 0, the if statement `[[ $? -eq 0 ]]` is true and the "[PASSED] Cloned successfully." is echoed and the score is incremented by one. Since the if statement is false, the else statement would not run. 
```
if [[ $? -eq 0 ]]
then
  echo "[PASSED] Cloned successfully."
  ((score++))
else
  echo "[FAILED] Cloning failed. Check the submit URL."
  echo "Final Grade: [$score/5]"
  exit 1
fi
```

Change directory to student-submission to search for the file.
```
cd student-submission
```

The if statement `if [[ -f $EXAMPLE_FILE_NAME ]]` is ran to check for existence of ListExamples.java file in the current directory. When the file is found, it should echo "[PASSED] File Found ($EXAMPLE_FILE_NAME)" and increment the score by one. 
However, since the implementation for submission 3 was saved under the a wrong file name, the command is unable to find a file named ListExamples.java in the current directory and echos "[FAILED] File Not Found ($EXAMPLE_FILE_NAME)" and echos "Final Grade: [$score/5]", when the score is 1. Then, finally, `exit 1` is ran, exiting the command lines early. 

```
if [[ -f $FILE_NAME ]]
then
  echo "[PASSED] File Found [$FILE_NAME]"
  ((score++))
  echo "Final Grade: [$score/5]"
else
  echo "[FAILED] File Not Found [$FILE_NAME]"
  echo "Final Grade: [$score/5]"
  exit 1
fi
```
