## Student# 16394923 

# Assignment 3 - P&T4AI

For this assignment we were required to code solutions for the Abstraction and Reasoning Corpus available at: https://github.com/fchollet/ARC

This repository contains my solutions for 4 of the ARC problems.



# The Abstraction and Reasoning Corpus (ARC)

This repository contains the ARC task data, as well as a browser-based interface for humans to try their hand at solving the tasks manually.

*"ARC can be seen as a general artificial intelligence benchmark, as a program synthesis benchmark, or as a psychometric intelligence test. It is targeted at both humans and artificially intelligent systems that aim at emulating a human-like form of general fluid intelligence."*

A complete description of the dataset, its goals, and its underlying logic, can be found in: [The Measure of Intelligence](https://arxiv.org/abs/1911.01547).

As a reminder, a test-taker is said to solve a task when, upon seeing the task for the first time, they are able to produce the correct output grid for *all* test inputs in the task (this includes picking the dimensions of the output grid). For each test input, the test-taker is allowed 3 trials (this holds for all test-takers, either humans or AI).


## Task file format

The `data` directory contains two subdirectories:

- `data/training`: contains the task files for training (400 tasks). Use these to prototype your algorithm or to train your algorithm to acquire ARC-relevant cognitive priors.
- `data/evaluation`: contains the task files for evaluation (400 tasks). Use these to evaluate your final algorithm. To ensure fair evaluation results, do not leak information from the evaluation set into your algorithm (e.g. by looking at the evaluation tasks yourself during development, or by repeatedly modifying an algorithm while using its evaluation score as feedback).

The tasks are stored in JSON format. Each task JSON file contains a dictionary with two fields:

- `"train"`: demonstration input/output pairs. It is a list of "pairs" (typically 3 pairs).
- `"test"`: test input/output pairs. It is a list of "pairs" (typically 1 pair).

A "pair" is a dictionary with two fields:

- `"input"`: the input "grid" for the pair.
- `"output"`: the output "grid" for the pair.

A "grid" is a rectangular matrix (list of lists) of integers between 0 and 9 (inclusive). The smallest possible grid size is 1x1 and the largest is 30x30.

When looking at a task, a test-taker has access to inputs & outputs of the demonstration pairs, plus the input(s) of the test pair(s). The goal is to construct the output grid(s) corresponding to the test input grid(s), using 3 trials for each test input. "Constructing the output grid" involves picking the height and width of the output grid, then filling each cell in the grid with a symbol (integer between 0 and 9, which are visualized as colors). Only *exact* solutions (all cells match the expected answer) can be said to be correct.


# Task Solutions
## Task 1 [0d3d703e] - A simple colour replacement

Colours correspond to other colours and are simply translated to more colours.

![0d3d703e](https://github.com/AJTYNAN/ARC/blob/master/0d3d703e.png)

The solution was to loop through the entries and replace each digit to match the corresponding colours.

## Task 2 [d4a91cb9] - Connecting two dots

The aim of this task was to connect a red and a blue square with yellow squares.
The connecting yellow squares are constrained vertically by the blue square and horizontally by the red square.

![d4a91cb9](https://github.com/AJTYNAN/ARC/blob/master/d4a91cb9.png)

The solution was to search the array for the locations of the blue and red squares. Then use the locations to draw a vertical line by comparing the y co-ordinates of the two squares, the line moves upwards if the red square is above the blue square or downwards if the blue square is above the red square.
The same thing happens for the horizontal constraint by comparing the horizontal locations of the two squares to go left and right.

## Task 3 [a61ba2ce] - Finding corners to populate a 4x4 grid

This task contains a large grid with various corners placed randomly. The goal is to locate the corners and place them in a 2x2 grid in the corresponding corners.

![a61ba2ce](https://github.com/AJTYNAN/ARC/blob/master/a61ba2ce.png)

To solve this task the function loops through the large array in 2x2 blocks.
These blocks search in the form:
`[x[i,j],x[i+1,j]]`
`[x[i,j+1],x[i+1,j+1]]`

When a block with one non-zero number appears, check the location of the zero and populate the corner into the appropriate location in the 4x4 grid.

## Task 4 [c3f564a4] - Finishing the pattern

This task presents a pattern with various sections missing. The goal is to complete the pattern by filling in the missing sections.

![c3f564a4](https://github.com/AJTYNAN/ARC/blob/master/c3f564a4.png)

The function to solve this task begins by searching for a row that doesn't have a missing section. From the row the pattern can be extracted.
The program then loops through the array searching for any missing sections, if a missing piece is found check the location next to it. If the location next to it is not missing, use that location to fill in the missing section from the extracted pattern.