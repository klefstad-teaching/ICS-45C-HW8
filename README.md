# ICS 45C Homework 8

3 Programs Using Standard Template Library

## Getting the assignment

1. Accept the assignment by clicking the link in Canvas
2. Once you accept the invite, you will reach a page that says "You're ready to go"
3. Click the URL from that page that looks similar to this: `https://github.com/klefstad-teaching/ics-45c-hw8-<YourGitHubUsername>`. It may take a bit of time for the repo to be ready.
4. Click the green `<> Code` Button on the top right, and then click the middle tab `SSH`
5. Copy that link
6. Go to your hub and go into the ICS45C folder, and open up the terminal and type in the following command:
```bash
git clone git@github.com:klefstad-teaching/ics-45c-hw8-<YourGitHubUserName>.git HW8
```
7. Go to VSCode and open up the `HW8` Folder

## Directory Structure

If you are not using `GitHub`, and want to use our testing framework, you will need to make a folder
named `hw8` with the following structure:

```bash
├── CMakeLists.txt
├── CMakePresets.json
├── gtest
│   ├── compute_grades_gtests.cpp
│   ├── gtestmain.cpp
│   ├── mapset_gtests.cpp
│   └── process_numbers_gtests.cpp
└── src
    ├── compute_grades.cpp
    ├── compute_grades.hpp
    ├── compute_grades_main.cpp
    ├── gradebook.txt
    ├── mapset.cpp
    ├── mapset.hpp
    ├── mapset_main.cpp
    ├── process_numbers.cpp
    ├── process_numbers.hpp
    ├── process_numbers_main.cpp
    ├── rand_numbers.txt
    ├── sample_doc.txt
    └── stopwords.txt
```

You should copy everything from the `CMakeLists.txt` and `CMakePresets.json` files into your own,
as well as the files `gtestmain.cpp` and the individual `gtests`.

## Overview and Objectives

Homework 8 consists of independent programs, including one that you have solved before (as `word_count` from Homework 2), but this time, using **Standard Template Library functions** instead of many of the low-level `for`, `while`, or `do-while` loops. You also gain more experience using lambdas.

The first program, `process_numbers`, reads integers from a file, sorts them, and prints odd and even subsets in two different formats.

The second program, like `word_count` from Homework 2, reads words from a file, ignoring case and the stopwords in a second file, and prints a sorted list of the words and their frequencies, in a specific format in an output file.

The third program, `compute_grades`, computes and prints course grades in a sorted, specific format, when given student data in a gradebook file, for a hypothetical course in which homework counts for 30% of the final grade, quizzes 40% with the lowest score dropped, and a final exam 30%.

### Relation to Course Objectives

The highest level of C++ programming uses the Standard Template Library, which is composed of containers and algorithms connected with iterators. We also use lambdas to customize and connect it all together into simple programs that we might otherwise write in scripting languages such as Python. Homework 8 restricts the use of C++ to only higher-level language components, to help us avoid errors and to leverage our productivity by reusing previously coded and tested software components.

These 3 programs provide practice in

 - Reading, parsing, and writing files with `ifstream`, `ofstream`, `istream_iterator<>()`, `ostream_iterator<>()`, `operator<<()`, `operator>>()`
 - Using STL containers: `string`, `stringstream`, `vector`, `set`, `map`
 - Using STL algorithms like `sort()`, `copy()`, `copy_if()`, `for_each()`, `min_element()`, `accumulate()`, `transform()`, `tolower()`, `find()`
 - Using functional objects like `back_inserter()`

The second program, `mapset.cpp`, **will also be re-used in Homework 9** to learn more about STL Iterators, where we will write both class Map and class Set (as well as their iterators) to replace the STL containers used in this Homework 8 program.

