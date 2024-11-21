java c
ECE 2560 Intro to Microcontroller-Based Systems 
Autumn 2024 
Midterm #2 
Due: Wednesday, November 20 – by 4:10 PM (Before Class) 
Submission: Media Recording and File Uploads to Carmen
This assignment is individual work. You are not allowed to copy the work of others including AI. 
Part 1: Coding task 
You will write a program with interrupts that implements a simpler version of the Simon game – with only two colors, only one light at a time, and no sound.
The game: One of the LEDs turns on and the player must press the push button adjacent to the LED (i.e., S1 for red, S2 for green). If the player presses the correct button, the game continues, another LED turns on etc. etc.
If the player presses the incorrect button, the game is over as indicated by three blinks of the red LED. Afterwards, the green LED blinks the score of the game. If the player got zero correct, there is no green blink. If the player got one correct, there is one green blink; two correct, two green blinks etc.
The game resets thereafter and starts over. (The player can play as long as they continue to press the correct button. The score will overflow and roll back to zero at 65535.)
Please watch the short video posted to Carmen to see how the game works.
The coding: 
Start by downloading the file midterm_2.asm from Carmen. It has the play sequence, constant definitions, and some helper subroutines.
The play_sqn array is a byte array with 32 entries

where a 0 indicates GREEN and a 1 indicates RED. You will use following symbolic constant definitions when checking for the values 0 and 1

Each game starts at the beginning of the play_sqnc array (i.e., the first element with index 0)   and continuously loops through the array, i.e., after the last element is played, it goes back to the first element. Define a global variable in RAM to keep track of the current state of the game. You can call this variable state or index. Each game starts with state=0.
The game flow depends on the value of the elements in play_sqnc. If the current element is RED the red LED is turned on, if it is GREEN the green LED. The player is expected to press the button that is adjacent to the powered LED, i.e., S1 if the red LED is on, S2 if it is the green LED.If the player presses the correct button, the player scores a point and the game continues.  Define another global variable in RAM to keep track of the score. You can call this variable score. Each game starts with score=0.
You will write following parts of code. My recommendation would be to write the modules in the given order. Test each module, make sure it works correctly before moving on to the next one.
•    The main loop configures input and output and starts the game by calling the subroutine reset_game. This part is very straightforward. Check the solution to Quiz 7 if you need  help with configuring the LEDs and pushbuttons.
•    A subroutine called reset_game that resets the state and score, and starts the game, i.e., turns on the LEDs based on the first entry in the play_sqnc. Both the logic and coding for 代 写ECE 2560 Intro to Microcontroller-Based Systems Autumn 2024 Midterm #2R
代做程序编程语言this subroutine are straightforward (~12 lines of instructions).
•    A subroutine called game_over that makes the red LED blink three times. Both coding and logic are straightforward. For example: turn all LEDs off. Call delay. Toggle red LED. Call delay. Repeat 6 times. The subroutine delay is given in the asm file. (My code is ~10 lines of instructions.)
•    A subroutine called blink_score that makes the green LED blink the score. You can start with the previous subroutine (game_over), change the LED (green instead of red) and add logic to make the number of blinks variable (instead of always three). There should be no blinks if the score is zero. This subroutine is not difficult, make sure to start with the correct logic and implement it in a tangle-free way. (My code is ~10 lines of instructions.)
•    An interrupt service routine called the game_master. Every time the player presses one of the buttons, the game_master will run and manage the game. It will check whether the correct button was pressed. If the correct button is pressed it will prepare the next LED. If the incorrect button is pressed it will end the game and reset. This is the juiciest module. My code is ~32 lines of instructions. It is not difficult, but you need to have a good understanding of the game and a good plan. And some time. 
•    Finally, expand the IVT so that the game_master will run every time S1 or S2 is pressed by the player.
Keep in mind that ISRs and any subroutines called from an ISR are not allowed to modify any core registers. The game_master and the subroutines are allowed to modify the global variables you have created in RAM.
Be mindful of how your program uses resources; minimize RAM usage (you do not need more than two 16-bit variables) and code size (no spaghetti please). Add good comments that describe the way the code works.
Once you have written and tested your program, you are ready for submission.
Part 2: Submission – Media Recording, PDF and text files uploaded to Carmen 
Media Recording: 
Take a short video of yourself and your program in action.
Demonstrate a play with zero score, followed by plays of two different scores. Keep the video short. Carmen will do the recording, do not forget to press the submit button! 
PDF File: Screenshot of your code 
Take a screenshot of your main program (including variable definitions), your ISR, your subroutines, and your interrupt vectors and submit these screenshots in a PDF file.
Text File: Your source code 
Save the final version of your source code as txt file so it can be read in Carmen, and make sure that both files reflect your name, e.g., firstname_lastname.txt or name_number.txt.
Make sure to submit the correct source code in the correct format – no word or PDF files for source codes. I will randomly select and run source code files throughout the semester. If your source code file is missing, does not compile, or does not produce the results you demonstrate in your video you will receive zero points for the assignments – end of story.



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
