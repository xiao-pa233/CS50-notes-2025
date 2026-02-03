## Pixel arts  
 -Pixels are squares,individual dots, of color that are arranged on an up-down, left-right grid.  
 -You can imagine an image as a map of bits, where zeros represent black and ones represent white.  
 
 -By doing this, we can draw pixel arts on our computer and documents. This is an example of today's topic, of how we can start to manipulate data at a lower level, including images and other things.  
 
## Hexadecimal  
 -Hexadecimal is a system of counting that has 16 counting values: 
 
    0 1 2 3 4 5 6 7 8 9 A B C D E F  
    
 -The letters are used to represent the next six digits, 10 to 15, because we don't want two symbols on the screen. The highest number we can count using a two-digit hexadecimal system is 255, which is ``FF``. It also turns out that we can represent a single hex digit using four bits, as a hex digit has 16 values with is 2^4. So we tend to use two hexadecimal digits, which is equivalent to 8 bits, or a byte.  
 -You can imagine how there may be confusion regarding whether the ``10``block in the memory may represent a location in memory or the value ``10``. Accordingly, by convention, all hexadecimal numbers are often represented with the ``0x``prefix.  
  
  
## Pointers  
 -In C, if we use the ampersand operator, just one of them, not two, that is going to be the so-called address of operator. So you can write ampersand and the name of a variable, and the compiler essentially will tell you where that variable is in the computer's memory.  
	
	& Provides the address of something stored in memory.  
	* Instructs the compiler to go to a location in memory.  

 -When the program is running, you will be told where it is. The star operator is not multiply in this context. It's going to be the dereference operator, which is going to be a trick via which we can have an address and go there, following X marks the spot on a map and going to that location in memory and just see what's there, what data type is it.  
 
 -So the address of operator and the dereference operator, so to speak. But we need one other building block. Recall that printf has all those format codes like ``%s`` for string, ``%i`` for integer. Turns out there's another one, ``%p`` allow us to print what are called pointers.  

 -A *pointer* is a variable that stores the address of something. Most succinctly, a pointer is an address in your computer's memory.  
 
 -就不要用指针理解，直接当运算符理解就行了。&就是取地址运算，``*`` 就是取该地址对应的值。也就是 ``*`` 是``&``的逆运算。只不过用``*``的时候要先定义。  
 ![](/Users/angelaren/Documents/CS/Programming notes/Generals/CS50x/pointer.png)   
  
 -When you create a variable or declare a variable for the first time, you specify not only star, but the type of the pointer, just like any other variable declaration. But when you use the pointer subsequently, you do not mention the data type.   
 
	#include <stdio.h>

	int main(void)
	{
    	int n = 50;
    	int *p = &n;
    	printf("%p\n", p);
	}  
	
-It is important to understand that the keyword **string** is actually made up for us for convenience over the beginning part. String is actually an array containing character data type and ends with a null character.   
-If we print out the string's address and all of the characters' address inside the string, we will find out that the string's address as a whole is the same to the address of its first character.  
-If we get rid of those training wheels and even the CS50 library, we can actually start calling strings char stars, ``char *s``. A char star in C is known to mean you're just talking about a string.  

	#include <cs50.h>
	#include <stdio.h>

	int main(void)
	{
    	string s = "HI!";
    	printf("%p\n", s);
    	printf("%p\n", &s[0]);
    	printf("%p\n", &s[1]);
    	printf("%p\n", &s[2]);
    	printf("%p\n", &s[3]);
	}  
	
-Notice that, we used the & in front of each of the characters 0 through 3, but we didn't use it for the 'string' ``s`` as a whole. The reason we didnt' use it here is because we now know that ``s``is already a pointer. It is a char *. So if it's already an address and %p expects an address, there is no reason to do ``&s``, as the pointer ``s`` already holds an address. If we incorrectly use an ampersand here, that would be getting the address of the pointer, not the address of the string.  

