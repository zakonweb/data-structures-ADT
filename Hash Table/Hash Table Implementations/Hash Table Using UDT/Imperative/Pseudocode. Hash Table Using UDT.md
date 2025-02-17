```
TYPE RECORD:
    DECLARE key: INTEGER
    DECLARE value: STRING
END TYPE
```
```
FUNCTION HashFunction(key: INTEGER, size: INTEGER) RETURNS INTEGER
    RETURN key MOD (size + 1)
END FUNCTION
```
```
SUB InsertHash(record: RECORD, hashTable[] : RECORD)
    DECLARE index : INTEGER 
    index ← HashFunction(record.key, hashTable[].LENGTH - 1)

    WHILE NOT hashTable[index] IS NOTHING
        index ← index + 1
        IF index > hashTable[].LENGTH - 1 THEN
            index ← 0
        END IF
    ENDWHILE
    hashTable[index] ← record
END SUB
```
```
FUNCTION SearchHash(recordKey : INTEGER, hashTable[] : RECORD) RETURNS INTEGER
    DECLARE totSearches : INTEGER = 0
    DECLARE index : INTEGER 
    index ← HashFunction(recordKey, hashTable[].LENGTH - 1)

    WHILE NOT hashTable[index] IS NOTHING ANDALSO hashTable[index].key <> recordKey
        totSearches ← totSearches + 1
        index ← index + 1

        IF index > hashTable[].LENGTH - 1 THEN
            index ← 0
        END IF

        IF totSearches > hashTable[].LENGTH - 1 THEN
            RETURN -1
        END IF
    ENDWHILE

    IF NOT hashTable[index] IS NOTHING THEN
        RETURN index
    ELSE
        RETURN -1
    END IF
END FUNCTION
```
```
DECLARE recordKey, i : INTEGER
DECLARE recordValue : STRING
DECLARE record : RECORD
DECLARE searchRecordKey : INTEGER
DECLARE foundIndex : INTEGER

FOR i ← 0 TO 10
    ' Prompt the user to enter a record key and read the input as an integer
    OUTPUT"Enter record key: "
    INPUT recordKey

    ' Create a string for the record value using the record key
    recordValue ← "Customer " + STR(recordKey)

    ' Create a new record object with the key and value
    record.key ← recordKey
    record.value ← recordValue

    ' Call the InsertHash function to insert the record into the hash table
    CALL InsertHash(record, hashTable[])

NEXT i

' Prompt the user to enter a search key and read the input as an integer
OUTPUT"Enter Search Record Key: "
INPUT searchRecordKey : INTEGER

' Call the SearchHash function to find the record with the given 
' search key in the hash table
foundIndex ← SearchHash(searchRecordKey, hashTable[])

' OUTPUTthe result of the search
IF foundIndex = -1 THEN
    OUTPUT "Not Found"
ELSE
    OUTPUT "Found: " + hashTable[foundIndex].value
END IF

' OUTPUTthe values of all the records in the hash table
FOR item ← 0 TO hashTable[].LENGTH
    OUTPUT hashTable[item].value
NEXT
```