> To learn more about using the STL, read its documentation on [cppreference.com](https://en.cppreference.com/w/). Many other sites or tutorials are not up to date with the C++20 standard.

## Organization of Classes and Files

> *Be sure to use **exactly** the names given in these instructions and in this repo for **files**, **functions**, and **classes**, because the autograder will be expecting exactly those names.*

> 💡**Tip:** Remember that when functions read files, **the path must be supplied if the file is not in the same directory as the executable.**

## 1 process_numbers

Write a C++ program, named `process_numbers`, in the files `process_numbers.hpp`, `process_numbers.cpp`, and `process_numbers_main.cpp` that
- reads a sequence of integers from a file named `rand_numbers.txt`
- stores them in a `std::vector`,
- sorts them in ascending order (some numbers may appear more than once; keep the duplicates in the results),
- writes the odd ones to a file named `odds.txt`, following the format in the sample output below with a newline after the list of numbers, and
- writes the even ones to a file named `evens.txt`, following the format in the sample output below. (Yes, the evens and odds have different output formats.)

Do not use any low-level `for`, `while`, or `do-while` loops.

Consider these because they will be useful: `vector`, `istream_iterator<>()`, `sort` or `ranges::sort()`, `copy_if` or `ranges::copy_if()`, `ostream_iterator<>()`, and `lambda`

> **Read about the `ranges` library [here](https://en.cppreference.com/w/cpp/ranges).**

Sample input and output formats

If the `rand_numbers.txt` file contains the following integers:

```
3 7 2 8 9 1 4 6 5
```

Then, the file `odds.txt` should contain the following:

```
1 3 5 7 9 <newline>
```

And the file `evens.txt` should contain the following:

```
2
4
6
8
```

A sample input file `rand_numbers.txt` is provided for testing.

**Be sure to follow the [General Steps of Development](#general-steps-of-development) below. Some relevant details may be provided only in the Steps.**

process_numbers.hpp screenshot

![process_numbers.hpp screenshot](/assets/1-1.png)

process_numbers_main.cpp screenshot

![process_numbers_main.cpp screenshot](/assets/1-2.png)

## 2 mapset.cpp

This second program for Homework 8 has the same behavior as Homework 2’s `word_count`, but uses STL `set`, `map`, `lambda`, `ranges`, and `algorithms`, rather than low-level `for`, `while`, `do-while` loops, or `vector`. Many students are tempted to use `vector`, because it is more familiar, but resist that temptation! You only need the containers `set` and `map`.

Write a C++ program, named `mapset`, in the files `mapset.hpp`, `mapset.cpp`, and `mapset_main.cpp`, that

- reads the contents of a file named `sample_doc.txt`,
  - counts the frequency of each word in the file (i.e., how many times a word occurred) using a `std::map`,
  - excludes common words given in a file named `stopwords.txt`, using a `std::set`, and
  - ignores upper- and lowercase letters, converting all to lowercase using `std::transform()` or [`ranges`](https://en.cppreference.com/w/cpp/ranges), `tolower`
- writes output to a file named `frequency.txt` 
  - with the words in ascending alphabetical order with their associated frequency count, one word per line.
  - C++ allows a very nice loop option for maps with a *destructuring for-loop* to assign `first` and `second` members of the `std::pair` into two named variables, e.g.,

```cpp
for (const auto& [word, count] : my_map) {
    cout << word << count;
}
```

### Sample input and output formats

If the `sample_doc.txt` file contains the following text:

```
This is a sample text file for the mapset program It is used to test the frequency count of words detected by the mapset program
```

And the `stopwords.txt` file contains the following words (noting that stop words can also be uppercase):

```
a is it of the to By
```

Then, the output file `frequency.txt` should contain the following (with no blank line at the beginning):

```
count 1
detected 1
file 1
for 1
frequency 1
mapset 2
program 2
sample 1
test 1
text 1
this 1
used 1
words 1
```

Sample input files for testing are provided:
- Sample input file `sample_doc.txt`
- Sample `stopwords.txt`

> 💡**Tip:** The bash command `diff` compares two files to see if they are the same or different:
> `diff fileA fileB`
> outputs just the differences. If they are the same, there will be no output.

> 💡 **Tip:**  Notepad on Windows DOES NOT display newlines at the end of the file in the same way as vim on Linux.

**Be sure to follow the [General Steps of Development](#general-steps-of-development) for the approach to develop `mapset`. Some relevant details may be provided only in the Steps.**

mapset.hpp screenshot

![mapset.hpp screenshot](/assets/2-1.png)

mapset_main.cpp screenshot

![mapset_main.cpp screenshot](/assets/2-2.png)

## 3 compute_grades.cpp

Write a C++ program named `compute_grades`, in three files named `compute_grades.hpp`, `compute_grades.cpp`, and `compute_grades_main.cpp`,  that computes course grades given a gradebook defined in an input file named `gradebook.txt`. The program produces an output file, named `course_grades.txt`, with a list of students followed by their course grade summaries of each component average (with components Homework, Quiz, and Final), and the final course grade (numerical and letter) computed as a weighted sum of component averages (after dropping one lowest quiz score).

Focus on these because they will be useful: 

- `ifstream`
- `ofstream`
- `istream_iterator<>()`
- `ostream_iterator<>()`
- `operator<<()`
- `operator>>()`
- `string`
- `stringstream`
- `vector`
- `for_each` or `ranges::for_each()`
- `min` or `ranges::min()`
- `round()`
- `to_string()`
- `accumulate()`
- `back_inserter()`
- `partition_point` or `ranges::partition_point()`
- `tie()`
- `getline()`
- `setw()`
- `sort ranges::sort()`
- `copy` or `ranges::copy()`

> **In this program, avoid using low-level for loops and/or while loops! Use an algorithm that does what you need.**

### Input format

The gradebook is stored in a file with the following format:

- Each `"student"` has a group of 4 attributes defined by a keyword (`Name`, `Quiz`, `HW`, `Final`) for each of the course components.
  - The keyword `Name` is followed by one first name and one (or more) last name(s), separated by spaces.
  - The keyword `Quiz` is followed by a sequence of (zero, one, or more) integer scores on one line, separated by spaces.
  - The keyword `HW` is followed by a list of (zero, one, or more) integer scores on one line, separated by spaces.
  - The keyword `Final` is followed by a single integer score for the final exam.
  - The Quiz, Homework, and Final scores are **all integers which must be in the range 0 to 100 inclusive**, so that they are considered as points out of 100 possible, or like percentages.
    - This requirement is handled by `Student::validate()`. If any score is outside the valid range, throw an instance of the exception `std::domain_error` containing the `std::string` message `"Error: invalid percentage 106"` where the number 106 is the actual score value that is outside the valid range. Read about `std::domain_error` [here](https://en.cppreference.com/w/cpp/error/domain_error).
  - If any of these keyword lines is missing for any student, assume the score for that category is zero. For example, if `Quiz` is missing, assume the student took no quizzes, and their Quiz average is `0`.
  - If `Name` is missing, have it default to `"Missing Name"` then treat it like any other student and include it in the output.
- For a given student, keywords with their values can appear in any order, but they are together in a group before the blank line.
- The number of scores following either `Quiz` or `HW` can vary (zero, one, or more), but each is given on one line.
- There is a blank line following each student (including after the last student in the file).

### Example of gradebook format, given in the sample input file gradebook.txt

![gradbook format screenshot](/assets/3-1.png)

### Calculating component averages and course grades

The program calculates the course score and letter grades according to the following rules:

- Compute the quiz average. If there are two or more quiz scores, drop the lowest quiz score before computing the quiz average. If there is only one score, it must count, so that quiz score is the average.  If there are no quiz scores, the quiz average is zero.
- The quiz average counts as 40 percent of the course grade.
- All homework assignments count, and the homework score average counts as 30 percent of the course grade.
- The final exam counts for 30 percent of the course grade.
- The course score is rounded to the nearest whole integer, so .5 and above rounds up to the next whole integer, while below .5 rounds down to the next whole integer.

Calculating course grade: Course grades are assigned according to the following scale.

| Score | Grade |
| -- | -- |
| 97-100 | A+ |
| 93-96 | A |
| 90-92 | A- |
| 87-89 | B+ |
| 83-86 | B |
| 80-82 | B- |
| 77-79 | C+ |
| 73-76 | C |
| 70-72 | C- |
| 67-69 | D+ |
| 63-66 | D |
| 60-62 | D- |
| 0-59 | F |

### Output format

Print the output to a file named `course_grades.txt`, with a summary of each component average in the following format, with students’ names sorted in ascending alphabetical order, with the primary sort key the last name, and the secondary key the first name.

Note: Use left alignment in a field width of size 8 for the labels: `Name:`, `HW Ave:`, etc. These are done using the `iomanip` `setw()` and `left`.

```
Name:   Lisa Simpson
HW Ave: 100
QZ Ave: 100
Final:  100
Total:  100
Grade:  A+
<blank line>
```

The following sample `course_grades.txt` is generated by running `compute_grades` (compare your output to the sample output file `course_grades.txt`).

![sample output file course_grades.txt](/assets/3-2.png)

**Be sure to follow the [General Steps of Development](#general-steps-of-development) below for the general approach to develop this `compute_grades` program. Some helpful details may be found only in the Steps.**

compute_grades.hpp screenshot

![compute_grades.hpp screenshot](/assets/3-3.png)

compute_grades_main.cpp screenshot

![compute_grades_main.cpp screenshot](/assets/3-4.png)

## General Steps of Development

Submit any one of the three programs to the autograder for partial credit towards full credit.

> **❗Note:  If asking for help with your program on Ed Discussion, give the Program name and Step number you are working on in the Subject line of the post. For example,** `"process_numbers Step 2 input file reading issue"`

1. Create the files for the program you are writing. Write the `main.cpp` program and associated `.hpp` and `.cpp` file for the problem you are working on.
2. Declare your data structures - most likely on the stack local to the `main()` function.
3. Write and/or call the functions to read the data from the input file into your data structures. `getline()` may be used to read an entire line of input, then create a `stringstream` around that line so you can extract values from the remainder of the line using the extractor `operator>>()`.
4. Write print functions and print the data in your data structure to test that it is being built correctly.
5. Write any processing functions that compute or organize information required for the problem.
6. Write and/or call the functions to print the data from your data structures to the output files.
7. Compare your output to the expected output.
8. Once your program is functioning correctly, use the sanitizers and/or `valgrind` to help detect memory errors.  We will benefit from the Rule of Zero this week, so memory errors should be less common or maybe non-existent if we are lucky!

## How to Submit and Grade the programs

In **GradeScope** for **Homework 8**, upload from GitHub hw8 to submit any or all of the program files detailed above:

- `process_numbers.hpp`
- `process_numbers.cpp`
- `process_numbers_main.cpp`
- `mapset.hpp`
- `mapset.cpp`
- `mapset_main.cpp`
- `compute_grades.hpp`
- `compute_grades.cpp`
- `compute_grades_main.cpp`

## Build Instructions

```bash
# Produce the `build` folder with the presets provided for the homework:
cmake --preset default

# Build all targets at once:
cmake --build build

# Build only mapset_main.cpp:
cmake --build build --target mapset

# Build only process_numbers_main.cpp:
cmake --build build --target process_numbers

# Build only compute_grades_main.cpp:
cmake --build build --target compute_grades

# Build mapset gtests:
cmake --build build --target mapset_gtests

# Build process_numbers gtests:
cmake --build build --target process_numbers_gtests

# Build compute_grades gtests:
cmake --build build --target compute_grades_gtests
```

To run the above targets after compiling them:

```bash
./build/mapset                  # Runs the 'main' function from src/mapset_main.cpp
./build/process_numbers         # Runs the 'main' function from src/process_numbers_main.cpp
./build/compute_grades          # Runs the 'main' function from src/compute_grades_main.cpp
./build/mapset_gtests           # Runs the 'mapset' gtests
./build/process_numbers_gtests  # Runs the 'process_numbers' gtests
./build/compute_grades_gtests   # Runs the 'compute_grades' gtests
```

Once you have run the code above and it either produces the output you expected or passes
all provided tests, congratulations! You are now ready to [submit](#submission) your homework!

## Grading criteria

Points are allotted for

- Passing tests of functional correctness.
- **Using the STL as specified in the instructions, rather than `for` or `while` loops.**
- Preventing memory leaks. Major points are deducted for mismatched new and delete and other memory errors detected by valgrind.
- Programs that do not compile with the autograder testing programs receive no points.
- Crashes due to a segfault means the program is not at all useful and, therefore, receives no points.

*We may adjust grades manually when warranted. For example, a submission that attempts to defraud the autograder points by not implementing the requirements may be given a 0.*

## Submission

As with previous submissions, submit via `GitHub` by the following steps:

1. `git add .`
2. `git commit -a -m "Commit Message Here"`
3. `git push --set-upstream origin main`

to push your changes to your private GitHub repository, and then submit `hw8` to `Gradescope`.

> ⚠️ Be sure your #includes and using match exactly what is specified, for the autograder to run your submission with our own test programs.

## Credit

All code moved from [ICS45c](https://github.com/RayKlefstad/ICS45c/tree/hw8)
