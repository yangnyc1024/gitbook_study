# Question 8 Valid Palindrome



* 非数字非字母需要忽略
  * !Character.isDigit(chars\[i]] && !Character.isLetter(chars\[i])
* 注意大小写case需要忽略
  * Character.toLowerCase(chars\[i]) == Character.toLowerCase(chars\[j])
