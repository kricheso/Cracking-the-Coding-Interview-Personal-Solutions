# <a name="Top" />Cracking the Coding Interview Personal Solutions

The purpose of this guide is to provide in depth explainations to the solutions in the book: Cracking the Coding Interview 6th Edition by Gayle Laakmann McDowell.

## Contents
* [Chapter 1 - String and Arrays](#Chapter1)
  * [Problem 1.1 - Is Unique](#Q1.1)


## <a name="Chapter1" />Chapter 1 - String and Arrays

### <a name="Q1.1" />Problem 1.1 - Is Unique
* Implement an algorithm to determine if a string has all unique characters. What if you cannot use addtional data structures?

One way to approach this problem is to use ASCII code. See below:

<img src="images/ASCIITable.png">

Becuase each character has an assigned integer value, we can make an array of size 128 (indexes 0-127) to represent each character in the english langauge. For example, 'a' = 97, 'b' = 98, and 'c' = 99. This means booleanArray['a'] == booleanArray[97]. 

```java
  //Program that prints: "Hello World!"
  public static void main(String args[]) {
  
    String[] array = new String[128];
    array[97] = "Hello World!";
    System.out.println(array['a']);   
    
  }
```

We will initialize all 128 values in our array to be false. This represents: "No, I have not seen this character yet". Since we are using 128 "blocks" of space, this simplifies down to O(1) becuase all constants are O(1) complexity. If we allocated a new data structure, we would have to use O(N) space because the input string might contain >100 million characters! 

Now all we need to do is loop through the input string. Everytime we see a unique character, for example c, change array['c'] = true. This represents: "This character is no longer unique". If we see a non-unique character, we will ask Mr. Array to see if that character is set to true. If the character is set to true, we know the character is not unique and we can return false. This will result in O(N) complexity becuase we will have to loop through each character in the input string. However, if we add a length check statement before the program starts, we can make the program O(1) time complexity, becuase the loop will never excute if more than 128 characters. And since 128 is constant, it is O(1) time.

```java
  public static boolean isUnique(String input) {
  
    //If there is more than 128 chracters in the string,
    //a character must have been repeated somewhere
    if(input.length() > 128) {
      return false;
    }
    
    //All boolean arrays are automatically initialized to false
    boolean[] alphabetArray = new boolean[128];
    
    for(int i=0; i<input.length(); i++) {
      
      //true means non-unique
      if(alphabetArray[input.charAt(i)] == true) {
        return false;
      }
      
      //If it is unique, set it to not unique
      alphabetArray[input.charAt(i)] = true;
      
    }
    
    return true;
    
  }
```

[Back to Top](#Top)
