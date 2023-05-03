Download Link: https://assignmentchef.com/product/solved-cs061-assignment-4-the-limits-of-your-lc3-skill
<br>
The purpose of this final programming assignment is to test the limits of your LC3 skill by giving you a challenging implementation problem straight out of the textbook.

High Level Description

There is a server somewhere, called the Busyness Server. This server tracks whether 16 different machines connected to it are <strong>busy (0)</strong>​ or ​ <strong>free (1)</strong>​      :​ this information is stored in a single LC-3 word (aka a “bit-vector”).

You will write a menu-driven system that allows the user to query this bit-vector as to the availability of the 16 machines, in various combinations.




<h1>Before You Start Coding</h1>

This assignment is based on a variation of  <u>​Question 9.9</u>​ (p. 242 of the textbook) – which will require that you first work through the following:

<ul>

 <li>Example 2.11 (p. 37)</li>

 <li>Question 2.36 (p. 46)</li>

 <li>Question 5.6 (p. 146)</li>

</ul>

<em>(</em><u>​</u><em><u>Note:</u></em>​<em> I have lightly edited the wording of the following excerpts from the text for increased clarity) </em>

<h2>Example 2.11</h2>

Suppose we have eight machines that we want to monitor with respect to their availability. We can keep track of them with an 8-bit BUSYNESS vector, where a bit is 1 if the unit is free and 0 if the unit is busy. The bits are labeled 0 through 7, from right (lsb) to left (msb).

The BUSYNESS bit vector 11000010 corresponds to the situation where only units 7, 6, and 1 are free, and therefore available for work assignment.

Suppose work is assigned to unit 7. We update our BUSYNESS bit vector by performing the logical AND, where our two operands are the current bit vector 11000010 and the bit mask 01111111. The purpose of the bit mask is to clear ​<em>(set to 0)</em>​ bit 7 of the BUSYNESS bit vector, without affecting the remaining 7 bits. The result is the bit vector 01000010, which replaces the previous BUSYNESS.

Recall that we encountered the concept of bit mask in Example 2.7. Recall that a bit mask enables one to interact with some bits of a binary pattern while ignoring the rest. In this case, the bit mask ​<em><u>clears</u></em><u>​</u> bit 7 and <u>​<em>leaves unchanged</em></u>​ (ignores) bits 6 through 0.

Suppose unit 5 finishes its task and becomes idle. We can update the BUSYNESS bit vector by performing the logical OR of it with the bit mask 00100000. The result is 01100010, which again replaces the previous BUSYNESS.







<u>Question 2.36</u>​ ​<em>(see Homework 2) </em>

Refer to Example 2.11 (above) for the following questions.

<ol>

 <li>What mask value and what operation would one use to set machine 2 from <u>free​ </u>​ (1) to ​<u>busy</u></li>

</ol>

(0)?       ​<em>(Without changing the state of the other machines, obviously!) </em>

<ol>

 <li>What mask value and what operation would one use to set machines 2 and 6 to <u>​free​</u> (1)? <em>(Again, without changing the state of the other machines)</em>​.</li>

</ol>

<em>Note: This can be done with a single </em>​<em><u>boolean operation</u></em>​<em>, but it cannot be implemented in LC-3 assembly language with a </em><u>​<em>single instruction</em></u><u>​</u><em>! </em>

<ol>

 <li>What mask value and what operation would one use to set ​<strong><em>all</em></strong>​ machines to <u>busy</u>​ <u>​</u> (0)?</li>

 <li>What mask value and what operation would one use to set <strong><em>all</em></strong>​ ​ machines to ​<u>free</u>​ (1)?</li>

 <li>Develop a procedure to “interrogate” the status of machine 2 by isolating it as the “sign bit” (i.e. the msb).</li>

</ol>

For example, if the BUSYNESS pattern is 0101 1100, then the output of this procedure is 10000000. If the BUSYNESS pattern is 0111 0011, then the output is 0110 0000. In general, if the BUSYNESS pattern is:




the output is

<table width="160">

 <tbody>

  <tr>

   <td width="20">b2</td>

   <td width="20">b1</td>

   <td width="20">b0</td>

   <td width="20"> 0</td>

   <td width="20"> 0</td>

   <td width="20"> 0</td>

   <td width="20"> 0</td>

   <td width="20"> 0</td>

  </tr>

 </tbody>

