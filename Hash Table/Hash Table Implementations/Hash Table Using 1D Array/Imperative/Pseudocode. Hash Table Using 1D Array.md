```
DECLARE hashTable: ARRAY [0:10] OF INTEGER
DECLARE i, recordKey, searchRecordKey, foundIndex AS INTEGER

FOR i ← 0 TO 10
    OUTPUT "Enter Record Key: "
    INPUT recordKey
    CALL InsertHash(recordKey, hashTable)
NEXT

OUTPUT "Enter Search Record Key: "
INPUT searchRecordKey

foundIndex ← CALL SearchHash(searchRecordKey, hashTable)
IF foundIndex = -1 THEN
    OUTPUT "Not Found"
ELSE
    OUTPUT "Found"
ENDIF

FOR i ← 0 TO LENGTH(hashTable) - 1
    OUTPUT hashTable[i]
NEXT
```
```
PROCEDURE InsertHash(recordKey, hashTable)
    DECLARE index AS INTEGER
    index ← CALL HashFunction(recordKey, LENGTH(hashTable) - 1)
    
    WHILE hashTable(index) <> 0
        index ← index + 1
        
        IF index > LENGTH(hashTable) - 1 THEN
            index ← 0
        ENDIF
    ENDWHILE
    
    hashTable(index) ← recordKey
ENDPROCEDURE
```
```
FUNCTION SearchHash(recordKey, hashTable) RETURNS INTEGER
    DECLARE totalSearches, index AS INTEGER
    totalSearches ← 0
    index ← CALL HashFunction(recordKey, LENGTH(hashTable) - 1)
    
    WHILE hashTable(index) <> recordKey
        totalSearches ← totalSearches + 1
        index ← index + 1
        
        IF index > LENGTH(hashTable) - 1 THEN
            index ← 0
        ENDIF
        
        IF totalSearches > LENGTH(hashTable) - 1 THEN
            RETURN -1
        ENDIF
    ENDWHILE
    
    RETURN index
ENDFUNCTION
```
```
FUNCTION HashFunction(keyValue, maxPosition) RETURNS INTEGER
    RETURN keyValue MOD (maxPosition + 1)
ENDFUNCTION
```