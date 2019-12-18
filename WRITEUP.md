# Lab 9 Report: Sam, Isaac, and Ben

For our Lab 9 project, we attempted to evolve a program that could take a string and return it as all lowercase. We choose this problem because we wanted to see how evolution could handle iterating through a string and if it could handle setting up conditionals that correctly switched the case of uppercase letters.

## Problem Setup

Here is a list of all functions and constants we gave our program:
- in1 (the input)
- integer_empty?
- integer_dup
- exec_dup
- exec_if
- exec_while
- boolean_not
- string_take
- string_drop
- string_length
- string_dup
- string_flip_pos
- string_upper_at_pos?
- close
- integer_range
- true
- false
- "" (empty string)
String_flip_pos is a function that takes a string and integer and returns a string where the case of a letter has been flipped at the given integer position. If the position is out of range we just return the inputted string.
String_upper_at_pos? is a function that takes a string and an integer and returns true if there is a character at the given position which is uppercase, false otherwise (if the character is lowercase or the integer is out of range).
Integer_range takes an integer and returns a list of integers from 0 to the input.  Due to the way in which propel handles lists, the integers are placed on the integer stack such that they are accessed in reverse order; we felt that, while slightly unintuitive to human viewers, this would not interfere with the program's evolution in any way and so we elected not to change it.

For our error function, we used Levenshtein distance.  Test cases consist of 14 fixed test cases, and 20 test cases generated randomly on each run of the program; all test cases consist of only uppercase and lowercase letters, and are a maximum of 30 characters long.  Individuals are selected with tournament selection with a tournament size of 5, with the default reproduction mechanisms used for generating new individuals (50% chance of crossover, 25% chance of uniform addition, and 25% chance of uniform division). 

## Results

The program was able to iterate through the string but was unable to handle conditionals correctly. Instead, it tended to  flip characters at fixed distances from the end of the string (as, due to the way in which integer_range works, it iterates through the string backwards).  Occasionally it would use conditionals, but not in intelligent ways--for instant, it would check if the last character was uppercase and if it was, flip the last two characters.  These led to stagnation, as it very efficiently found local maxima rather than actually understanding the nature of the problem.

## Changes

Initially, we attempted to have the program break the string down into a series of characters, handle each character individually, and reassemble them back into a string. We quickly realized that was too complicated and allowed it instead to directly modify the string. We briefly had it retrieve a character from a given position to check the character's case but we decided that allowing it to simply look at the string, rather than interact with characters, allowed a higher chance of success.

We also tested the difference between tournament and lexicase selection. While lexicase seemed to have slightly better results overall, it still ran into the smae problem of finding a local maxima and sticking to that.