## Pointer Arithmetic  
-If every chuck of memory has an address and that address is just a number, whether it's in hexadecimal, decimal, binary, whatever, they're just numbers, means that we can actually do math on addresses. This means if we can start in one location, we can go 1 byte away, 2 bytes away etc. just by adding 1 or 2 or more.   

	#include <stdio.h>

	int main(void)
	{
    	char *s = "HI!";
    	printf("%c\n", *s);
    	printf("%c\n", *(s + 1));
    	printf("%c\n", *(s + 2));
	}  
	
## String Comparison  
-A string of characters is simply an array of characters identified by the location of its first byte. We can compare the two integers by using the ``==`` operator. In the case of strings, however, one cannot compare two strings using the ``==``operator.  
-Using ``==``operator in an attempt to compare strings will attempt to compare the memory locations of the strings instead of the charaters therein. So we have to use ``strcmp`` instead. When trying to print the string, we use ``%s``, and ``%p`` to print out the address of the strings.  

## Copying and malloc  
-A common need in programming is to copy one string to another. Here, we want to copy the string as follows. We get string s from the user's prompt and copy the string as follows, string t equals s, then we capitalise the first character of t but not s.  

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
    	// Get a string
    	string s = get_string("s: ");

    	// Copy string's address
    	string t = s;

    	// Capitalize first letter in string
    	t[0] = toupper(t[0]);

    	// Print string twice
    	printf("s: %s\n", s);
    	printf("t: %s\n", t);
	}  
	
-However, when we run the program, both s and t were somehow capitalised for some reason, even though we only changed the first character of t. This is because that ``string t=s``copies the address of ``s`` to ``t`` instead of the string.  

![](/Users/angelaren/Documents/CS/Programming notes/Generals/CS50x/pointer_str.png)  

-As shown in the photo, ``s`` and ``t`` are still pointing at the same blocks of memory. This is not an authentic copy of a string. Instead these are two pointers pointing at the same string.   
-Before we address this challenge, it's important to ensure that we don't experience a *segmentation fault* through our code, where we attempt to copy ``string s``to ``string t``, where ``string t`` does not exist. We can employ the ``strlen`` funciton as follows to assist with that, so only when ``string t`` has content things will be copied.   

	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <string.h>

	int main(void)
	{
    	// Get a string
    	string s = get_string("s: ");

    	// Copy string's address
    	string t = s;

    	// Capitalize first letter in string
    	if (strlen(t) > 0)
    	{
        	t[0] = toupper(t[0]);
    	}

    	// Print string twice
    	printf("s: %s\n", s);
    	printf("t: %s\n", t);
	}
-To be able to make an authentic copy of the string, we will need to introduce two new building blocks. First, ``malloc`` allows you, the programmer, to allocate a block of a specific size of memory, or more specific, it will hand you back the address of that chunk of memory. Second, ``free`` allows you to tell the compiler to *free up* that block of memory you previously allocated, or more specific, hand back the address of that chunk of memory.  Once you're done with this memory, you can call free and give it back so that you don't eventually run out of memory.  
 
	#include <cs50.h>
	#include <ctype.h>
	#include <stdio.h>
	#include <stdlib.h>
	#include <string.h>

	int main(void)
	{
    	// Get a string
    	char *s = get_string("s: ");

    	// Allocate memory for another string
    	char *t = malloc(strlen(s) + 1);

    	// Copy string into memory, including '\0'
    	for (int i = 0, n = strlen(s); i <= n; i++)
    	{
        	t[i] = s[i];
    	}

    	// Capitalize copy
    	t[0] = toupper(t[0]);

    	// Print strings
    	printf("s: %s\n", s);
    	printf("t: %s\n", t);
	}
	
