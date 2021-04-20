# Java core

## String

### .lenght()
The method `int length()` returns the number of characters in the String.

### .charAt()
The method `char charAt(int index)` returns the char at a certain index.

OBS: Any invalid index throws an IndexOutOfBoundsException

### .indexOf()

The method indexOf() looks at the characters in the string and finds
the first index that matches the desired value.

    int indexOf(int ch)
    int indexOf(int ch, int fromIndex)
    int indexOf(String str)
    int indexOf(String str, int fromIndex)
    
### .substring()
The method substring() returns a piece of a string defined by the indexes

    String substring(int beginIndex)
    String substring(int beginIndex, int endIndex)
    
If the beginIndex is bigger then the endIndex or endIndex goes beyond the lenght 
an exception is generated.

### .toLowerCase() and .toUpperCase()

toLowerCase() and toUpperCase() is respectively all caps or none caps

