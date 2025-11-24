##Visual Studio Code for CS50
 -GUI: graphical user interface, clicking buttons.  
 -CLI: command line interface, type in the name of program to run it rather than click buttons.    
 
##Source code, compiler and machine code  
![I/O](/Users/angelaren/Documents/Programming notes/Generals/CS50x/IO.jpeg)  
  
-The document ```hello.c``` we made is where we write our source code. After writing the source code, we need to convert it into machine code that can be run by our computer. This is where we induce the compiler part, ```make hello```.  

 -We always omit the ```.c``` when using make as the make look for the ```hello.c``` and turn it into a program called ```hello```. ```make```trigger compilation of the code ```hello.c``.  
 
 -The ```./hello``` will read the machine code compiled by make and execute it saying ```hello, world```. 
 
###Basic syntax in C  
-To display any texts on the screen, we use a build-in function called ```printf```.  

    printf("hello, world\n");  
-We have to put the display texts inside opening and closing parenthese, and we also have to surround everything in double quotes, if you are using a string variable. ***Not single quotes in C for string***  

-The ```\n``` inside tells the compiler to create a new line of command code, rather than following right after the output.  
-This \ character is called an *escape character* that tells the compiler that \n is a special instruction to create a line break.  

**Some other escape characters**

    \n  create a new line
	\r  return to the start of a line
	\"  print a double quote
	\'  print a single quote
	\\  print a backslash  
	
##Header files  
  
 -Any files that end in ```.h``` is what we're going to call a header file. It tells the compile that you want to use the capabilities of a *library* called ```stdio.h```, by including the code ```#include <stdio.h>```at the start of the code.  
 -A library is a collection of code that someone else wrote for you, it's a package of existing functions you can acess by including header files.  
 
###Example of functions from library  
 
     // get_string and printf with %s

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
    	string answer = get_string("What's your 	name? ");
    	printf("hello, %s\n", answer);
	}   
	
 -At the start, we include the libraries containing the wanted functions using ```#include <lib.h>```.  
 
 -The ``get_string``` function is used to get a string from the user. Then, the variable ```answer``` is passed to the ```printf``` function. ```%s``` tells the ```printf``` function to prepare itself to receive a string.  
 
 -Inside the ```get_string``` function, we can enter the text we want to display while waiting for an user input to be received.  
 
 -The ```string``` in front of the variable ``` answer```states that the variable format is a type of data, string.  
 
 -```%s``` is a placeholder called a *format code* that tells the ```printf``` function to prepare to receive a string. ```answer``` is the string being passed to ```%s```. This has to be separated by a comma ,.  
 
 ***Remember to add a semi-colon at end of the statements to terminate it.***  
 
##Conditionals  
    // Compare integers

	if (x < y)
	{
    	printf("x is less than y\n");
	}
	else if (x > y)
	{
    	printf("x is greater than y\n");
	}
	else
	{
    	printf("x is equal to y\n");
	}
	  
 -The two sets of curly braces are used to define code blocks; we put what functions they should have inside the curly braces and separate them from other code blocks.  
 
 -The data type ```char```is a type of data that represents a single character or letter, it should be in *single*
 -The operators in C are ```||``` which stands for *or* and ```&&``` which stands for *and*.  
 
##Type of Loops
 -While loop:  
 
	#include <stdio.h>
	int main(void)
	{
    	int i = 0;
    	while (i < 3)
    	{
        	printf("meow\n");
        	i++;  //decrement by 1
    	}
	}  

 -The parenthetical is actually itself a Boolean expression. In a while loop here in C the Boolean expression is evaluated again and again everytime you go through the loop, to check if you should keep going through the loop. *keep looping while true*  
 
 -For loop:  
 
    #include <stdio.h>

    int main(void)
	{
    	for (int i = 0; i < 3; i++)
    	{
        	printf("meow\n");
    	}
	}  
	
 -The ```for``` loop includes three arguments. The first one ```int i = 0``` start counter at zero. The second one ```i<3``` is the condition being checked. The third one ```i++``` tells the loop to increment by one each time.  
 
 
 -Whenever the code runs out of controll and start to get into an infinite loops, press ```ctrl+c``` to break out of the program.  
 
##Functions  
 -When writing codes, it is encouraged to put the function ```main``` at the top of the program, so we put the user-defined funciton to the bottom or after the ```main``` function.  But how do we define a function that is needed inside the ```main``` function, if C can only follow a flow of codes that are in order?  
 
 -By solving this problem, we write down the first line of our function (with semicolon added), which make it a *prototype* of the function.  
 
 -In a function, we need to define the type of *output* and *input* it accept by using the format codes.  
 	-If there are no I/O of a funciton:  
 		```void meow(void)```  
 	-If there's only input for a funciton:
 		```void meow(int n)  
 	-If there's only output for a function:
 		```int meow(void)```  
 		
 
 // Abstraction with parameterization

	#include <stdio.h>

	void meow(int n);

	int main(void)
	{
    	meow(3);
	}

	// Meow some number of times
	void meow(int n)
	{
    	for (int i = 0; i < n; i++)
    	{
        	printf("meow\n");
    	}
	}  
	
-What should we do when the user enters unwanted values to keep asking them for a correct value?  

###do...while loop  
不像 for 和 while 循环，它们是在循环头部测试循环条件。在 C 语言中，do...while 循环是在循环的尾部检查它的条件。  

do...while 循环与 while 循环类似，但是 do...while 循环会确保至少执行一次循环。   

-By using ```do...while```, we can allow the user to enter a number first, then we check if the number is available at the end. We also formed a loop that keep checking if the input is valid, and if not, the loop continues until valid answer is entered.  

***We use ```do...while``` when we want to do something at least once but potentially again and again, not like for or while loop that just keep looping.***  

	// Return value

	#include <cs50.h>
	#include <stdio.h>

	int get_positive_int(void);
	void meow(int n);

	int main(void)
	{
    		int n = get_positive_int();
    		meow(n);
	}

	// Get number of meows
	int get_positive_int(void)
	{
    		int n;	//we declare the funciton there
    		do
    		{
       		n = get_int("Number: ");	//then we define it 
    		}
    		while (n < 1);		//so n can be reached from here
    		return n;		//here the returned value is used in meow function
	}

	// Meow some number of times
	void meow(int n)
	{
    		for (int i = 0; i < n; i++)
    		{
        		printf("meow\n");
    		}
	}  

-The scoping of the variable; the variable is limited to a specific scope that it can only be used when they are in the same curly bracket, most of the time.   

-If we want to use a variable many times in different part of functions, we can declare a variable in advance outside of one scope, but then define it, initialise it elsewhere.  
  
***-This is the recommended way of writing codes in C, we declare a variable without giving it any value initially, then, in a specific part of function, we proceed to give it a value. By doing this we ensure the variable can be reached by other functions.***