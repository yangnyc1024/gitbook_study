---
description: API
---

# String API

##

Question1: String底层是什么？

Ans:属于java.lang



<table><thead><tr><th width="200">Method API</th><th width="320">Description</th><th width="84">TC&#x26;SC</th><th></th></tr></thead><tbody><tr><td>charAt(int index)</td><td>Returns the car value at the specified index</td><td></td><td></td></tr><tr><td>compareTo(String anotherString)</td><td>Compare two strings <mark style="color:purple;">lexicographically.</mark></td><td></td><td></td></tr><tr><td>compareToIgnoreCase</td><td>Compares two strings lexicographically, ignoring case differences</td><td></td><td></td></tr><tr><td>concat(String str)</td><td>Concatenates the specified string to the end of this string.</td><td></td><td></td></tr><tr><td>equals(Object anObject)</td><td>Compares this string to the specified object.</td><td></td><td></td></tr><tr><td>equalsIgnoreCase(String anotherString)</td><td>Compares this String to another String, ignoring case considerations</td><td></td><td></td></tr><tr><td>indexOf(int ch)</td><td>Returns the index within this string of the first occurrence of the specified character</td><td></td><td></td></tr><tr><td>indexOf(String str)</td><td>Returns the index within this string of the first occurrence of the speecified  substring</td><td></td><td></td></tr><tr><td>length()</td><td>Returns the length of this string</td><td></td><td></td></tr><tr><td>repeat(int count)</td><td>Returns a string whose value is the concatenation of this string repeated count times.</td><td></td><td></td></tr><tr><td>replace(char oldChar, char newChar)</td><td>Returns a string resulting from replacing all occurrences of oldChar in this string with newChar.</td><td></td><td></td></tr><tr><td>replaceAll(String regex, String replacement)</td><td>Replace each substring of this string that matches the given regular expression with the given replacement.</td><td></td><td></td></tr><tr><td>split(String regex)</td><td>Splits this string around matches of the given regular expression.</td><td></td><td></td></tr><tr><td>split(String regex, int limit)</td><td>Splits this string around matches of the given regular expression.</td><td></td><td></td></tr><tr><td>substring(int beginIndex)</td><td>Returns a string that is a substring of this string.</td><td></td><td></td></tr><tr><td>substring(int beginIndex, int endIndex)</td><td>Returns a string that is a substring of this string.</td><td></td><td></td></tr><tr><td>toCharArray()</td><td>Converts this string to a new character array.</td><td></td><td>你可以最后再变回去String newStr = new String((array)， 这里array是一个char[] array（为了修改我必须如此，StringBuildler使用的概率小</td></tr><tr><td>toLowerCase()</td><td>Convert all of the characters in this String to lowercase using the rules of the default locale.</td><td></td><td></td></tr><tr><td>toString()</td><td>This object(which is already a string!)</td><td></td><td></td></tr><tr><td>toUppderCase()</td><td>Coverts all of the characters in this String to upper case using the rules of the default locale.</td><td></td><td></td></tr><tr><td>trim()</td><td>Return a string whose value is this string, with all leading and trailing space removed, where space is defined as any character whose codepoint is less than or equal to 'U+0020' (the space character).</td><td></td><td></td></tr><tr><td>repeat()</td><td>Returns a string whose value is the concatenation of this string repeated count times</td><td></td><td></td></tr><tr><td>String[] split(String regex)</td><td></td><td></td><td></td></tr><tr><td>String[] split(String regex, int limit)</td><td></td><td></td><td></td></tr><tr><td>startsWith(String prefix)</td><td>Check whether a string starts with the specified characters.</td><td></td><td></td></tr><tr><td>endsWith(String suffix)</td><td>Check whether a string ends with the specified characters.</td><td></td><td></td></tr><tr><td>intern()</td><td></td><td></td><td></td></tr></tbody></table>

## API 1: charAt() method



## API 2: compareTo() method

* lexicographically

## API 3: comparetToIgnoreCase() method



## API 4: String concat(String)作用等同于String做加法



## API 5: boolean equals(Object anObject)



## API 6: boolean equalsIgnoreCase(String anotherString)



## API 7: int indexOf(int ch)



## API 8: int indexOf(String str)





## API 9: int length()



## API 10: String replace(char oldChar, char newChar)





## API 11: deleteCharAt(int index)





## API 12: string replaceAll(String regex, String replacement)





## API 13: String substring(int beginIndex):\[index....]







## API 14: String substring(int beginIdnex, int endIndex) \[beginIndex, endIndex)



## API 15: char\[] toCharArray()





## API 16: String toLowerCase()



## API 17: String toUpperCase()



## API 18: String toString()



## API 19: String trim()



## API 20: repeat(int count)



## API 21: String\[] split(String regex)



## API 22: String\[] split(String regex, int limit)



## API 23 startsWith(String prefix)



## API 24 endsWith(String suffix)



## API 25 intern()