-Notice that ``malloc(strlen(s)+1)`` creates a block of memory that is the length of the string ``s``plus one. This allows for the inclusion of the *null* ``\0`` character in our final copied string, so the program knows when to stop. Also notice that ``n=strlen(s)`` is defined now in the left-hand side of the for loop. It's best not to call unneeded functions in the middle condition of the for loop, as it will run over and over again to calculate length of the string at the start of each loop. Defining ``n`` at left-hand side make the function ``strlen`` only runs once.   
-The C language has a built-in function to copy strings called ``strcpy``. It can be implemented as follows. ``strcpy(t, s);``. Both ``get_string`` and ``malloc`` return ``NULL``, a special value in memory, in the event that something goes wrong. 

	char *s = get_string("s: ");
	if (s == NULL)
	{
		return 1;
	}
	
-Once we are done using ``t`` in the first place, we can simply free ``t`` and C itself -- or the function that we are using keeps track of how many bytes you asked for. ``free`` lets the computer know you are done with this block of memory you created via ``malloc``, and it does the opposite of ``malloc``.  

## Valgrind  
-*Valgrind* is a tool that can check to see if there are memory-related issues with your programs wherein you utilised ``malloc``. Specifically, it checks to see if you ``free`` all the memory you allocated.  

## Garbage Values  
-When you ask the compiler for a block of memory, there is no guarantee that this memory will be empty. It is very possible that the memory you allocated was previously utilised by the computer. Accordingly, you may see *junk* or *garbage values*. This is a result of you getting a block of memory but not initialising it.  
-Initially, pointers don't point to anything. The thing they point to are called pointees, and setting them up is a separate step. We have to allocates a pointee and then dereference the pointer to store a data type into its pointee.   

## Swapping  
-In the real world, a common need in programming is to swap two values. Naturally, it's hard to swap two variables without a temporary holding space. By copying value ``x`` into a temporary variable ``temp``, then copy the value ``y`` into ``x`` and then copy the value in ``temp``back to ``y``, we swap the two values in ``x`` and ``y`` with a temporary variable.   

	// Fails to swap two integers
	
	#include <stdio.h>

	void swap(int a, int b);

	int main(void)
	{
    	int x = 1;
    	int y = 2;

    	printf("x is %i, y is %i\n", x, y);
    	swap(x, y);
    	printf("x is %i, y is %i\n", x, y);
	}

	void swap(int a, int b)
	{
    	int tmp = a;
    	a = b;
    	b = tmp;
	}  

-However, the code above failed to swap the values of ``x`` and ``y``. Why? The answer is related to memory. This is because that for code like this, encapsulated in a function, is not correct precisely for the matter of scope because we'are changing the values of variables that are local to the swap function but has no effect on main that's actually using the function.  
-This is because when we pass arguments to functions, you're generally passing things by value, which are the copies of those values, and there are no effect on the original versions of ``x`` and ``y``. So what swap really needs is a treasure map, so to speak, that leads it to the actual location of ``x`` and ``y`` using the ``*`` operator, so it can go there and swap the actual values inside of main's frame of memory.  
-So, instead of doing pass by value, we want to pass by *reference* or pass by *address*. Why? In terms of the computer's memory, we has standardised how we use computers' memories when running programs, and we tend to use the memory at the top in certain ways and type of memory at the bottom in other ways.   
![](/Users/angelaren/Documents/CS/Programming notes/Generals/CS50x/leap_stack.png)  
-When we run the program, the computer automatically loads the machine code compiled into the top of the computer's memory relatively. Then, it loads the global variables defined outside of main, and goes below the machine. The ``malloc`` function we used to allocate memory also comes from this location here, below the global. This type of data storage that grows downwards, and more stuff gets filled up top to bottom are what we called ``heap``.  
-The last region of memory are what we called the stack, its like a stack of trays in the cafeteria that works its way up as we continue putting stacks of tray and tray on top of each other, which the stack grows upward. It's like the guns clip，弹匣，先入后出，早放入的子弹最后才会被弹出。The heap and the stack are used differently. The heap is used for ``malloc``, or large and permanent type of data, and we have to free the memory when we don't need this data anymore manually.  
-For stack on the other hand, we use it when we call a function or when we have local variables, they are for small data and need to be read quickly. The memory in stack are pop out and destroyed at the same time.   
![](/Users/angelaren/Documents/CS/Programming notes/Generals/CS50x/stack.png)  
-Notice that ``main`` and ``swap`` have two separate *frames* or areas of memory. Therefore, we cannot simply pass the values from one function to another to change them, because only the copy is changed.  
-So, the ``swap`` function is logically correct, but it has not been given access to the locations of ``x`` and ``y`` in memory. We need a pointer that leads to the actual location of ``x`` and ``y``, so using the ``*`` operator it can go there and swap the actual values inside of main's frame of memory.   

	#include <stdio.h>

	void swap(int *a, int *b);

	int main(void)
	{
    	int x = 1;
    	int y = 2;

    	printf("x is %i, y is %i\n", x, y);
    	swap(&x, &y); //pass in address
    	printf("x is %i, y is %i\n", x, y);
	}

	void swap(int *a, int *b) //pointer declarations
	{
    	int tmp = *a; //start of pointer dereferencing
    	*a = *b;
    	*b = tmp;
	}  
