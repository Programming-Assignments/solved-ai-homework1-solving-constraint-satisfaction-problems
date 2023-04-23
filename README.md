Download Link: https://assignmentchef.com/product/solved-ai-homework1-solving-constraint-satisfaction-problems
<br>
The objective of this assignment is for you to practice with solving constraint satisfaction problems with searching (the backtracking search in the lecture slides).

The problems to be solved in this assignment are crossword puzzles without hints. Any words from a given word list can be used in the solution as long as the constraints are satisfied. To the right is an example crossword puzzle with a possible solution. (Note: Since we do not provide hints, the solution is not unique.)

A puzzle is specified in the format of (start_x, start_y, length, direction) for each word. For example, for the sample puzzle here, the specification is

<strong>0 2 5 A   1 1 5 D   3 0 7 D   1 4 5 A   3 6 4 A   5 4 3 D </strong>

The origin (0,0) is at the top-left corner. For directions, “A” means “across” and “D” means “down”.

To start, each word in the puzzle is a variable (6 variables here), and the provided word list is the initial domain. Consider the length of each word to be its unary constraint. Each block where two words intersect gives a binary constraint (there are 7 here).

The following are some notes about implementation:

<ul>

 <li>Before you start the search, apply the unary constraints so that the domain of each variable contains only words of the correct length. Optionally, you can use AC-3 to further trim the domains.</li>

 <li>Each node in the search tree needs to maintain the following information:

  <ul>

   <li>The variable+value combination to be assigned at this node (only for non-root nodes).</li>

   <li>The list of assignments between the root and the current node.</li>

   <li>The domains of all the variables. (This is required only if you want to apply forward checking or AC-3 after each assignment.)</li>

  </ul></li>

 <li>Use a stack for the backtracking search. Initialize the stack with only the root node with an empty list of assignment and initial variable domains.</li>

 <li>When popping a node from the stack (node expansion), do the following:

  <ul>

   <li>Add the variable+value combination of this node to its list of assignments, and set the domain of the assigned variable to contain only the assigned value.</li>

   <li>(If forward checking / AC-3 is used) Update the domains of the unassigned variables, if any.</li>

   <li>Consistency check: 1. Do the current list of assignments satisfy all the constraints? 2. (If forward checking / AC-3 is used) are all the variables still have nonempty domains?</li>

   <li>If consistency check returns TRUE and all the variables are already assigned, a solution is found, and the program returns with the solution.</li>

   <li>If consistency check returns TRUE and there are still unassigned variables:

    <ul>

     <li>Generate a list of child nodes, one for each variable+value combination of the unassigned variables.</li>

     <li>Copy the list of assignments and variable domains of the current node to the child nodes.</li>

     <li>Push the child nodes into the stack. (If the MRV/degree/LCV heuristics are used, you should push the child nodes in the order of <u>increasing</u>)</li>

    </ul></li>

   <li>If the stack becomes empty, there is no solution, and the program returns failure.</li>

  </ul></li>

</ul>




A file containing about 3000 English words is provided. Also the file puzzle.txt is provided, where each line represents a puzzle.

You submission is a report file in Word or PDF format. The report (maximum 5 pages single-spaced) should describe your experiments and results, especially the comparison between the different algorithms. Several topics that you can experiment with include

<ul>

 <li>Numbers of visited nodes for the different puzzles.</li>

 <li>How the numbers of visited nodes change with or without any of the heuristics.</li>

 <li>How the numbers of visited nodes change with or without the initial run of AC-3.</li>

 <li>How the numbers of visited nodes change with or without forward checking or AC-3 during the search.</li>

 <li>Is it possible to do a complete search (not stopping when solutions are found) and determine the numbers of valid solutions for the different puzzles?</li>

 <li>Can you somewhat randomize the search so that each run can generate a different solution?</li>

</ul>

Some example solutions to the provided puzzles:

