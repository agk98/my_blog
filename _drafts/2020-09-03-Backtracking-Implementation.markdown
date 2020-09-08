---
layout: post
title:  "Solving Puzzles With Backtracking Algorithm."
description: In this post, I am going to show you how I implemented the backtracking algorithm to solve a Sudoku board as well as arrive at the right solution of a Peg Solitaire board.
date:   2020-09-03
categories: Algorithms
comments: False
---
<!-- Put introduction stuff -->
<!-- <h2><b>A little bit about backtracking.</b></h2> -->
<p>
    Backtracking is the technique used for problem solving. The algorithm follows a brute-force approach. Unlike Dynamic programming, which looks for the optimal solution, backtracking is used when there are multiple solutions to the problem and all of them need to be found.
</p>
<p> 
    Backtracking uses a recursive calling function to find a solution in a step-by-step manner. Each problem has a unique set of constraints which are checked after every step. If the currently found solution holds good with the constraints, then the program continues to the next stage. Otherwise, the program performs an undo operation where the current step solution is retracted, and the next feasible solution for the step is found. 
</p>
<p>
    So, backtracking algorithm can be seen as trying to find a path to the solution with small barriers where the problem can backtrack, if there is no feasible solution for the problem.
</p>

<h2><b>Solving a Sudoku Board. </b></h2>

<h3><b>Approach: Brute Force vs. Backtracking</b></h3>
<p>
    The regular Sudoku board is made up of a partially filled 9 x 9 grid of cells. To find the solution, one must fill each empty cell with digits from 1-9 so that every row, column and subgrid contains exactly one instance of the digit. A general approach to solving the puzzle would be to employ a Brute Force algorithm. This algorithm would be responsible for generating all the board, regardless of whether they are correct or no. This means that the algorithm is tasked with a huge task of generating a huge number of digits for each board and this results in a combinational explosion as the size of the board increases.
</p>
<p>
    Instead of this, I employed the technique of backtracking to solve the problem. The algorithm selects an empty cell and generates a number for this cell. It then proceeds to check whether this number belongs to the cell and doesn't break the board. If the number is proven to be in the right position, the algorithm continues by looking for the next cell. If the number is proven to be wrong for the position, the algorithm removes this number and tries the next digit. Hence, it performs backtracking and results in much lesser computation than the general brute force approach.
</p>

<h3><b>Lets Code!</b></h3>

<h4><b>Finding An Empty Cell</b><br/>
<script src="https://gist.github.com/agk98/943d47510bbbe9fa77223f4da0472e69.js"></script>
<p>
    The 9 x 9 Sudoku board is stored as 2-dimensional list. The empty cells are filled with the number '0' while the rest of the cells are filled with their respective numbers.
</p>
<p>
    The algorithm starts with finding an empty cell to fill with the right number. By looping through cells of every row and every column, it finds an empty cell. When the cell has the value of 0, it is said to be empty and the function <b>find_empty</b> returns the respective co-ordinates in the form of a tuple. 
</p>

<h4><b>Check Validity </b></h4>
<script src="https://gist.github.com/agk98/0fbd7c67e575b0e36151ac88b21c226a.js"></script>
<p>
    Once an empty cell is found, it is to be filled with a number between 1 and 9. The number should fit all the constraints of the problem and to check for it's validity, the function <b>check_validity</b> performs a series of checks.<br>
    It first checks to make sure that the inserted <b>number</b> is unique to that that respective row and column.<br>
    After this, the sub-grid that contains the current cell is checked. This is a 3 x 3 grid and must contain unique numbers between 1 and 9. To get the starting corner of the sub-grid, the row and column positions are divided by 3 and the floor value of this is retrieved. They are divided by 3 as the board is seen as a 3 x 3 grid of sub-grids. With the starting position of the sub-grid, the rows and columns of that subgrid are tested for validity of the numbers.<br>
    Only if the <b>number</b> passes all the constraints, then the function returns <b>True</b>. Otherwise, it returns <b>False</b>, prompting the algorithm to test the next number.
</p>

<h4><b>Solving Board </b></h4>
<script src="https://gist.github.com/agk98/263eaf6333a0003af99ace397abd11da.js"></script>
<p>
    This is the entry point of the program. After finding an empty cell, it finds a valid number to fit that cell. After assigning the valid number to that cell, it continues to find the next empty cell by recursively calling the function. <br>Everytime that the function finds out that the new number breaks the board, it backtracks and looks for a new solution.<br>Finally, once the solution is found, the board can be printed. In this way, backtracking can be used to find the solution to a Sudoku Board.
</p>


<h2><b>Solving a Peg Solitaire Board. </b></h2>

<h3><b>The Peg Solitaire Puzzle</b></h3>
