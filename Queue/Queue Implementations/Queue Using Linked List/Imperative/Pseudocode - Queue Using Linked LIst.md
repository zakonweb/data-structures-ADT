```
TYPE Node
    DECLARE Data : Integer
    DECLAER NextPointer : Integer
END TYPE
```
```
CONSTANT MAX ← 10
CONSTANT NULL_POINTER ← -1

QueueFront ← NULL_POINTER
QueueRear ← NULL_POINTER
FreeListHead ← 0

DECLARE NodeList: ARRAY [0:MAX] OF Node
```
```
PROCEDURE InitializeNodes()
    FOR i ← 0 TO MAX - 2 DO
        NodeList[i].NextPointer ← i + 1
    NEXT
    NodeList[MAX - 1].NextPointer ← NULL_POINTER
END PROCEDURE
```
```
PROCEDURE Enqueue(Data : Integer)
    IF FreeListHead = NULL_POINTER THEN
        OUTPUT "Queue is full"
    ELSE
        NewNodeIndex ← FreeListHead
        FreeListHead ← NodeList[FreeListHead].NextPointer

        NodeList[NewNodeIndex].Data ← Data
        NodeList[NewNodeIndex].NextPointer ← NULL_POINTER

        IF QueueRear = NULL_POINTER THEN
            QueueFront ← NewNodeIndex
            QueueRear ← NewNodeIndex
        ELSE
            NodeList[QueueRear].NextPointer ← NewNodeIndex
            QueueRear ← NewNodeIndex
        ENDIF
    ENDIF
END PROCEDURE
```
```
FUNCTION Dequeue() RETURNS Integer
    IF QueueFront = NULL_POINTER THEN
        OUTPUT "Queue is empty"
        RETURN -1
    ELSE
        OldFrontIndex ← QueueFront
        QueueFront ← NodeList[QueueFront].NextPointer

        IF QueueFront = NULL_POINTER THEN
            QueueRear ← NULL_POINTER
        ENDIF

        NodeList[OldFrontIndex].NextPointer ← FreeListHead
        FreeListHead ← OldFrontIndex

        RETURN NodeList[OldFrontIndex].Data
    ENDIF
END FUNCTION
```
```
PROCEDURE Display()
    Size ← 0
    IF QueueFront = NULL_POINTER THEN
        OUTPUT "Queue is empty"
    ELSE
        OUTPUT "Elements in the queue: "
        CurrentIndex ← QueueFront
        WHILE CurrentIndex <> NULL_POINTER DO
            OUTPUT NodeList[CurrentIndex].Data, " "
            CurrentIndex ← NodeList[CurrentIndex].NextPointer
        ENDWHILE
        OUTPUT "" //NEWLINE

        OUTPUT "Front: ", QueueFront
        OUTPUT "Rear: ", QueueRear
        OUTPUT "Free: ", FreeListHead

        CurrentIndex ← QueueFront
        WHILE CurrentIndex ≠ NULL_POINTER DO
            Size ← Size + 1
            CurrentIndex ← NodeList[CurrentIndex].NextPointer
        ENDWHILE
        OUTPUT "Size: ", Size
        OUTPUT "" //NEWLINE
    ENDIF
END PROCEDURE
```
```
// Main section
CALL InitializeNodes()

WHILE TRUE
    Output "Circular Queue using Linked List with Free List"
    Output "1. Enqueue"
    Output "2. Dequeue"
    Output "3. Display"
    Output "4. Exit"
    Output "Enter your choice: "
    INPUT Choice

    CASE OF Choice
        1:
            INPUT Data
            CALL Enqueue(Data)
        2:
            Data ← Dequeue()
            IF Data <> -1 THEN
                OUTPUT "The dequeued element is: ", Data
            ENDIF
        3:
            CALL Display()
        4:
            EXIT WHILE
        ELSE:
            OUTPUT "Invalid choice"
    ENDCASE
ENDWHILE
```