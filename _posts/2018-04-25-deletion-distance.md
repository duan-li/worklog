---
layout: post
title: "Deletion Distance"
date: 2018-04-25 15:50 +1000
---
# Overview
The deletion distance of two strings is the minimum number of characters you need to delete in the two strings in order to get the same string. For instance, the deletion distance between `heat` and `hit` is `3`:

 - By deleting `e` and `a` in `heat`, and `i` in `hit`, we get the string `ht` in both cases.
 - We cannot get the same string from both strings by deleting `2` letters or fewer.
Given the strings `str1` and `str2`, write an efficient function `deletionDistance` that returns the deletion distance between them. Explain how your function works, and analyze its time and space complexities.

**Examples:**

```shell
input:  str1 = "dog", str2 = "frog"
output: 3

input:  str1 = "some", str2 = "some"
output: 0

input:  str1 = "some", str2 = "thing"
output: 9

input:  str1 = "", str2 = ""
output: 0
```

Constraints:

 - [input] string str1
 - [input] string str2
 - [output] integer

```php
function deletionDistance($str1, $str2) {
  // your code goes here
}

```

# Hints

* Recommend your peer to identify the base cases first. That is, cases where one of the strings is the empty string. In this case, the deletion distance is simply the length of the other string. After that, encourage them to try cases that are somewhat similar, such as one string containing `1` or `2` characters.
* If your peer needs additional assistance, help them by hinting toward a recursive relation between the `deletionDistance(str1, str2)`, and the `deletionDistance` for some prefixes of `str1` and `str2`. After they find the relation, you may suggest using Dynamic Programming.
 * If your peer is still stuck finding the recursive relation guide them to look at two cases:
  * Case 1: The last character in `str1` is equal to the last character in `str2`. In that case, one may assume that these two characters aren’t deleted, and look at the prefixes that don’t include the last character.
  * Case 2: The last character in `str1` is different from the last character in `str2`. In that case, at least one of the characters must be deleted, thus we get the following equation: `d(str1,str2) = 1 + min( d(str1.substring(0, n-1), str2), d(str1, str2.substring(0, m-1)) )` where `n` is the length of `str1`, `m` is the length of `str2`, and `d(x,y)` is the deletion distance between `x` and `y`.

# Solution
Let `str1Len` and `str2Len` be the lengths of `str1` and `str2`, respectively. Consider the function: `opt(i,j)` which returns the deletion distance for the `i'th` prefix of `str1`, and the `j'th` prefix of `str2`. What we want to do in this solution, is to use dynamic programming in order to build a function that calculates opt(str1Len, str2Len). Notice the following:

* `opt(0,j) = j and opt(i,0) = i`

This is true because if one string is the empty string, we have no choice but to delete all letters in the other string.

* If `i,j > 0` and `str1[i] ≠ str2[j]` then `opt(i,j) = 1 + min(opt(i-1, j), opt(i, j-1))`

This holds since we need to delete at least one of the letters `str1[i]` or `str2[j]` and the deletion of one of the letters is counted as `1` deletion (hence the `1` in the formula). Then, since we’re left with either the `(i-1)'th` prefix of str1, or the `(j-1)'th` prefix of `str2`, need to take the minimum between `opt(i-1,j)` and `opt(i,j-1)`. We, therefore, get the equation `opt(i,j) = 1 + min(opt(i-1,j), opt(i,j-1))`.

* If `i,j > 0` and `str1[i] = str2[j]`, then `opt(i,j) = opt(i-1, j-1)`

This holds since we don’t need to delete the last letters in order to get the same string, we simply use the same deletions we would to the `(i-1)'th` and `(j-1)'th` prefixes.

## Solution 1
After finding the relations above for `opt(i,j)`, we use dynamic programming methods to calculate `opt(str1Len, str2Len)`, i.e. the deletion distance for the two strings, by calculating `opt(i,j)` for all `0 ≤ i ≤ str1Len`, `0 ≤ j ≤ str2Len`, and saving previous values for later use:

**Pseudocode:**
```
function deletionDistance(str1, str2):
    str1Len = str1.length
    str2Len = str2.length
    
    # allocate a 2D array with str1Len + 1 rows and str2Len + 1 columns
    memo = new Array(str1Len + 1, str2Len + 1)

    for i from 0 to str1Len:
        for j from 0 to str2Len:
            if (i == 0):
                memo[i][j] = j
            else if (j == 0):
                memo[i][j] = i
            else if (str1[i-1] == str2[j-1]):
                memo[i][j] = memo[i-1][j-1]
            else:
                memo[i][j] = 1 + min(memo[i-1][j], memo[i][j-1])

    return memo[str1Len][str2Len]
```
**Time Complexity**: we have a nested loop that executes `O(1)` steps at every iteration, thus we the time complexity is `O(N⋅M)` where `N` and `M` are the lengths of `str1` and `str2`, respectively.

**Space Complexity**: we save every value of `opt(i,j)` in our `memo` 2D array, which takes O(N⋅M) space, where `N` and `M` are the lengths of `str1` and `str2`, respectively.

## Solution 2
The solution above takes `O(N⋅M)` space since we save all previous values, but notice that `opt(i,j)` requires only `opt(i-1,j)`, `opt(i,j-1)` and `opt(i-1,j-1)`. Thus, by iterating first through `0 ≤ i ≤ str1Len`, and then for every `i` calculating `0 ≤ j ≤ str2Len`, we need only to save the values for the current `i` and the last `i`. This will reduce the space needed for the function.