</table>

Hint: What happens when you ADD a bit pattern to itself?

<h2>Question 5.6</h2>

Recall the machine busy example from Section 2.7.1. Assuming the BUSYNESS bit vector is stored in R2, we can use the LC3 instruction AND R3, R2, #1 to determine whether machine 0 is busy or not. If the result of this instruction is 0, then machine 0 is busy.

<ol>

 <li>Write an LC3 instruction that determines whether machine 2 is busy.</li>

 <li>Write an LC3 instruction that determines whether <u>​<em>both</em></u>​ machines 2 and 3 are busy.</li>

 <li>Write an LC3 instruction that indicates whether none of the machines are busy.</li>

 <li>Can you write a single LC3 instruction that determines whether machine 6 is busy? Is there a problem here?</li>

</ol>




The variation of <u>​Question 9.9</u>​ that you will implement in this assignment:

<em>(remember – 0 = busy; 1 = free) </em>

<ol>

 <li>Check if ​<em><u>all</u></em>​ machines are busy; return 1 if all are busy, 0 otherwise (i.e. if any are free).</li>

 <li>Check if ​<em><u>all</u></em>​ machines are free; return 1 if all are free, 0 otherwise (i.e. if any are busy).</li>

 <li>Check ​<em><u>how many</u></em>​ machines are busy; return the number of busy machines.</li>

 <li>Check ​<em><u>how many</u></em>​ machines are free; return the number of free machines.</li>

 <li>Check the ​<em><u>status</u></em><u>​</u> of a specific machine whose number is passed as an argument in R1; return 1 if that machine is free, 0 if it is busy.</li>

 <li>Return the <u>​<em>number</em></u>​ of the first (lowest numbered, or rightmost) machine that is free – i.e. a number between 0 and 15.    ​<strong>If no machine is free, return -1</strong>​ ​<em>(= xFFFF)</em></li>

</ol>

e.g. if the busyness vector is 0101 0100, then the first available machine is #2

