## Debugging
 -An important built-in function is breakpoint.  
 -If we hover the mouse over the 'gutter' in VS Code, there's a little stop sign or red dot that appears. When we click on the red dot, it gets redder and this is where we set a breakpoint.  
 -A breakpoint it where the program stop at (before the indicated line), the code will run but won't be beyond the breakpoint.   
 	-The button *step over* will run the 	breakpoint line but then pause on the next line.  
 	
## Types  
 -Each data type requires a certain amount of 	system resources:  
	bool 1 byte  
	int 4 bytes  
	long 8 bytes  
	float 4 bytes  
	double 8 bytes  
	char 1 byte  
	string ? bytes  
	
 -Basically, inside of the computer there is a finite amount of memory available. The size of each data type is relative to others in comparison.  
 
## Arrays  
 -An array is a sequence of values back-to-back or contiguous in memory, all of which are the same data type.  
 
 **-The syntax of an array:**  
     
     int scores[3];
   -There are three different part of an array, the first part is where you state the type of the variable, ```int```. The second part is the name of the variable, ```scores```. The third part is where you enter how many data you want to be associated with this variable, that is enclosed by square brackets, ```[3]```.  
   
 -To initialize each of these values in array to numbers, we just state the variable names and square bracket, then the corresponding value.  
 **-The array values are zero indexing, so starting from zero in square bracket.**   
// Averages three numbers using an array, a constant, and a helper function

	#include <cs50.h>
	#include <stdio.h>

	// Constant
	const int N = 3;

	// Prototype
	float average(int length, int array[]);

	int main(void)
	{
    	// Get scores
    	int scores[N];
    	for (int i = 0; i < N; i++)
    	{
        	scores[i] = get_int("Score: ");
    	}

    	// Print average
    	printf("Average: %f\n", average(N, 	scores));
	}

	float average(int length, int array[])
	{
    	// Calculate average
    	int sum = 0;
    	for (int i = 0; i < length; i++)
    	{
        	sum += array[i];
    	}
    	return sum / (float) length;
	}
 
 -Notice that the three variables are not different names, they are all called scores as they are stored under the same catalogue ```score```.  
 -In array, we find the data by indexing into the array to find the location we assign to the data.  
 
 
 -In the previous example code, ```int scores[3]``` is a way of telling the compiler to provide you three back-to-back places in memory of size ```int``` to store three ```scores```.
 
 
 -If we want to keep a varbiable unchanged, we can add ```const``` infront of the datatype. Sometimes its also a good idea to put your constants outside of the funcitons, so if we want to change it it is very obvious at the very top.  
 
 -Notice that a new function called ```average``` is declared. Further, notice that a ```const``` or constant value of ```N``` is declared. Most importantly, notice how the ```average``` function takes ```int array[]```, which means that the compiler passes an array to this function.  
 
 -In simple word, the function ```average``` is created with two parameter, one parameter ```length``` is the length of array and another one is ```int array``` that data type in array is processed. We put ```N``` as length and ```scores```, ***the whole array*** into function for it to process.  
 - ***Important idea, not only can arrays be containers, they can be passed between funcitons as a whole as well.***  

 
## Strings  
 -Strings are a sequence of characters, which means back-to-back contiguous in memory. In this way, the string can be seen as an array of characters, the size of string depends on the amount of length of characters in that array. A string is just a more precise type of array specifically containing characters.  
 
 -The string is an array of characters that begins with the first character and ends with a special character called a ```NUL character```, which is shown as ```\0```.  
 
 -Since the array's data are back-to-back which are next to each data, the automatically added ```\0``` is to distinguish what belongs to one data and what belongs to another data.  
 -The double quotes implies that this data is a ```string```, so let me terminate it with backslash 0. ***You do not want a \0 for a single char.***. And the single quotes means one character.  
 
 -If the words (strings) are the array, and the string is the array of the characters, we can actually use the square brackets twick. The first set of brackets says what word do you want and the second set of brackets says what character do you want, since this is an array of strings, so an array of arrays.  
 
 
## String length  

    #include <cs50.h>
	#include <stdio.h>

	int string_length(string s);

	int main(void)
	{
    	// Prompt for user's name
    	string name = get_string("Name: ");
    	int length = string_length(name);
    	printf("%i\n", length);
	}

	int string_length(string s)
	{
    	// Count number of characters up until 	'\0' (aka NUL)
    	int n = 0;
    	while (s[n] != '\0')
    	{
        	n++;
    	}
    	return n;
	}
	
 -We can determine the length of the string, which is an array itself, by looping through the index of the array until the corresponding value of the index is equal to zero. Each loop finished the count increase by one to count the length of the string.    
 
 -The loop scan the string from left to right and checking if the value is equal to null, if so, it stops the loop and print out the number of successful loop which is equal to length of loop.  
 -You can always initialise more than one variable in the for loop, which are separate by the comma ```,```.   
 
 -A character ```char``` is just an ```int```, and an ```int``` is just a ```char```, and you can format them however you want. ***Remember everything is based on binary numbers and bits and bytes.*** Due to this relationship, we can do arithmetic on characters and compare the characters numerically and use them in calculations.   
 
    #include <cs50.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
    	string s = get_string("Before: ");
    	printf("After:  ");
    	for (int i = 0, n = strlen(s); i < n; i++)
    	{
        	if (s[i] >= 'a' && s[i] <= 'z')
        	{
            	printf("%c", s[i] - ('a'-'A')); //equal to minus 32
        	}
        	else
        	{
            	printf("%c", s[i]);
        	}
    	}
    	printf("\n");
	}  
	  
	  
	  
	  #include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
    	string s = get_string("Before: ");
    	printf("After:  ");
    	for (int i = 0, n = strlen(s); i < n; i++)
    	{
        	if (islower(s[i]))
        	{
            	printf("%c", toupper(s[i]));
        	}
        	else
        	{
            	printf("%c", s[i]);
        	}
    	}
    	printf("\n");
	
 -In the code above, we do not need to worry about the line swap for a new character printed; this is because ***a new line won't be automatically added***, it is important to keep this in mind so we don't need to worry about format when a new character is printed out - it just added to the previous character from the back.  
 
 
## Command-Line Arguments  
 -```Command-line arguments``` are those arguments that are passed to your program at the command line. We are able to take arguents before the program runs, which we receive input in command lines straight forward.  
 
    #include <cs50.h>
	#include <stdio.h>

	int main(int argc, string argv[])
	{
		//expecting user input
		
    	if (argc == 2)
    	{
        	printf("hello, %s\n", argv[1]);
    	}
    	
    	//if there's no user input, return a default value
    	
    	else
    	{
        	printf("hello, world\n");
    	}
	}  
	
  -In the code above, instead of using ```void```, we assign two input to the ```main``` function.  
	-```argc``` is the counter for the NO. command-line arguments. This includes the name of the program so it is one-indexing.    
	-```argv``` is the whole array of the argument strings. The shell parses the input in command line and breaks it into separate strings automatically. **(only work with the main functions.)**  
	
## Exit status  
 -When a program ends, a special exit code is provided to the computer.  
 -When a program exits without error, a status code of ```0``` is provided to the computer. Often, when an error occurs that results in the program ending, a status of ```1``` is provided by the computer. This is because if program runs successful it runs, but the error can varies so we can use positive or negative values.  
 
## Cryptography  
 ![](cryptography.png)  
 
 -Cryptography is the art of ciphering and deciphering a message.  
 -```plaintext``` and a ```key``` are provided to a ```cipher```, resulting in ciphered text. 


 