Pseudocode:
```
function deletionDistance(str1, str2):
    # make sure the length of str2 isn't
    # longer than the length of str1
    if (str1.length < str2.length)
        tmpStr = str1
        str1 = str2
        str2 = tmpStr

    str1Len = str1.length
    str2Len = str2.length
    prevMemo = new Array(str2Len  + 1)
    currMemo = new Array(str2Len  + 1)

    for i from 0 to str1Len:
        for j from 0 to str2Len:
            if (i == 0):
                currMemo[j] = j
            else if (j == 0):
                currMemo[j] = i
            else if (str1[i-1] == str2[j-1]):
                currMemo[j] = prevMemo[j-1]
            else:
                currMemo[j] = 1 + min(prevMemo[j], currMemo[j-1])

        prevMemo = currMemo
        currMemo = new Array(str2Len + 1);  
                                           
    return prevMemo[str2Len]
 ```
**Time Complexity**: the time complexity stays the same, i.e. `O(N⋅M)`, since we still run a nested loop with `N⋅M` iterations.

**Space Complexity**: `O(min(N,M))`, as we only need to hold two rows of the double array.


# Example Code

**PHP code**
```php
function deletionDistance($str1, $str2) {
	$cur = range(0, strlen($str1));
	$prev = [];
	for($i=0; $i<=strlen($str2); $i++){
		$prev[$i] = 0;
	}
	
	for($i=0; $i<strlen($str1);$i++){
		$cur = $cur;
		$prev = $prev;
		$cur[0] = $i + 1;
		for($j=0; $j<strlen($str2);$j++){
			$sub = $str1[$i] == $str2[$j] ? 0 : 2;
			$cur[$j+1] = min($prev[$j]+$sub, $cur[$j]+1, $prev[$j+1]+1);
		}
	}
	return $cur[count($cur)-1];
}
```

**Python code 1 (working)**

```python
def deletionDistance(s1, s2):
  cur = list(range(len(s2) + 1))
  prev = [0] * (len(s2) + 1)
  for i in range(len(s1)):
    cur, prev = prev, cur
    cur[0] = i + 1
    for j in range(len(s2)):
      # Substitution is same as two deletions
      sub = 0 if s1[i] == s2[j] else 2
      cur[j+1] = min(prev[j] + sub, cur[j] + 1, prev[j+1] + 1)
  return cur[-1]
```

**Python code 2 (not working)**
```python
def deletionDistance(s1, s2):
	m = [[0 for j in range(len(s2)+1)] for i in range(len(s1)+1)]
	for i in range(len(s1)+1):
    	for j in range(len(s2)+1):
	        if i == 0:
	            m[i][j] = sum(bytearray(s2[:j]))
	        elif j == 0:
	            m[i][j] = sum(bytearray(s1[:i]))
	        elif s1[i-1] == s2[j-1]:
	            m[i][j] = m[i-1][j-1]
	        else:
	            m[i][j] = ord(s1[i-1]) + ord(s2[j-1]) + min(m[i-1][j-1], m[i-1][j], m[i][j-1])
	return m[len(s1)][len(s2)]
```

**Python code 3 (not working)**

```python
def deletionDistance(s1, s2):
    m = [[0 for j in range(len(s2)+1)] for i in range(len(s1)+1)]
    for i in range(len(s1)+1):
        for j in range(len(s2)+1):
            if i == 0:
                m[i][j] = sum(bytearray(s2[:j]))
            elif j == 0:
                m[i][j] = sum(bytearray(s1[:i]))
            elif s1[i-1] == s2[j-1]:
                m[i][j] = m[i-1][j-1]
            else:
                s1del = ord(s1[i-1])
                s2del = ord(s2[j-1])
                s1s2del = s1del + s2del
                m[i][j] = min(m[i-1][j-1] + s1s2del, m[i-1][j] + s1del, m[i][j-1] + s2del)
    return m[len(s1)][len(s2)]
```

# Test case
**PHP**
```php
$testCase = [
	["", "", 0],
	["", "hit", 3],
	["neat", "", 4],
	["heat", "hit", 3],
	["hot", "not", 2],
	["some", "thing", 9],
	["abc", "adbc", 1],
	["awesome", "awesome", 0],
	["ab", "ba", 2],
];

foreach($testCase as $key=>$case) {
	$index = $key+1;
	if ($case[2] != deletionDistance($case[0], $case[1])) {
		echo "Test case #{$index} failed<br />\n";
	} else {
		echo "Test case #{$index} passed<br />\n";
	}
}
```

**Python**
```python
testCase = [
	["", "", 0],
	["", "hit", 3],
	["neat", "", 4],
	["heat", "hit", 3],
	["hot", "not", 2],
	["some", "thing", 9],
	["abc", "adbc", 1],
	["awesome", "awesome", 0],
	["ab", "ba", 2],
];
# print(testCase)

index = 1;
for case in testCase:
  if(case[2] != deletionDistance(case[0], case[1])):
    print('#' + str(index) + 'failed<br />\n');
  else:
    print('#' + str(index) + 'passed<br />\n');
  index+=1

```


https://stackoverflow.com/questions/44490091/deletion-distance-between-2-strings
https://stackoverflow.com/questions/41275345/deletion-distance-between-words