<table width="508">

 <tbody>

  <tr>

   <td rowspan="5" width="55">


    <table width="54">

     <tbody>

      <tr>

       <td width="18"><strong>H</strong></td>

       <td width="19"><strong>O</strong></td>

       <td width="18"><strong>M</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>O</strong></td>

       <td width="19"> </td>

       <td width="18"><strong>A</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>U</strong></td>

       <td width="19"> </td>

       <td width="18"><strong>N</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>S</strong></td>

       <td width="19"><strong>A</strong></td>

       <td width="18"><strong>Y</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>E</strong></td>

       <td width="19"> </td>

       <td width="18"> </td>

      </tr>

     </tbody>

    </table></td>

   <td rowspan="5" width="170"></td>

   <td rowspan="5" width="63">


    <table width="55">

     <tbody>

      <tr>

       <td width="18"> </td>

       <td width="18"> </td>

       <td width="18"><strong>E</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>A</strong></td>

       <td width="18"> </td>

       <td width="18"><strong>A</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>D</strong></td>

       <td width="18"><strong>E</strong></td>

       <td width="18"><strong>G</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>D</strong></td>

       <td width="18"> </td>

       <td width="18"><strong>E</strong></td>

      </tr>

      <tr>

       <td width="18"> </td>

       <td width="18"> </td>

       <td width="18"><strong>R</strong></td>

      </tr>

     </tbody>

    </table></td>

   <td rowspan="3" width="63">


    <table width="54">

     <tbody>

      <tr>

       <td width="18"><strong>A</strong></td>

       <td width="19"><strong>S</strong></td>

       <td width="18"><strong>T</strong></td>

      </tr>

      <tr>

       <td width="18"> </td>

       <td width="19"> </td>

       <td width="18"><strong>H</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>R</strong></td>

       <td width="19"><strong>E</strong></td>

       <td width="18"><strong>E</strong></td>

      </tr>

      <tr>

       <td width="18"> </td>

       <td width="19"> </td>

       <td width="18"><strong>R</strong></td>

      </tr>

     </tbody>

    </table></td>

   <td width="157">


    <table width="149">

     <tbody>

      <tr>

       <td width="18"><strong>S</strong></td>

       <td width="19"><strong>M</strong></td>

       <td width="19"><strong>O</strong></td>

       <td width="19"><strong>K</strong></td>

       <td width="19"><strong>E</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="18"> </td>

      </tr>

      <tr>

       <td width="18"><strong>O</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="19"><strong>M</strong></td>

       <td width="19"><strong>O</strong></td>

       <td width="19"><strong>S</strong></td>

       <td width="18"><strong>T</strong></td>

      </tr>

     </tbody>

    </table></td>

   <td width="0"></td>

  </tr>

  <tr>

   <td width="157">


    <table width="148">

     <tbody>

      <tr>

       <td width="18"><strong>L</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="19"><strong>I</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="18"><strong>O</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>D</strong></td>

       <td width="19"><strong>E</strong></td>

       <td width="19"><strong>C</strong></td>

       <td width="19"><strong>I</strong></td>

       <td width="19"><strong>S</strong></td>

       <td width="19"><strong>I</strong></td>

       <td width="19"><strong>O</strong></td>

       <td width="18"><strong>N</strong></td>

      </tr>

      <tr>

       <td width="18"><strong>I</strong></td>

       <td width="19"> </td>

       <td width="19"><strong>H</strong></td>

       <td width="19"> </td>

       <td width="19"><strong>S</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="18"><strong>E</strong></td>

      </tr>

     </tbody>

    </table></td>

   <td width="0"></td>

  </tr>

  <tr>

   <td rowspan="2" width="157">


    <table width="148">

     <tbody>

      <tr>

       <td width="18"><strong>E</strong></td>

       <td width="19"><strong>V</strong></td>

       <td width="19"><strong>E</strong></td>

       <td width="19"><strong>N</strong></td>

       <td width="19"><strong>I</strong></td>

       <td width="18"><strong>N</strong></td>

       <td width="19"><strong>G</strong></td>

       <td width="18"> </td>

      </tr>

     </tbody>

    </table></td>

   <td width="0"></td>

  </tr>

  <tr>

   <td rowspan="2" width="63">


    <table width="54">

     <tbody>

      <tr>

       <td width="18"><strong>I</strong></td>

       <td width="19"><strong>D</strong></td>

       <td width="18"><strong>E</strong></td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td width="157">


    <table width="149">

     <tbody>

      <tr>

       <td width="18"><strong>R</strong></td>

       <td width="19"> </td>

       <td width="19"><strong>A</strong></td>

       <td width="19"> </td>

       <td width="19"><strong>O</strong></td>

       <td width="19"> </td>

       <td width="19"><strong>O</strong></td>

       <td width="18"><strong>R</strong></td>

      </tr>

      <tr>

       <td width="18"> </td>

       <td width="19"><strong>S</strong></td>

       <td width="19"><strong>P</strong></td>

       <td width="19"><strong>I</strong></td>

       <td width="19"><strong>N</strong></td>

       <td width="19"> </td>

       <td width="19"> </td>

       <td width="18"> </td>

      </tr>

     </tbody>

    </table></td>

   <td width="0"></td>

  </tr>

 </tbody>

</table>