-There, the addresses of ``a`` and ``b`` are provided to the function. Therefore, the ``swap`` function can know where to make changes to the actual values from the main function.  
-***The C in defualt only allows pass by value, if you want to pass by reference, we need to use pointer, so that's why we can't use &a &b in the swap function but *a and *b first.***   
![](/Users/angelaren/Documents/CS/Programming notes/Generals/CS50x/stack_pointers.png)  
 -When a function returns, the stack does not disappear, we still have remnants of all those values that were once there, unless the complier write over that memory. This is the problem, as the memory in stack is *free* as soon as the function returns the value, so it can be write over by other data at any moment, and the output will no longer be the original value. That's why we use ``malloc`` to make sure the value stick with us.  
   
   
##Overflow  
-A *heap overflow* is when you overflow the heap, touching areas of memory you are not suppsed to. It will write over other memory and causes data to be corrupted.  
-A *stack overflow* is when too many functions are called, overflowing the amount of memory available.  
-Both of these are considered *buffer overflows.*

##Scanf  
***-It is important to keep in mind that if we want another function to be able to change my variable, we can't just hand it the variable, we have to hand it the address of our variable.***  
-In, CS50, we have created functions like ``get_int`` to simplify the act of getting input from the user. ``scanf`` is a built-in function that can get user input, and we can reimplement ``get_int`` rather easily using ``scanf`` as follows:   

	#include <stdio.h>

	int main(void)
	{
    	int n;
    	printf("n: ");
    	scanf("%i", &n);
    	printf("n: %i\n", n);
	}  
	
-Notice that the value of ``n`` is stored at the location of ``n`` in the line ``scanf("%i", &n)``.  
-Howevery, attempting to reimplement ``get_string`` is not easy, as string is not an actual data type but an array of characters, which are act as pointers as well, so no ``&`` is required. We also don't know how many memory we need to allocate as we don't know how long of a string may be inputted by the user, and we don't know what garbage values may exist at the memory location.  
  
  
##File I/O  
-You can read from and manipulate files. While using C, we need pointer syntax to modify the files, there are a bunch of functions that come with C related to files. Any function that starts with an f probably means that it operates somehow on files, whether it's text files or binary files.  
-There's a data type called ``FILE`` in all capital letters, we use this data type to manipulate files.  
-We should get into the habit of checking return values. Any time pointers are involved from malloc, fopen and other functions asw, do not trust that they are valid until you have checked whether they are null or not.  

	#include <stdio.h>

	typedef unsigned char BYTE;

	int main(int argc, char *argv[])
	{
    	FILE *src = fopen(argv[1], "rb");
    	FILE *dst = fopen(argv[2], "wb");

    	BYTE b;

    	while (fread(&b, sizeof(b), 1, src) != 0)
    	{
        	fwrite(&b, sizeof(b), 1, dst);
    	}

    	fclose(dst);
    	fclose(src);
	}
