![image](https://user-images.githubusercontent.com/106586186/174310459-3d76a968-ceed-4e18-b1a7-12b9cc7667a9.png)



1. INTRODUCTION

Sudoku is a logic-based number puzzle. It was invented in the USA by Howard Garns and published in 1979 in the puzzle books.The most common sudoku consists of a 9x9 gird. Some of the squares are already filled. The purpose of the puzzle  is to fill the remaining squares, using numbers from 1 to 9 exactly once in each row, column, and the nine 3 × 3 subgrids. 

Except for the simplest version, there are also other variants of the puzzle. In this case, we focus on one of the irregular sudoku in which subgrids take different combinations (thus the shapes) instead of 3x3. However, the rule that the numbers 1-9 will be put in each subgrid once is kept up. This makes this type of sudoku more difficult, but also more interesting.




2. EXPLANATION

Below we present the explanation of the codes of above-presented irregular sudoku in Prolog programme.

• Directive that we use to make integer constraints available in all Prolog programmes

	:- use_module(library(clpfd)).


• A block-comment that makes the programme more comprehensible

	/*
	sudoku(+Matrix)
	it is true if Matrix unify with a 9x9 matrix 
	that represent a valid sudoku. 
	*/
 

• The head and the neck

	sudoku(Matrix):-

Then we are describing a body created by adding individual elements (goals).
		
• Represents the number of elements in Matrix (subgrids)

	length(Matrix, 9),

• Each of the Matrix (subgrids) has the same length as the other Matrix (subgrids)

	maplist(same_length(Matrix), Matrix),


• The concatenation of all elements in Matrix; each of the element is between 1 and 9 

	append(Matrix, Elems), Elems ins 1..9,

•Every Matrix (subgrids) has distinct (not equal pairwise) elements

	maplist(all_distinct, Matrix),
			
• Transposition Matrix into Matrix2 to check if all elements are distinct also by selecting them in the vertical way (turning all the rows of a given matrix into columns and vice-versa)

	transpose(Matrix, Matrix2),
	
• Same as before- checking if every Matrix2 (subgrids) has all distinct elements

	maplist(all_distinct, Matrix2),
	

• Name lines and their elements

	Matrix= [L1, L2, L3, L4, L5, L6, L7, L8, L9],
	L1 = [E11, E12, E13, E14, E15, E16, E17, E18, E19],
	L2 = [E21, E22, E23, E24, E25, E26, E27, E28, E29],
	L3 = [E31, E32, E33, E34, E35, E36, E37, E38, E39],
	L4 = [E41, E42, E43, E44, E45, E46, E47, E48, E49],
	L5 = [E51, E52, E53, E54, E55, E56, E57, E58, E59],
	L6 = [E61, E62, E63, E64, E65, E66, E67, E68, E69],
	L7 = [E71, E72, E73, E74, E75, E76, E77, E78, E79],
	L8 = [E81, E82, E83, E84, E85, E86, E87, E88, E89],
	L9 = [E91, E92, E93, E94, E95, E96, E97, E98, E99],
	
• Set apart each group depending on colors (dodać coś o distinct???)

	all_distinct([E11, E12, E13, E14, E21, E23, E31, E41, E51]),
	all_distinct([E15, E24, E25, E26, E27, E28, E34, E43, E44]),
	all_distinct([E16, E17, E18, E19, E29, E36, E37, E38, E39]),
	all_distinct([E22, E32, E33, E42, E52, E61, E62, E71, E81]),
	all_distinct([E35, E45, E54, E55, E64, E74, E83, E84, E85]),
	all_distinct([E46, E47, E48, E49, E56, E59, E65, E66, E75]),
	all_distinct([E53, E63, E72, E73, E82, E91, E92, E93, E94]),
	all_distinct([E57, E67, E76, E77, E78, E86, E88, E95, E96]),
	all_distinct([E58, E68, E69, E79, E87, E89, E97, E98, E99]).

• Fill the given numbers  

	sudoku1([
		[9,_,_,3,_,8,_,_,5],
		[_,8,_,_,4,_,_,1,_],
		[_,_,_,_,9,_,_,_,_],
		[7,_,_,_,_,_,_,_,2],
		[_,1,4,_,_,_,2,3,_],
		[2,_,_,_,_,_,_,_,4],
		[_,_,_,_,7,_,_,_,_],
		[_,2,_,_,8,_,_,5,_],
		[3,_,_,9,_,4,_,_,7]
		]).
		
3. SOLUTION	

We can use the code to generate valid Sudoku boards. To see whole/all result in shape of sudoku (in more clear shape) we can add:

	maplist(portray_clause, S).

Sample query: 

	sudoku1(S), sudoku(S), maplist(label, S), maplist(portray_clause, S).

4. SUMMARY

Irregular sudoku is different everytime, that is why this code works only for one which is presented at the beginning. To solve other irregular sudoku it is necessary to describe every group (square) the same as in 32-40 lines. 

Authors:
Kinga Kołtun
Klara Marzec
For Knowledge Representation Subject