<em>(Remember – </em>​<em><u>the lsb is always considered bit #0</u></em>​<em>)</em><strong>                          </strong>

<h1>Your Tasks</h1>

The assignment can be broken down into the following tasks:




<ol>

 <li>Your main code block should call a MENU subroutine, which prints out a fancy looking menu with numerical options, allows the user to input a choice, and returns in <strong>R1</strong>​ the user’s selection​ {1, 2, 3, 4, 5, 6, 7} If the user inputs a non-existent option, output an error message and re-print the menu; repeat until a valid entry is obtained.</li>

</ol>

Here is the menu that you will be using for the assignment:

<em>(it is given to you in the starter code as a single long string located at memory  address </em>​<strong><em>x6000) </em></strong>




***********************

* The Busyness Server *

***********************

<ol>

 <li>Check to see whether all machines are busy</li>

 <li>Check to see whether all machines are free</li>

 <li>Report the number of busy machines</li>

 <li>Report the number of free machines</li>

 <li>Report the status of machine n</li>

 <li>Report the number of the first available machine</li>

 <li>Quit</li>

</ol>




<ol start="2">

 <li>Write the following corresponding subroutines:

  <ol>

   <li>MENU</li>

   <li>ALL_MACHINES_BUSY</li>

   <li>ALL_MACHINES_FREE</li>

   <li>NUM_BUSY_MACHINES</li>

   <li>NUM_FREE_MACHINES</li>

   <li>MACHINE_STATUS</li>

   <li>FIRST_FREE</li>

  </ol></li>

</ol>




plus the two helper subroutines:

GET_MACHINE_NUM

PRINT_NUM




=========================================================================







<h1>Subroutine Headers</h1>

The following headers have been provided to you in the template.

<strong>NOTE</strong>:​ R1 is always used to return a numeric or character value; R2 to return a flag value

;—————————————————————————————————————–

; Subroutine: MENU

; Inputs: None

; Postcondition: The subroutine has printed out a menu with numerical options, allowed the ;                            user to select an option, and returned the selected option.

; Return Value (R1): The option selected:  #1, #2, #3, #4, #5, #6 or #7

;                                no other return value is valid.

;—————————————————————————————————————– ;—————————————————————————————————————–

; Subroutine: ALL_MACHINES_BUSY (#1)

; Inputs: None

; Postcondition: The subroutine has returned a value indicating whether all machines are busy

; Return value (R2): 1 if all machines are busy, 0 otherwise

;—————————————————————————————————————–

;—————————————————————————————————————–

; Subroutine: ALL_MACHINES_FREE (#2)

; Inputs: None

; Postcondition: The subroutine has returned a value indicating whether all machines are free

; Return value (R2): 1 if all machines are free, 0 otherwise

;—————————————————————————————————————–

;—————————————————————————————————————–

; Subroutine: NUM_BUSY_MACHINES (#3)

; Inputs: None

; Postcondition: The subroutine has returned the number of busy machines.

; Return Value (R1): The number of machines that are busy (0)

;—————————————————————————————————————–

;—————————————————————————————————————–

; Subroutine: NUM_FREE_MACHINES (#4)

; Inputs: None

; Postcondition: The subroutine has returned the number of free machines

; Return Value (R1): The number of machines that are free (1)

;—————————————————————————————————————–

;—————————————————————————————————————–

; Subroutine: MACHINE_STATUS (#5)

; Input (R1): Which machine to check

; Postcondition: The subroutine has returned a value indicating whether the machine indicated

;                             by (R1) is busy or not.

; Return Value (R2): 0 if machine (R1) is busy, 1 if it is free

;—————————————————————————————————————–

;—————————————————————————————————————–

; Subroutine: FIRST_FREE (#6)

; Inputs: None

; Postcondition: The subroutine has returned a value in R1

;                            indicating the lowest numbered free machine

; Return Value (R1): the number of the free machine

;—————————————————————————————————————–
















<strong><u>Helper subroutines (i.e. not included in menu)</u> </strong>

Both subroutines are required for Option 5 (MACHINE_STATUS);

PRINT_NUM is required also for Options 3, 4 and 6




;—————————————————————————————————————–

; Subroutine: GET_MACHINE_NUM

; Inputs: None

; Postcondition: The number entered by the user at the keyboard has been converted into binary,

;                and stored in R1. The number has been validated to be in the range {0,15}

; Return Value (R1): The binary equivalent of the numeric keyboard entry

; NOTE: You can use your code from assignment 4 for this subroutine, changing the prompt,

;       and with the addition of validation to restrict acceptable values to the range {0,15}

;—————————————————————————————————————–

Your assignment 4 code is kind of overkill for this purpose, as it accepts  &amp; converts to binary all possible numbers in range {-32768, +32767}, while we only want {0, 15}

However, the code is already written &amp; tested, so it is simpler to just package it as a subroutine and modify it a bit for the new purpose:

<strong><u>Required changes to your assn 4 code:</u> </strong>

<ul>

 <li>The binary value must be returned in <strong>R1</strong>​ , rather than the register specified for assn 4​</li>

 <li>The prompt and error messages in assn 4 were provided as <em>remote</em>​ ​ data, requiring the use of pointers to access them. You must substitute these with the new prompt &amp; error messages, which are provided in the starter code as <em>local</em>​ ​</li>

</ul>

So in assn 4 you would probably have set up the string output like this:

<strong>LD R0, msg_pointer ; msg_pointer stores remote address of message string</strong>  In this subroutine version make sure you change that to:

<strong>LEA R0, msg_label ; msg_label is start of local message string</strong>

<em>If you have trouble understanding this advice, go back &amp; redo labs 2 &amp; 3!!) </em>

<ul>

 <li>Treat an initial ‘-‘​ ​ sign as an invalid input, exactly as you would a non-numeric input</li>

</ul>

<strong><em>NOTE</em></strong>​<em>: This is different from the behavior depicted in sample screen 9 below, which shows user entry “-14”: this spec requires that the ‘-‘ sign </em><u>​<em>immediately</em></u><u>​</u><em> trigger the error handler. </em>

<ul>

 <li>After successfully converting the user input number, you must test that it is &lt;= 15 (you already know that it is &gt;=0, because you rejected negative inputs). If the the number is &gt;15, it is invalid, so start over.</li>

</ul>




;—————————————————————————————————————–

; Subroutine: PRINT_NUM

; Inputs: R1, guaranteed to be in range {0,15}

; Postcondition: The subroutine has output the number in R1 as a decimal ascii string

; Return Value : R1 (unchanged from input)

;—————————————————————————————————————–

<ul>

 <li>Do <strong>NOT</strong>​ output a newline after the number output, as it may be part of a larger message.​</li>

 <li>if n &lt; 10, it is a single digit, and can be output as ascii by just adding x30</li>

 <li>if n &gt;= 10, it is a 2-digit number: the first digit is ‘1’, and the second digit is (n-10)</li>

</ul>

<h1>Expected/ Sample output <em>Output</em></h1>

<ul>

 <li>The caption for each sample screen lists the corresponding menu selection &amp; value of the test busyness vector</li>

 <li>Note the placing of newlines in the output!</li>

</ul>




<strong><em>Examples </em></strong>

<strong> </strong>




<ol>

 <li>Wrong Input for menu, BUSYNESS = x0000<strong>                                      </strong>2. Option 1, BUSYNESS = x0000</li>

</ol>




<ol start="3">

 <li>Option 1, BUSYNESS = xABCD 4. Option 2, BUSYNESS = xFFFF</li>

</ol>




5.(Option 2, BUSYNESS = xABCD                                              6. Option 3, BUSYNESS = xABCD




<ol start="7">

 <li>Option 4, BUSYNESS = xABCD 8. Option 5, BUSYNESS = x0000 with correct input</li>

</ol>




<ol start="9">

 <li>Option 5, BUSYNESS = x0000 with incorrect input 10. Option 5, BUSYNESS = x0000 with incorrect</li>

</ol>

example #1                                                                          input example #2




<ol start="11">

 <li>Option 6, BUSYNESS = x0000 12. Option 6, BUSYNESS = xABCD</li>

</ol>

<strong> </strong>

<strong>Notes: </strong>

<ul>

 <li>As always, you must echo ​<u>all​</u> inputs (no “ghost writing”).</li>

 <li>When an invalid input is detected: Output the error message and re-prompt the user for input</li>

 <li><strong><em>all outputs must be newline terminated</em></strong></li>

</ul>

<em>(except the number in machine status, which is internal to a larger message) </em>




Your code will obviously be tested with a range of different busyness vectors:  Make sure you do likewise!

<strong> </strong>

<strong> </strong>

<strong>Uh</strong><u>…</u><strong>help? </strong>

No individual component of this assignment is really difficult – but it has a lot of “moving parts” that all have to work together properly, so it can be ​<em><u>very</u></em>​ challenging, and take a <u>​<em>long</em></u><u>​</u> time to complete! So we’ll give you some hints  &#x1f642;




<u>Really, Really Important</u>

<h1>● 1 means free; 0 means busy</h1>

<ul>

 <li>Store the BUSYNESS vector at the memory address ​<strong> given to you in the template.</strong></li>

</ul>

○ The grader will test different values using this address

<ul>

 <li>Several of your subroutines require input validation: make sure that there is no way to exit such a subroutine except by providing valid input – in other words, if the user messes up, the subroutine must start over, with all prompts ​<em>(see e.g. the three Option 5 samples above) </em></li>

</ul>




<h2>Hint 01</h2>

All the subroutine headers have been provided in the starter code, along with all prompts and error messages. Use the headers as a guide to the construction of your subroutines.

In particular, detailed guides for the two helper functions are provided with their headers above. <em>DO NOT ALTER ANY STRINGS OR ADDRESSES PROVIDED IN YOUR STARTER CODE! </em>




<h2>Hint 02</h2>

<strong>NEVER</strong>​ backup (store/reload) the register used to return a value!

<em>In all subroutines, R1 is used to return a numeric or character value; R2 is used to return a flag value</em> <strong>AWAYS</strong>​ backup R0 and R7 if your subroutine invokes any Traps; plus all registers used as temporary storage in the course of the subroutine.




<h2>Hint 03</h2>

Remember the algorithm you created to print out a number in binary: you examined each individual bit of a 16-bit register by “shifting” each bit into the msb in turn.

You will be using this same technique in several of your subroutines in this assignment.




<h2>Hint 04 – sub A (MENU)</h2>

This subroutine gets a ​<strong>single </strong>character from the user. You do ​          ​<strong>NOT</strong>​ have to press enter for the character to be accepted. The moment the user enters a character, it will be echoed, and the subroutine will try to validate the input {‘1’, ‘7’}; if valid, the option value will be returned in R1; if not, an error message should be output and the prompt repeated (i.e. start over).

Should you return the menu option as an ascii numeric digit, or as the corresponding number? Either can be made to work, but which do you think is easier to test after return to main?




After responding to any menu selection other than #7, the menu must be re-presented, in an infinite loop ​<em>(see pseudo-code at end)</em>​.

The only way to exit the loop is by selecting menu option 7 (“Goodbye”).




<h2>Hint 05 – subs B &amp; C (ALL BUSY/ALL FREE?)</h2>

If a machine is free, then it is NOT busy. If a machine is busy, then it is NOT free – i.e. you can use the exact same code structure for these two subroutines.

In both cases, return flag R2 = 1 for “affirmative” (all machines <u>​are</u>​ busy/free respectively).




<em><u>Hint 06 – subs D &amp; E (HOW MANY BUSY/FREE?)</u> </em>

These two subroutines form a pair like subs B &amp; C above – you can use the same logic for both.




<h2>Hint 07 – sub F (MACHINE STATUS)</h2>

The first step is to obtain user input by invoking the helper subroutine GET_MACHINE_NUM

This will return a <em><u>validated</u></em><u>​       </u>​ number from 0 to 15 in R1, to be passed directly to subroutine F. The same number is also passed, still in R1, to the other helper subroutine PRINT_NUM when printing the full status report.

The only acceptable return values from GET_MACHINE_NUM are in the range<strong> {0,</strong>​ ​ <strong>15}.</strong>​

<u>Examples of valid input:</u>                                           <u>Examples of invalid input:</u>

<em>(sub returns with value in R1)                                  (error message, repeat prompt) </em>

<ul>

 <li>12 -12</li>

 <li>0 16</li>

 <li>0003 +2g</li>

 <li>+4 g</li>

</ul>

<em>See also the guide provided with the helper subroutine headers above. </em>




<u>Machine numbers for subroutine F:</u>

The FIRST machine is machine 0 <em>(</em>​ <em>the lsb, or rightmost bit)</em>​; the LAST machine is machine 15 <em>(</em>​ <em>the msb, or leftmost digit) </em>Machine IDs:




Subroutine F can assume that the value in R1 has been properly validated {0, 15} If machine (R1) is busy, return flag R2 = 0; if it is free, return R2 = 1




<em><u>Hint 08 – sub G (FIRST_FREE)</u>  </em>

As for sub F: the “lowest numbered” machine is the rightmost bit, aka the lsb, aka bit 0

<em> </em>

<em>   </em>

<h2>Hint 09</h2>

To implement your menu-driven system, construct an <u>infinite loop​ </u> that works like this:<u>​ </u>

<em><u>NOTE</u></em>​<em>:</em> ​<em>Print (R1)</em>​<em><sup> means invoke </sup></em>​<em>PRINT_NUM(R1) </em>

<em>If you needed to print the contents of a different register, you would have to </em>​<em>R1 &lt;= Rx</em>​<em> first. </em>

<table width="385">

 <tbody>

  <tr>

   <td width="216"> while( true ) {</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="216">  R1 = menu()</td>

   <td width="169">; call MENU subroutine</td>

  </tr>

 </tbody>

</table>




if (R1 == 1)

R2 = all_machines_busy()      ; call ALL_MACHINES_BUSY subroutine     if (R2 == 1)

Print “All machines are busy
”     else

Print “Not all machines are busy
”




else if (choice == 2)

[similar]




else if (choice == 3)

R1 = num_busy_machines()        ; call NUM_BUSY_MACHINES subroutine

Print “There are “, (R1), ” machines busy
”




else if (choice == 4)

[similar]




else if (choice == 5)

R1 = get_machine_number()     ; validated user entry from #0 to #15     R2 = machine_status(R1)    ; call MACHINE_STATUS and pass in R1     if (R2 == 1)

Print “Machine “, (R1), ” is free
”     else

Print “Machine “, (R1), ” is busy
”




else if (choice == 6)

R1 = first_machine_free()       ; call FIRST_FREE subroutine

if (R1 == -1 )                   ; #-1 == xFFFF

Print “No machines are free”

else

Print “The first available machine is number “, (R1), ‘
’

; don’t forget to terminate this o/p with a nl!

; all other messages have their terminal nl built in.




else if (choice == 7)

Print “Goodbye!
”

HALT

}