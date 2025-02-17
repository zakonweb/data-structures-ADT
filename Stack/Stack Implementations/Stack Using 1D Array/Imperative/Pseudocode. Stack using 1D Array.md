```
// Declare constants and variables
CONSTANT NULL_POINTER = -1
DECLARE TOP_OF_STACK: INTEGER

// Initialize top of stack to null pointer and prompt user for stack size
TOP_OF_STACK ← NULL_POINTER
DECLARE SIZE: INTEGER
OUTPUT "Enter the size of the stack:"
INPUT SIZE

// Declare stack array and initialise with 0 values
DECLARE STACK : ARRAY[0 : SIZE - 1] OF INTEGER
FOR i ← 0 TO SIZE - 1 DO
    STACK[i] ← 0
```
```
// Subroutine to push a value onto the stack
PROCEDURE PUSH()
    // Prompt user for value to push onto the stack
    INPUT "Enter the value to push: ", VALUE

    // Push the value onto the stack
    IF TOP_OF_STACK = SIZE - 1 THEN
        OUTPUT "Stack is full. Cannot push value."
    ELSE
        TOP_OF_STACK ← TOP_OF_STACK + 1
        STACK[TOP_OF_STACK] ← VALUE
    ENDIF
ENDPROCEDURE
```
```
// Subroutine to pop the top value from the stack
PROCEDURE POP()
    // Pop the top value from the stack
    IF TOP_OF_STACK = NULL_POINTER THEN
        OUTPUT "Stack is empty. Cannot pop value."
    ELSE
        DECLARE VALUE: INTEGER
        VALUE ← STACK[TOP_OF_STACK]
        TOP_OF_STACK ← TOP_OF_STACK - 1
        OUTPUT "Popped value is " + VALUE
    ENDIF
ENDPROCEDURE
```
```
// Subroutine to display the stack as a list of values with the pointer at the top
PROCEDURE DISPLAY()
    // Display the stack as a list of values with the pointer at the top
    IF TOP_OF_STACK = NULL_POINTER THEN
        OUTPUT "Stack is empty. Cannot display value."
    ELSE
        OUTPUT "Pointer is at " + TOP_OF_STACK
        FOR i ← TOP_OF_STACK TO NULL_POINTER STEP -1 DO
            OUTPUT STACK[i]
        NEXT i
    ENDIF
ENDPROCEDURE
```
```
// Subroutine to display the entire stack array with the pointer value
PROCEDURE DISPLAY_ARRAY()
    // Display the entire stack array with the pointer value
    IF TOP_OF_STACK = NULL_POINTER THEN
        OUTPUT "Stack is empty. Cannot display value."
    ELSE
        OUTPUT "Pointer is at " + TOP_OF_STACK
        FOR i ← 0 TO SIZE - 1 DO
            OUTPUT "Index " + i + ": " + STACK[i]
        NEXT i
    ENDIF
ENDPROCEDURE
```
```
// Start menu loop
WHILE TRUE DO
    // Print menu options and prompt user for choice
    OUTPUT "1. Push"
    OUTPUT "2. Pop"
    OUTPUT "3. Display"
    OUTPUT "4. Display Array"
    OUTPUT "5. Exit"
    INPUT "Enter your choice: ", CHOICE

    // Perform selected operation based on user's choice
    IF CHOICE = 1 THEN
        PUSH()
    ELSEIF CHOICE = 2 THEN
        POP()
    ELSEIF CHOICE = 3 THEN
        DISPLAY()
    ELSEIF CHOICE = 4 THEN
        DISPLAY_ARRAY()
    ELSEIF CHOICE = 5 THEN
        // Exit the program
        EXIT WHILE
    ELSE
        // Invalid choice, ask the user to try again
        OUTPUT "Invalid choice. Try again."
    ENDIF
ENDWHILE
```