
#eprintf - The Embedded String I/O library
***

##Overview
eprintf is a collection of string I/O functions specifically written for embedded systems with low-memory capacity and low computing capacity like MCU. 
The recommended use of this library includes: debug/maintenance console and writing formatted strings into display device.

##API
#####Output APIs are:
* `void eputchar(int character)`
Writes a character to default I/O.
* `void eputs(const char* string)`
Writes every character from the null-terminated string to default I/O.
* `void eprintf(const char* formatStringPointer, ...)`
 Writes a formatted string to default I/O. For the syntax of  format placeholder, please refer to the comment at the start of the definition of this function in eprintf.c
* `void evprintf(const char* formatStringPointer, va_list argumentsPointer)`
Writes a formatted string to default I/O using variable argument list.
* `void esprintf(char *buffer, const char *formatStringPointer, ... )`
Writes a formatted string to a character string buffer. The behavior is undefined if the string to be written (plus the terminating null character) exceeds the size of the array pointed to by buffer.

#####Input APIs are:
* `/* upcoming soon */`

#####Others
* `#define CONVERT_CR_TO_CRLF_ENABLED 1`
Set this Macro to 1 when you want a '\n' printed as "\r\n". This Macro is set to 1 in default.
* `/* upcoming soon */`

##Replanting
User shall always remember to use the LINK_USER_OUTPUT() Macro to link the user-defined one-byte output function to the library. e.g.

* `LINK_USER_OUTPUT(UART1_PrintOneByte);`
* `LINK_USER_OUTPUT(LCD_PrintOneByte);`


##Examples

    //Examples for eprintf - The Embedded String I/O Library

    #include "eprintf.h"
    #include "stdio.h"

    int main(int argc, char const *argv[])
    {
	    //link the putchar() function in stdio.h to our library
	    LINK_USER_OUTPUT(putchar);

	    eprintf("1. Hello world\n");
	    eprintf("2. %d\n", 123);
	    eprintf("3. %6d,%3d%%\n", -75, 5);
	    eprintf("4. %-6u\n", 99);
	    eprintf("5. %ld\n", 123456789L);
	    eprintf("6. %04x\n", 0xA3);
	    eprintf("7. %08LX\n", 0x123ABC);
	    eprintf("8. %016b\n", 0x550F);
	    eprintf("9. %s\n", "String");
	    eprintf("a. %-6s\n", "abc");
	    eprintf("b. %6s\n", "abc");
	    eprintf("c. %c\n", 'a');
	    eprintf("d. %f\n", 10.0);

	    return 0;
    }

    //outputs are:
    1. Hello world
    2. 123
    3.    -75,  5%
    4. 99    
    5. 123456789
    6. 00a3
    7. 00123ABC
    8. 0101010100001111
    9. String
    a. abc   
    b.    abc
    c. a
    d. 'f' is not supported


