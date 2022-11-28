CSE 15L Lab Report 5

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
