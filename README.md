# LeetCode - CheatSheet

A compilation of notes that I made when working with Leetcode problems - Note a majority of the content and code was taken off of 
the solution and discuss sections of the Leetcode website so I do not take any owenership of the below. The following is simply 
notes compiled for learning purposes.


## Getting Started

Currently LeetCode-CheatSheet contains various text files for notes but is primarily composed of this README file which supports 
the markdown formatting language. This makes the notes and code look a lot better and supports many awesome features like quick links 
and makes formatting much easier. 


### Prerequisites

In the future I might add a html document which also performs some formatting and if that comes out, ideally the html and css
would be written for web browsers on large screens which support the newest version of bootstrap and html 5.
I use the following application when building and testing html.

```
Chrome Version 71.0.3578.98
```


## Built With

* [Markdown](https://guides.github.com/features/mastering-markdown/) - Syntax styling



## Authors

* **Lichen Ma** - *compiling information* 



## Acknowledgments

* **Leetcode** - *content belongs to respective creators*


## Quick Access Links 
### LeetCode 
1. [Two Sum](#twoSum)
    1. [Brute force](#twoSumBruteForce)
    2. [One pass Hash Table](#twoSumOnePassHashTable) 
2. [Add Two Numbers](#addTwoNumbers)
    1. [Elementary Math Solution](#addTwoNumbersElementaryMath)
3. [Substring No Repeat](#substringNoRepeat)
    1. [Brute force](#substringNoRepeatBruteForce)
    2. [Sliding Window](#substringNoRepeatSlidingWindow)
    3. [Optimized Sliding Window](#substringNoRepeatOptimized)
4. [Median of Two Sorted Arrays](#medianofTwoSortedArrays)
    1. [Recursive Approach](#medianofTwoSortedArraysRecursiveApproach)
5. [Longest Palindromic Substring](#longestPalindromicSubstring)
    1. [Longest Common Substring](#longestPalindromicSubstringLongestCommonSubstring)
    2. [Brute Force](#longestPalindromicSubstringBruteForce)
    3. [Dynamic Programming](#longestPalindromicSubstringDynamicProgramming)
    4. [Expand Around Center](#longestPalindromicSubstringExpandAroundCenter)
    5. [Manacher's Algorithm](#longestPalindromicSubstringManacherAlgorithm)
6. [ZigZag Conversion](#zigZagConversion)
    1. [Sort by Row](#zigZagConversionSortbyRow)
    2. [Visit by Row](#zigZagConversionVisitbyRow)
7. [Reverse Integer](#reverseInteger)
    1. [Pop and Push Digits and Check Before Overflow](#reverseIntegerPopandPush)
8. [String to Integer](#stringtoInteger)
    1. [ASCII Conversion](#stringtoIntegerASCII)
9. [Palindrome Number](#palindromeNumber)
    1. [Revert Half of the Number](#palindromeNumberRevertHalf)
10. [Regular Expression Matching](#regularExpressionMatching)
    1. [Recursion](#regularExpressionMatchingRecursion)
    2. [Dynamic Programming](#regularExpressionMatchingDynamicProgramming)
    3. [Non - Recursive](#regularExpressionMatchingNonRecursive)
11. [Container With the Most Water](#containerwiththeMostWater)
    1. [Brute Force](#containerwiththeMostWaterBruteForce)
    2. [Two Pointer Approach](#containerwiththeMostWaterTwoPointer)
12. [Integer To Roman](#integertoRoman)
    1. [String Array](#integertoRomanStringArray)
13. [Roman To Integer](#romantoInteger)
    1. [Character Array](#romantoIntegerCharacterArray)
14. [Longest Common Prefix](#longestCommonPrefix)
    1. [Horizontal Scanning](#longestCommonPrefixHorizontalScanning)
    2. [Vertical Scanning](#longestCommonPrefixVerticalScanning)
    3. [Divide and Conquer](#longestCommonPrefixDivideandConquer)
    4. [Further Thoughts](#longestCommonPrefixFurtherThoughts)
15. [3Sum](#threeSum)
    1. [Sorted Array](#threeSumSortedArray)
16. [3Sum Closest](#threeSumClosest)
    1. [3 Pointers](#threeSumClosestThreePointers)
17. [Letter Combinations of a Phone Number](#letterCombinationsofaPhoneNumber) 
    1. [Backtracking](#letterCombinationsofaPhoneNumberBacktracking)
    2. [FIFO Queue](#letterCombinationsofaPhoneNumberFIFOQueue)
18. [4Sum](#fourSum)
    1. [Sorted Array](#fourSumSortedArray)
19. [Remove Nth Node From End of List](#removeNthNodefromEndofList)
    1. [Two Pass Algorithm](#removeNthNodefromEndofListTwoPassAlgorithm)
    2. [One Pass Algorithm](#removeNthNodefromEndofListOnePassAlgorithm)
20. [Valid Parentheses](#validParentheses)
    1. [Stack](#validParenthesesStack)

### Algorithms and Data Structures 
* [Trie](#trie)
    

<br><br><br><br><br>
***
<br><br><br>

<a name="twoSum"></a>
# 1-Two Sum 

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

<br><br>
<a name="twoSumBruteForce"></a>
## Brute Force 

```java 
public int[] twoSum(int[] nums, int target) {
	for (int i=0; i<nums.size; i++){
		for (int j=i+1;j<nums.length;j++){
			if (nums[j]==target-nums[i]){
				return new int[] {i,j};
			}
		}
	}
	throw new IllegalArgumentException("No two sum solution");
} 
```
**Complexity Analysis** 
```
* Time complexity:   O(n^2)       we have a nested loop 
* Space complexity:  O(1) 	  we do not allocate any additional memory
```
<a name="twoSumOnePassHashTable"></a>
## One Pass Hash Table 

```java 
public int[] twoSum(int[] nums, int target) {
	Map<Integer, Integer> map = new HashMap<>();
	for(int i=0; i<nums.length; i++){
		int complement=target-nums[i];
		if (map.containsKey(complement)){
			return new int[] {map.get(complement),i};
		}
		map.put(nums[i],i);
	}
	throw new IllegalArgumentException("No two sum solution"); 
}
```
**Complexity Analysis**
```
* Time complexity:   O(n)		each lookup in the hash table only requires O(1) time
* Space complexity:  O(n)		we require additional space for the hash table which stores at most n
```

<br><br><br>
***
<a name="addTwoNumbers"></a>
# 2-Add Two Numbers 

Given two non-empty linked lists representing two non-negative integers with the digits stored in 
reverse order and each node containing a single digit, add the two numbers and return as a linked list

Example: 
```
Input (2 -> 4 -> 3) + (5 -> 6 -> 4) 
Output 7 -> 0 -> 8 

342 + 465 = 807
```


<br><br>
<a name="addTwoNumbersElementaryMath"></a>
## Elementary Math Solution

```java 
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */



class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead= new ListNode(0); 
        ListNode p=l1, q=l2, curr=dummyHead; 
        int carry=0; 
        while (p!=null||q!=null){
            int x= (p!=null) ? p.val :0; //if (p!=null) then x contains p.val
            int y= (q!=null) ? q.val :0;
            int sum=carry+x+y;
            carry=sum/10;
            curr.next=new ListNode(sum%10);
            curr=curr.next; 
            if (p!=null) p=p.next; 
            if (q!=null) q=q.next; 
        }
        if (carry>0){
            curr.next= new ListNode(carry);
        }
        return dummyHead.next; 
    }
}
```

**Complexity analysis** 
```
* Time Complexity:  O(max(m,n))         depends on the lengths of the two linked lists 
* Space Complexity: O(max(m,n))		the maximum length of the new list is max(m,n)+1
```


<br><br><br>
***
<a name="substringNoRepeat"></a>
# 3-Substring No Repeat 

Longest Substring Without Repeating Characters 

Given a string find the length of the longest substring without repeating characters. 

```
Example
Input: 		"abcabcbb"
Output:		3
Explanation:	The answer is "abc", with the length of 3
```
```
Example 2
Input:		"bbbbb"
Output:		1
Explanation:	The answer is "b", with the length of 1
```
```
Example 3
Input:		"pwwkew"
Output:		3
Explanation: 	The answer is "wke", with the length of 3. Note that the answer must be a substring
		"pwke" is a subsequence and not a substring 
```

<br><br>
<a name="substringNoRepeatBruteForce"></a>
## Brute Force 

*Algorithm* 


Suppose we have a function "boolean allUnique(String substring)" which returns true if all the
characters in the substring are unique and false otherwise. We can iterate through all the possible 
substrings of the given string s and call the function allUnique. If it turns out to be true, then we 
update our answer of the maximum length of substring without duplicate characters. 

To enumerate all substrings of a given string we enumerate the start and end indices of them. Suppose
the start and end indices are i and j respectively. Then we have 0 <= i <= j <= n. Thus using two 
nested loops with i from 0 to n-1 and j from i+1 to n, we can enumerate all the substrings of s

To check if one string has duplicate characters we can use a set. We iterate through all the 
characters in the string and put them into the set one by one. Before putting one character, we check
if the set already contains it. If so we return false and after the loop we return true.


```java 
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j <= n; j++)
                if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
        return ans;
    }

    public boolean allUnique(String s, int start, int end) {
        Set<Character> set = new HashSet<>();
        for (int i = start; i < end; i++) {
            Character ch = s.charAt(i);
            if (set.contains(ch)) return false;
            set.add(ch);
        }
        return true;
    }
}
```

**Complexity Analysis** 

```
* Time Complexity:   O(n^3)		Verifying if characters in   [i,j) are unique requires us to scan all of
					them which would cost O(j-i) time. 

					For a given i, the sum of time costed by each j -> [i+1,n] is 
					"Summation from i+1 to n O(j-1)"

					Thus, the sum of all the time consumption is: 
					O(summation from 0 to n-1(summation from j=i+1 to n (j-1))) 
					O(summation from i=0 to n-1(1+n-i)(n-i)/2)) = O(n^3)


					*Note that the sum of all numbers up to n 1+2+3+...+n = n(n+1)/2


* Space Complexity:  O(min(n,m))	We require O(k) space for checking a substring has no duplicate 
					characters, where k is the size of the set. The size of the Set is 
					upper bounded by the size of the string n amd the size of the charset
					or alphabet m 
				
				
```

<br><br>
<a name="substringNoRepeatSlidingWindow"></a>
## Sliding Window 

A sliding window is an abstract concept commonly used in array/string problems. A window is a range of 
elements in the array/string which usually defined by the start and end indices
```
Ex. [i,j) left-closed, right-open
```
A sliding window is a window that slides its two boundaries in a certain direction, for example if we
slide \[i,j) to the right by 1 element, then it becomes \[i+1, j+1) - left closed, right open.



Sliding Window approach, whenever we are looking at a section on an array usual to perform calculations
we don't need to completely recalculate everything for every section of the array. Usually we can use
the value obtained from another section of the array to determine something about this section of the 
array. For example if we are calculating the sum of sections of an array we can use the previously 
calculated value of a section to determine the sum of an adjacent section in the array. 
```
Ex. 1 2 3 4 5 6 7 8 
```
If we calculate the first section of four values we get 1+2+3+4 = 10 , then to calculate the next section
2+3+4+5 we can just take our first section (window_sum) and perform the operation: 
```
window_sum-first entry + last entry = 10-1+5= 14
```
So essentially for the window sliding technique we use what we know about an existing window to 
determine properties for another window. 

<br><br>
*Algorithm*

In the brute force approach, we repeatedly check a substring to see if it has duplicate characters but
this is unnecessary. If a substring from index i to j-1 is already checked to have no duplicate 
characters we only need to check if s[j] is already in the substring. 

To check if a character is already in the substring we can scan the substring which leads to an O(n^2)
algorithm but we can improve on this runtime using a HashSet as a sliding window to check if a 
character exists in the current set O(1). 

We use a HashSet to store the characters in the current window \[i,j) and then we slide the index j to
the right, if it is not in the HashSet, we slide j further until s[j] is already in the HashSet. At
this point we found the maximum size of substrings without duplicate characters starting with index i.
If we do this for all i, then we obtain our answer. 


```java 
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> set = new HashSet<>();
        int ans = 0, i = 0, j = 0;
        while (i < n && j < n) {
            // try to extend the range [i, j]
            if (!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));
                ans = Math.max(ans, j - i);
            }
            else {
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
}
```

**Complexity Analysis**
```
Time complexity:	O(2n)=O(n)	Worst case each character will be visited twice by i and j

Space complexity: 	O(min(m,n))	Same as the brute force method, we need O(k) space for the 
					sliding window where k is the size of the set. The size of the
					set is bounded by the size of the string n and the size of the
					charset/alphabet m
```


<br><br>
<a name="substringNoRepeatOptimized"></a>
## Sliding Window Optimized 

The previously discussed sliding window approach requires at most 2n steps and this could in fact be
optimized even further to require only n steps. Instead of using a set to tell if a character exists or
not, we could define a mapping of the characters to its index. Then we can skip the characters 
immediately when we found a repeated character 

If s[j] has a duplicate in the range \[i , j) with index j', we don't need to increase i little be little
we can just skip all the elements in the range \[i , j'] and let i be j'+1 directly 

```java 
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```

<br><br><br>
***
<a name="medianofTwoSortedArrays"></a>
# 4-Median of Two Sorted Arrays 

There are two sorted arrays num1 and num2 of size m and n respectively. Find the median of the two 
sorted arrays. The overall run time complexity should be O(log (m+n)). You may assume nums1 and nums2
cannot be both empty. 

```
Example 

nums1 = [1, 3] 
nums2 = [2]

The median is 2.0
```

```
Example 2

nums1= [1, 2] 
nums2= [3, 4] 

The median is (2+3)/2 = 2.5
```


<br><br>
<a name="medianofTwoSortedArraysRecursiveApproach"></a>
## Recursive Approach

In statistics the median is used for dividing a set into two equal length subsets with one set being
always greater than the other set. To approach this problem first we cut A into two parts at a random
position i: 

```
         left_A                |           right_A 

  A[0], A[1], ... , A[i-1]         A[i], A[i+1], ... , A[m-1]
```

Since A has m elements, there are m+1 kinds of cutting as i can range from 0-m. We can also see that
left_A is empty when i is zero and right_A is empty when i=m

```
len(left_A) = i and len(right_A)= m-i
```

We can similarly cut B into two parts at a random position j: 

```
	left_B			|	right_B

  B[0], B[1], ... , B[j-1]	   B[j], B[j+1], ... , B[n-1]
```
  
Now if we put left_A and left_B into one set and put right_A and right_B into another set and name 
them left_part and right_part, then we get

```
	left_part		|	right_part
  A[0], A[1], ... , A[i-1]	  A[i], A[i+1], ... , A[m-1]
  B[0], B[1], ... , B[j-1]	  B[j], B[j+1], ... , B[n-1]
```

If we can ensure that 
1. the len(left_part) = len(right_part)
2. max(left_part) <= min(right_part)

then we divide all the elements in {A,B} into two parts with equal length and one part is always
greater than the other. Then 

```
median= (max(left_part)+min(right_part))/2
```
To ensure these two conditions, we need to ensure: 
1. i+j= m-i+n-j (or: m-i+n-j+1) if n>m, we just need to set i=0~m, j= (m+n+1)/2 - i
2. B\[j-1]<=A\[i] and A\[i-1]<=B\[j]

So, all we need to do is search for i in \[0,m] to find an object i such that 
B\[j-1]<=A\[i] and A\[i-1]<=B\[j] where j=(m+n+1)/2 -i

Then we perform a binary search following the steps described below: 

1) Set imin=0, imax=0, then start searching in \[imin, imax]
2) Set i=(imin+imax)/2 , j=(m+n+1)/2 - i
3) Now we have len(left_part) = len(right_part) and there are only 3 more situations which we may 
   encounter: 
   
```
   - B[j-1] <= A[i] and A[i-1]<=B[j] 
     This means that we have found the object i, so we can stop searching

   - B[j-1] > A[i]
     Means A[i] is too small, we must adjust i to get B[j-1]<=A[i] so we increase i because this will
     cuase j to be decreased. We cannot decrease i because when i is decreased, j will be increased
     so B[j-1] is increased and A[i] is decreased (B[j-1]<= A[i] will never be satisfied)

   - A[i-1] > B[j] 
     Means A[i-1] is too big and thus we must decrease i to get A[i-1]<=B[j]. In order to do that we 
     must adjust the searching range to [imin, i-1] so we set imax=i-1 and go back to step 2
```
When the object i is found, then the media is: 

 max(A\[i-1],B\[j-1]), when m+n is odd
(max(A\[i-1],B\[j-1])+min(A\[i],B\[j]))/2, when m+n is even

Next is to consider the edge values i=0, i=m, j=0, j=n where A\[i-1], B\[j-1], A\[i], B\[j] may not exist

```java 
class Solution {
	public double findMedianSortedArrays(int[] A, int[] B) {
		int m=A.length;
		int n=B.length;
		if (m>n) {   	//ensuring that m<=n
			int[] temp=A; A=B; B=temp;
			int tmp=m; m=n; n=tmp;
		}
		int iMin=0, iMax=m, halfLen=(m+n+1)/2;
		while (iMin<=iMax) {
			int i=(iMin+iMax)/2
			int j= halfLen - i;
			if (i<iMax && B[j-1] > A[i]){
				iMin=i+1; //i is too small
			}
			else if (i>iMin && A[i-1]>B[j]) {
				iMax=i-1; //i is too big
			}
			else{ //we have found the object i 
				int maxLeft=0; 
				if (i==0) {
					maxLeft=B[j-1];
				}
				else if (j==0){
					maxLeft=A[i-1];
				}
				else{
					maxLeft=Math.max(A[i-1], B[j-1]);
				}

				if ((m+n)%2 ==1) {
					return maxLeft;
				}

				int minRIght=0;
				if (i==m) {
					minRight=B[j];
				}
				else if (j==n) {
					minRight=A[i];
				}
				else {
					minRight=Math.min(B[j], A[i]);
				}

				return (maxLeft+minRight)/2.0;
			}
		}
		return 0.0;
	}
}
```

**Complexity Analysis**

```
Time Complexity: O(log(min(m,n)))	At first the searching range is [0,m] and the length of this 
					searching range will be reduced by half after each loop so we
					only need log(m) loops. Since we do constant operations in 
					each loop the time complexity is O(log(m) and since m<=n the
					time complexity is O(log(min(m,n))

Space Complexity: O(1)			We only need constant memory to store 9 local variables so the
					space complexity is O(1)
```


<br><br><br>
***
<a name="longestPalindromicSubstring"></a>
# 5-Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length
of s is 1000. 

```
Example 1: 

Input: "babad" 
Output: "bab" 

Note: "aba" is also a valid answer 
```

```
Example 2: 

Input: "cbbd"
Output: "bb" 
```

<br><br>
<a name="longestPalindromicSubstringLongestCommonSubstring"></a>
## Longest Common Substring

Some people will be tempted to come up with this quick solution which is unforunately flawed, "reverse
S and become S'. Find the longest common substring between S and S' and that will be the longest
palindromic substring." This will work with some examples but there are some cases where the longest
common substring is not a valid palindrome. 

	Ex. S="abacdfgdcaba", S'="abacdgfdcaba" 	

	The longest common substring between S and S' is "abacd" and clearly this is not a valid 
	palindrome

We can solve this problem however by checking if the substring's indices are the same as the reversed
substring's original indices each time we find a longest common substring. If it is, then we attempt
to update the longest palindrome found so far, if not we skip this and find the next candidate

**Complexity Analysis**
```
Time Complexity: O(n^2) 
Space Complexity: O(n^2) 
```
<br><br>
<a name="longestPalindromicSubstringBruteForce"></a>
## Brute Force 

The obvious brute force solution is to pick all possible starting and ending position for a substring 
and verify if it is a palindrome 

**Complexity Analysis**
```
Time Complexity: O(n^3)		If n is the length of the input string, there are a total of 
				(n 2) = n(n-1)/2 substrings and since verifying each substring takes 
				O(n) time, the run time complexity is O(n^3)

Space Complexity: O(1) 
```
<br><br>
<a name="longestPalindromicSubstringDynamicProgramming"></a>
## Dynamic Programming 

We can improve on the brute force solution by avoid some unnecessary re-computation while validating 
palidromes. Consider the word "ababa", if we already know that "bab" is a palindrome then we can 
determine that ababa is a palindrome by noticing that the two left and right letters connected to bab
are the same. 

This yields a straight forward dynamic programming solution where we initialize the one and two letters
palindromes and then work our way up finding all three letters palindromes and so on.

**Complexity Analysis**
```
Time Complexity: 	O(n^2)	

Space Complexity: 	O(n^2)	Using O(n^2) space to store the table 
```
<br><br>
<a name="longestPalindromicSubstringExpandAroundCenter"></a>
## Expand Around Center

This approach allows us to solve this problem in O(n^2) time using only constant space complexity. We
observe that a palindrome mirrors around its enter and therefore a palindrome can be expanded from its
center and there are only 2n-1 such centers (for palindromes with an even number of letters like 
"abba" its center is in between two letters).

```java 
public String longestPalindrome(String s) {
	if (s==null || s.length() < 1) return "";     //edge case 
	int start=0, end=0;
	for (int i=0; i<s.length(); i++) {
		int len1=expandAroundCenter(s,i,i);
		int len2=expandAroundCenter(s,i,i+1);
		int len=Math.max(len1,len2);
		if (len>end-start) {
			start= i-(len-1)/2;
			end=i+len/2
		}
	}
	return s.substring(start,end+1);
}

private int expandAroundCenter(String s, int left, int right) {
	int L=left, R=right;
	while(L>=0 && R<s.length() && s.charAt(L)==s.charAt(R)) {
		L--;
		R++;
	}
	return R-L-1;
}
```

<br><br>
<a name="longestPalindromicSubstringManacherAlgorithm"></a>
## Manacher's Algorithm 

There is an O(n) algorithm called Manacher's algorithm, however, it is a non-trivial algorithm and no 
one would expect you to come up with this algorithm in a 45 minute coding session


<br><br><br>
***
<a name="zigZagConversion"></a>
# 6-ZigZag Conversion 

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: 
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR". Write a code that will take a string and make this 
conversion given a number of rows: 

```
string convert(string s, int numRows);
```

```
Example 1: 

Input: s="PAYPALISHIRING", numRows=3
Output: "PAHNAPLSIIGYIR"
```

```
Example 2:

Input: s="PAYPALISHIRING", numRows=4
Output: "PINALSIGYAHRPI"

Explanation:

P           I          N
A       L   S      I   G
Y   A       H   R
P           I
```

<br><br>
<a name="zigZagConversionSortbyRow"></a>
## Sort by Row 

By iterating through the string from left to right we can easily determine which row in the Zig-Zag
pattern that a character belongs to

<br><br>
*Algorithm*

We can use min(numRows,len(s)) lists to represent the non-empty rows of the Zig-Zag Pattern. 
Iterate through s from left to right appending each character to the appropriate row. The appropriate
row can be tracked using two variables: the current row and the current direction. 

The current direction only changes when we moved to the topmost row or moved down to the bottommost 
row 

```java
class Solution {
	public String convert(String s, int numRows) {
		if (numRows==1) return s;		//if there is only one row return string

		List<StringBuilder> rows=new ArrayList<>();
		for (int i=0; i<Math.min(numRows, s.length()); i++){
			rows.add(new StringBuilder());
		}
		int curRow=0;
		boolean goingDown=false;

		for(char c: s.toCharArray()) {
			rows.get(curRow).append(c);
			if (curRow==0 || curRow==numRows-1) {
				goingDown=!goingDown;
			}
			curRow+=goingDown ? 1 : -1;
		}	

		StringBuilder ret= new StringBuilder();
		for(StringBuilder row:rows) {
			ret.append(row);
		}
		return ret.toString();
	}
}
```

**Complexity Analysis**

```
Time Complexity:  O(n)	where n==len(s)
Space Complexity: O(n)
```

<br><br>
<a name="zigZagConversionVisitbyRow"></a>
## Visit by Row

Visit the characters in the same order as reading the Zig-Zag pattern line by line

<br><br>
*Algorithm*

Visit all characters in row 0 first, then row 1, then row 2, and so on.
For all whole numbers k, 
	* characters in row 0 are located at indexes  k\*(2\*numRows-2)
	* characters in row numRows -1 are located at indexes  k\*(2\*numRows-2)+ numRows -1 
	* characters in inner row i are located at indexes  k\*(2\*numRows-2)+i and (k+1)(2\*numRows-2)-i

```java
class Solution {
	public String convert(String s, int numRows) {
		if (numRows==1) return s; 

		StringBuilder ret=new StringBuilder();
		int n=s.length();
		int cycleLen= 2* numRows -2;

		for (int i=0; i<numRows; i++) {
			for (int j=0; j+1<n; j+= cycleLen) {
				ret.append(s.charAt(j+i));
				if (i!=0 && i!=numROws-1 && j+cycleLen-i<n) {
					ret.append(s.charAt(j+cycleLen-i));
				}
			}
			return ret.toString();
		}
	}
}
```

**Complexity Analysis**
```
Time Complexity: O(n)	where n==len(s) Each index is visited once

Space Complexity: O(n) 	C++ implementation can achieve O(1) if the return string is not considered 
			extra space
```


<br><br><br>
***
<a name="reverseInteger"></a>
# 7-Reverse Integer 

Given a 32- bit signed integer, reverse digits of an integer. 

```
Example 1: 

Input: 123
Output: 321
```

```
Example 2: 

Input: -123
Output: -321
```

```
Example 3: 

Input: 120 
Output: 21
```

For the purpose of this problem assume that your function returns 0 when the reversed integer overflows

<br><br>
<a name="reverseIntegerPopandPush"></a>
## Pop and Push Digits and Check Before Overflow 

We can build up the reverse integer one digit at and time and before doing so we can check whether or
not appedning another digit would cause overflow 

<br><br>
*Algorithm*

Reversing an integer can be done similarly to reversing a string. We want to repeatedly "pop" the last
digit off of x and push it to the back of the rev so that in the end rev is the reverse of x. 

To push and pop digits without the help of some auxiliar stack/array we can use math 

```
//pop operation: 
pop = x%10; 
x/=10;

//push operation:
temp=rev*10+pop;
rev =temp;
```

This statement is dangerous however as the statement temp=rev\*10+pop may cause an overflow and luckily
it is easy to check beforehand whether or not this statement would cause an overflow. 

1. If temp=rev\*10+pop causes an overflow, then rev>=INTMAX/10
2. If rev> INTMAX/10, then temp=rev\*10+pop is guaranteed to overflow
3. if rev==INTMAX/10, then temp=rev\*10 + pop will overflow if an only if pop>7

```java
class Solution {
	public int reverse(int x) {
		int rev=0; 
		while (x!=0) {
			int pop=x%10;
			x/=10;
			if (rev>Integer.MAX_VALUE/10||(rev==Integer.MAX_VALUE/10 && pop>7)) return 0;
			if (rev<Integer.MIN_VALUE/10||(rev==Integer.MIN_VALUE/10 && pop<-8)) return 0;
			rev=rev*10 +pop;
		}
		return rev;
	}
}
```

**Complexity Analysis**
```
Time Complexity:  O(log(x))	There are roughly log10(x) digits in x 
Space Complexity: O(1)
```


<br><br><br>
***
<a name="stringtoInteger"></a>
# 8-String to Integer (atoi)

Implement atoi which converts a string to an integer 

The function first discards as many whitespace characters as necessary until the first non-whitespace
character is found. Then, starting from this character, takes an optional initial plus or minus sign
followed by as many numerical digits as possible and interprets them as a numerical value. 

The string can contain additional characters after those that form the integral number, which are 
ignored and have no effect on the behavior of this function. 

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such
sequence exits because either str is empty or it contains only whitespace characters, no conversion is
performed. 

If no valid conversion could be performed a zero value is returned 

Note: 
* only the space character ' ' is considered as whitespace character 
* assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [-2^31, 2^31-1]. If the numerical value is out of the range of representable values, INT_MAX (2^31-1) or INT_MIN (-2^31) is returned

```
	Example 1: 

	Input: "42"
	Output: 42
```

```
	Example 2: 

	Input: "      -42" 
	Output: -42
```

```
	Example 3:

	Input: "4193 with words "
	Output: 4193
```

```
	Example 4: 
	
	Input: "words and 987"
	Output: 0
```

```
	Example 5:
	
	Input: "-91283472332"
	Output: -2147483648 	//out of the range of a 32-bit signed integer so INT_MIN is returned
```


<br><br>
<a name="stringtoIntegerASCII"></a>
## ASCII Conversion

Recognize that ASCII characters are actually numbers and 0-9 digits are numbers starting from decimal
48 (0x30 hexadecimal) 

```
	'0' is 48
	'1' is 49
	...
	'9' is 57
```
So to get the value of any character digit you can just remove the '0' 

```
	'1' - '0' => 1
	49  -  48 => 1
```

```java
public int myAtoi(String str) {
	int index=0, sign=1, total=0;
	
	//1. Empty string 
	if (str.length() ==0) return 0;

	//2. Remove Spaces 
	while(str.charAt(index)==' ' && index < str.length())
		index++;
	
	//3. Handle signs 
	if (str.charAt(index)=='+' || str.charAt(index)=='-'){
		sign= str.charAt(index) == '+' ? 1:-1;
		index++;
	}

	//4. COnvert number and avoid overflow
	while(index<str.length()){
		int digit= str.charAt(index) - '0'; 
		if (digit<0||digit>9) break;

		//check if total will overflow after 10 times and add digit
		if (Integer.MAX_VALUE/10 < total || Integer.MAX_VALUE/10 == total 
		    && Integer.MAX_VALUE%10<digit) {    
		    return sign==1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
		}
		total= 10* total+digit;
		index++;
	}
	return total*sign;
}
```


<br><br><br>
***
<a name="palindromeNumber"></a>
# 9-Palindrome Number


Determines whether an interger is a palindrome. An integer is a palindrome when it reads the same 
backward as forward. 

```
Example 1: 

Input: 121
Output: true
```

```
Example 2: 

Input: -121
Output: false 
Explanation: 	From left to right, it reads -121, meanwhile from right to left it becomes 121- . 
		Therefore it is not a palindrome
```

```
Example 3: 

Input: 10 
Output: false 
Explanation: 	Reads 01 from right to left. Therefore it is not a palindrome
```


<br><br>
<a name="palindromeNumberRevertHalf"></a>
## Revert Half of the Number

A first idea which may come to mind is to convert the number into a string and check if the string is a
palindrome but this would require extra non-constant space for creating the string not allowed by the 
problem description 

Second idea would be reverting the number itself and comparing the number with the original number, if
they are the same then the number is a palindrome, however if the reversed number is larger than 
int.MAX we will hit integer overflow problem. 

To avoid the overflow issue of the reverted number, what if we only revert half of the int number? The
reverse of the last half of the palindrome should be the same as the first half of the number if the 
number is a palindrome. 

If the input is 1221, if we can revert the last part of the number "1221" from "21" to "12" and compare
it with the first half of the number "12", since 12 is the same as 12, we know that the number is a 
palindrome. 

<br><br>
*Algorithm* 

At the very beginning we can deal with some edge cases. All negative numbers are not palindrome and 
numbers ending in zero can only be a palindrome if the first digit is also 0 (only 0 satisfies this 
property) 

Now let's think about how to revert the last half of the number. For the number 1221 if we do 1221%10 
we get the last digit 1. To get the second last digit we divide the number by 10 1221/10=122 and then
we can get the last digit again by doing a modulus by 10, 122%10=2. If we multiply the last digit by 
10 and add the second last digit 1\*10+2=12 which gives us the reverted number we want. COntinuing this
process would give us the reverted number with more digits. 

Next is how do we know that we've reached the half of the number? 
Since we divided the number by 10 and multiplied the reversed number by 10 when the original number is
less than the reversed number, it means we've gone through half of the number digits. 

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x<0 || (x%10==0 && x!=0)) {
            return false;
        }
        
        int revertedNumber=0;
        while (x>revertedNumber){
            revertedNumber=x%10+revertedNumber*10;
            x/=10;
        }
        //when the length is an odd number, we can get rid of the middle digit by 
        //revertedNumber/10
        
        //For example when the input is 12321, at the end of the while loop we get x=12, 
        //revertedNumber=123, since the middle digit doesn't matter in a palindrome we can
        //simply get rid of it 
        
        return x==revertedNumber||x==revertedNumber/10;
    }
}
```


<br><br><br>
***
<a name="regularExpressionMatching"></a>
# 10-Regular Expression Matching

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.'
and '*'

```
	'.' Matches any single character
	'*' Matches zero or more of the preceding element 
```
The matching should cover the entire input string (not partial) 

Note: 
* s could be empty and contains only lower case letters a-z
* p could be empty and contains only lower case letters a-z and characters like . or * 

```
Example 1: 

Input:
	s="aa" 
	p="a" 
	Output: false 
	Explanation: 	"a" does not match the entire string "aa" 
```

```
Example 2: 

Input: 
	s="aa"
	p="a*" 
	Output: true 
	Explanation: 	'*' means zero of more of the preceding element, 'a'. Therefore, by repeating
			'a' once it becomes "aa"
```

```
Example 3: 

Input: 
	s="ab" 
	p=".*" 
	Output: true 
	Explanation: 	'.*' means "zero or more (*) of any character (.)"
```

```
Example 4: 

Input: 
	s="aab" 
	p="c*a*b" 
	Output: true
	Explanation: 	c can be repeated 0 times, a can be repeated 1 time. Therefore it matches 
			"aab" 
```

```
Example 5: 

Input: 
	s="mississippi" 
	p="mis*is*p*."
	Output: false 
```

<br><br>
<a name="regularExpressionMatchingRecursion"></a>
## Recursion

If there were no Kleene stars (the * wildcard characters for regular expressions), the problem would 
be easier- we simply check from left to right if each character of the text matches the pattern. When
a star is present we may need to check for may different suffixes of the text and see if they match
the rest of the pattern. A recursive solution is a straightforward way to represent this relationship

```java
class Solution {
	public boolean isMatch(String text, String pattern) {
		if (pattern.isEmpty()) return text.isEmpty(); 
		
		boolean first_match=(!text.isEmpty() && 
				    (pattern.charAt(0)==text.charAt(0) || pattern.charAt(0)=='.'));

		if (pattern.length()>=2 && pattern.charAt(1) =='*'){
			return (isMatch(text,pattern.substring(2))||
			       (first_match && isMatch(text.substring(1),pattern)));
		
		//note: pattern.substring(2) returns all of the characters after index 2 of pattern
		}
		else {
			return first_match && isMatch(text.substring(1), pattern.substring(1));
		}
		
	}
}
```

**Complexity Analysis**

```
Time Complexity: 	Let T, P be the lengths of the text and the pattern respectively. In the worst
			case, a call to match(text[i:],pattern[2j:]) will be made (i+j i) times, and 
			strings of the order O(T-i) and O(P-2*j) will be made. Thus the complexity has
			the order: 

			summation from i=0 to T * summation from j=0 to P/2 * (i+j i) O(T+P-i-2j).

			We can show that this is bounded by O((T+P)2^(T+P/2))

Space Complexity:	For every call to match, we will create those strings as described above 
			possibly creating duplicates. If memory is not freed, this will also take a
			total of O((T+P)2^(T+P/2)) space even though there are only order O(T^2+P^2) 
			unique suffixes of P and T that are actually required 
```

<br><br>
<a name="regularExpressionMatchingDynamicProgramming"></a>
## Dynamic Programming

As the problem has an optimal substructure, it is natural to cache intermediate results. We ask the 
question dp(i,j): does text[i:] and pattern[j:] match? We can describe our answer in terms of answers
to questions involving smaller strings

<br><br>
*Algorithm* 

We proceed with the same recursion as in Approach 1, except because calls will only ever be made to 
match(text[i:], pattern[j:]), we use dp(i,j) to handle those calls instead, saving us expensive 
string-building operations and allowing us to cache the intermediate results 


**Java Top-Down Variation**

```java
enum Result {
	TRUE, FALSE
	
}

class Solution {
	Result[][] memo; 

	public boolean isMatch(String text, String pattern) { 
		memo=new Result[text.length() +1][pattern.length() +1];
		return dp(0,0,text,pattern);
	}

	public boolean dp(int i, int j, String text, String pattern) {
		if (memo[i][j]!=null) {
			return memo[i][j]==Result.TRUE;
		}
		boolean ans; 
		if (j==pattern.length()){
			ans=i==text.length();
		}
		else {
			boolean first_match=(i<text.length() && (pattern.charAt(j) == text.charAt(i) ||
					     patter.charAt(j) == '.'));

			if (j+1<pattern.length() && pattern.charAt(j+1)=='*'){
				ans=(dp(i,j+1,text,pattern)||first_match&& dp(i+1,j,text,pattern));
			}
			else {
				ans=first_match && dp(i+1, j+1, text, pattern); 
			}
		}
		memo[i][j]=ans? Result.TRUE: Result.FALSE; 
		return ans; 
	}
}
```

**Complexity Analysis**

```
Time Complexity: 	Let T, P be the lengths of the text and the pattern respectively. The work 
			for every call to dp(i,j) for i=0,...,T; j=0,...,P is done once and it is O(1) 				work. Hence the time complexity is O(TP)

Space Complexity:	The only memory we use is the O(TP) boolean entries in our cache. Hence, the 
			space complexity is O(TP) 
```

<br><br>
<a name="regularExpressionMatchingNonRecursive"></a>
## Non-Recursive

The recursive programming solutions are pretty confusing so this implementation uses 2D arrays and 
Dynamic Programming 


The logic works as follows: 
```
1. If p.charAt(j) == s.charAt(i) : dp[i][j] = dp[i-1][j-1]; 
2. If p.charAt(j) == '.' : dp[i][j] = dp[i-1][j-1]; 
3. If p.charAt(j) == '*': 
	
	Subconditions
	1. If p.charAt(j-1)!= s.charAt(i):dp[i][j]=dp[i][j-2]  	//in this case a* only counts as empty
	2. If p.charAt(i-1)== s.charAt(i) or p.charAt(i-1) == '.': 
		
		dp[i][j] = dp[i-1][j]	//in this case a* counts as multiple a 
	     or dp[i][j] = dp[i][j-1]	//in this case a* counts as single a 
	     or dp[i][j] = dp[i][j-2]	//in this case a* counts as empty 
```

```java
public boolean isMatch(String s, String p) {
	if (s==null || p==null){
		return false;
	}
	boolean[][] dp=new boolean[s.length()+1][p.length()+1];
	dp[0][0]=true; 
	for (int i=0;i<p.length(); i++){
		if (p.charAt(i)=='*' && dp[0][i-1]){
			dp[0][i+1]=true; 
		}
	}
	for (int i=0;i<s.length();i++){
		for (int j=0;j<p.length();j++){
			if (p.charAt(j)=='.'){
				dp[i+1][j+1]=dp[i][j];
			}
			if (p.charAt(j)==s.charAt(i)){
				dp[i+1][j+1]=dp[i][j];
			}
			if (p.charAt(j)=='*'){
				if (p.charAt(j-1)!=s.charAt(i) && p.charAt(j-1) !='.'){
					dp[i+1][j+1]=dp[i+1][j-1];
				}
				else{
					dp[i+1][j+1]=(dp[i+1][j] || dp[i][j+1] || dp[i+1][j-1]);
				}
			}
		}
	}
	return dp[s.length()][p.length()];
}
```


<br><br><br>
***
<a name="containerwiththeMostWater"></a>
# 11-Container with the Most Water 

Given n non negative integers a1,a2, ... , an where each represents a point at coordinate (i, ai). n 
vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two 
lines, which together with x-axis forns a container such that the container contains the most water. 

```Example: The array [1,8,6,2,5,4,8,3,7] would have a max area of water which is 49. 

		      ^		    ^
	 These two values form the container which could hold water at a max height of 7, these values
	 are also 7 array indexes apart from each other so it could hold water at a max width of 7. The
	 area of water which could be held is thus 7 x 7 = 49
```


<a name="containerwiththeMostWaterBruteForce"></a>
## Brute Force

In this case we simply consider the area for every possible pair of the lines and find out the maximum
area out of those. 

```
public class Solution {
	public int maxArea(int[] height) {
		int maxarea=0; 
		for (int i=0; i<height.length; i++){
			for (int j=i+1;j<height.length;j++){
				maxarea=Math.max(maxarea, Math.min(height[i],height[j])*(j-i));
			}
		}
		return maxarea;
	}
}
```

**Complexity Analysis**
```
Time complexity: 	O(n^2) 	Calculating the area for all n(n-1)/2 height pairs 
Space complexity: 	O(1) 	Constant extra space is used 
```

<br><br>
<a name="containerwiththeMostWaterTwoPointer"></a>
## Two Pointer Approach

The intuition behind this approach is that the area formed between the lines will always be limited by 
the height of the shorter line. Further, the farther the lines, the more will be the area obtained. 

We take two pointers, one at the beginning and one at the end of the array constituting the length of 
the lines. Further, we maintain a variable maxarea to store the maximum area obtained till now. At 
every step, we find out the area formed between them, update maxarea and move the pointer pointing to 
the shorter line towards the other end by one step. 

Initially we consider the area constituting the exterior most lines. Now to maximize the area we need
to consider the area between the lines of larger lengths. If we try to move the pointer at the longer
line inwards, we won't gain any increase in area, since it is limited by the shorter line. But moving
the shorter line's pointer could turn out to be benefical, as per the same argument, despite the 
reduction in width. This is done since a relatively longer line obtained by moving the shorter line's 
pointer might overcome the reduction in area caused by the width reduction. 

```java
public class Solution {
	public int maxArea(int[] height) {
		int maxarea=0, l=0, r=height.length-1; 
		while (l<r){
			maxarea=Math.max(maxarea,Math.min(height[l],height[r])*(r-l));
			if (height[l]<height[r]){
				l++;
			}
			else{
				r--;
			}
		}
		return maxarea; 
	}
}
```

**Complexity Analysis**
```
Time complexity: 	O(n) 	Single pass
Space complexity: 	O(1) 	Constant space is used 
```

<br><br><br>
***
<a name="integertoRoman"></a>
# 12-Integer To Roman 

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M
```
Symbol		Value 
I		1
V		5
X		10
L		50
C		100
D		500
M		1000
```

For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as
XII which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II. 

Roman numerals are usually written largest to smallest from left to right. However, the numeral for 
four is not IIII. Instead, the number four is written as IV. Because the one is before the five we 
subtract it making four. The same principle applies to the number nine which is written as IX. There 
are six instances where subtraction is used: 

* I can be placed before V (5) and X (10) to make 4 and 9 
* X can be placed before L (50) and C(100) to make 40 and 90 
* C can be placed before D (500) and M(1000) to make 400 and 900

Given an integer, convert it to a roman numeral, input is guaranteed to be within the range from 
1 to 3999

```
Example 1: 

Input: 3 
Output: "III" 
```

```
Example 2: 

Input: 4
Output: "IV" 
```

```
Example 3: 

Input: 9 
Output: "IX" 
```

```
Example 4: 

Input: 58 
Output: "LVIII" 
Explanation: L=50, V=5, III=3
```

```
Example 5: 

Input: 1994
Output: "MCMXCIV"
Explanation: M=1000, CM=900, XC=90 and IV=4 
```

<a name="integertoRomanStringArray"></a>
## String Array

```java
public static String intToRoman(int num) { 
	
	String M[]={"", "M", "MM", "MMM"};
	//represents 1000, 2000, and 3000 since we know the number is in the range 1 to 3999
	
	String C[]={"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
	//represents 0, 100,  200,   300,  400, 500,  600,   700,    800,  900

	String X[]={"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
	//represents 0,  10,   20,    30,   40,  50,   60,    70,     80,   90

	String I[]={"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"}; 
	//represents 0,   1,    2,     3,    4,  5,    6,     7,      8,    9

	return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10]; 
} 
```

<br><br><br>
***
<a name="romantoInteger"></a>
# 13-Roman to Integer

Roman numerals are represented by seven different symbols I, V, X, L, C, D and M 
```
Symbol 		Value 
I		1
V		5
X		10 
L		50
C		100
D		500
M		1000
```

For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as
XII which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II. 

Roman numerals are usually written largest to smallest from left to right. However, the numeral for 
four is not IIII. Instead, the number four is written as IV. Because the one is before the five we 
subtract it making four. The same principle applies to the number nine which is written as IX. There 
are six instances where subtraction is used: 

* I can be placed before V (5) and X (10) to make 4 and 9 
* X can be placed before L (50) and C(100) to make 40 and 90 
* C can be placed before D (500) and M(1000) to make 400 and 900

Given an integer, convert it to a roman numeral, Input is guaranteed to be within the range from 
1 to 3999

```
Example 1: 
	
Input: "III" 
Output: 3 
```

```
Example 2: 

Input: "IV" 
Output: 4
```

```
Example 3: 

Input: "IX" 
Output: 9 
```

```
Example 4: 

Input: "LVIII" 
Output: 58 
Explanation: L=50, V=5, III=3
```

```
Example 5: 

Input: "MCMXCIV" 
Output: 1994
Explanation: M=1000, CM=900, XC=90 and IV=4
```
<br><br>
<a name="romantoIntegerCharacterArray"></a>
## Character Array

```java
class Solution {
	public int romanToInt(String s) {
		Map<Character, Integer> map = new HashMap(); 
		map.put('I', 1); 
		map.put('V', 5); 
		map.put('X', 10); 
		map.put('L', 50); 
		map.put('C', 100); 
		map.put('D', 500); 
		map.put('M', 1000); 

		char[] sc= s.toCharArray(); 
		int total= map.get(sc[0]); 
		int pre=map.get(sc[0]); 
		for (int i=1; i<sc.length; i++) {
			int curr=map.get(sc[i]); 
			if (curr<=pre) {
				total= total + curr; 
			}
			else {
				total=total+curr -2*pre; 
			}
			pre=curr; 
		}
		return total; 
	}

}
```

<br><br><br>
***
<a name="longestCommonPrefix"></a>
# 14-Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings. If there is no 
common prefix, return an empty string ""

```
Example 1: 

Input: ["flower", "flow", "flight"]
Output: "fl"
```

```
Example 2: 

Input: ["dog", "racecar", "car"] 
Output: ""

Explanation: There is no common prefix among the input strings 
```

*Note:* 
All given inputs are in lowercase letters a-z

<br><br>
<a name="longestCommonPrefixHorizontalScanning"></a>
## Horizontal Scanning

<br>
*Intuition:* 

For a start we will describe a simple way of find the longest prefix shared by a set of strings 
LCP(S1 ... Sn).We will use the observation that: 
```
LCP(S1 ... Sn) = LCP(LCP(LCP(S1, S2), S3), ... Sn) 
```

<br><br>
*Algorithm:*

To employ this idea, the algorithm iterates through the strings [S1 ... Sn]. finding at each iteration
i the longest common prefix of strings LCP(S1 ... Si). When LCP(S1 ... Si) is an empty string, the 
algorithm ends. Otherwise after n iterations, the algorithm returns LCP(S1 ... Sn) 

```

Example: 

{leets, leetcode, leet, leeds}
   \       /      
  LCP{1,2} = leets
  	     leetcode
	     leet 

	 	\	{leets, leetcode, leet, leeds}
		 \ 			   /

		 LCP{1,3} = leet
		 	    leet
			    leet

			      \          {leets, leetcode, leet, leeds}
			       \ 				  /
			       LCP{1,4}   leet
			       		  leeds
					  lee

				LCP{1,4} = "lee"
```

```java
public String longestCommon Prefix(String[] strs){
	if (strs.length==0){
		return ""; 
	}
	String prefix=strs[0]; 
	for (int i=1; i<strs.length; i++) {
		while (strs[i].indexOf(prefix) != 0) {
			prefix=prefix.substring(0, prefix.length() -1);
			if (prefix.isEmpty()) {
				return "";
			}
		}
		return prefix; 
	}
}
```

**Complexity Analysis**
```
Time complexity: 	O(S)	Where S is the sum of all characters in all strings. In the worse case
				all n strings are the same. The algorithm compares the string S1 with 
				the other strings [S2 ... Sn]. There are S character comparisons where
				S is the sum of all characters in the input array 

Space complexity: 	O(1) 	We only used constant extra space 
```


<br><br>
<a name="longestCommonPrefixVerticalScanning"></a>
## Vertical Scanning

Imagine a very short string is at the end of the array. The above approach will still do S comparisons.
One way to optimize this case is to do vertical scanning. We compare characters from top to bottom on
the same column (same character index of the strings) before moving on to the next column. 


```java
public String longestCommonPrefix(String[] strs) {
	if (strs==null || strs.length==) return ""; 
	for (int i=0; i<strs[0].length(); i++){
		char c=strs[0].charAt(i); 
		for (int j=1; j<strs.length; j++) {
			if (i==strs[j].length() || strs[j].charAt(i)!=c){
				return strs[0].substring(0,i);
			}
		}
	}
	return strs[0]; 
}
```

**Complexity Analysis**

```
Time complexity: 	O(S) 	Where S is the sum of all characters in all strings. In the worst case
				there will be n equal strings with length m and the algorithm performs
				S=n*m character comparisons. Even the worst case is still the same as 
				Approach 1, in the best case there are at most n*minLen comparisons 
				where minLen is the length of the shortest string in the array. 

Space complexity: 	O(1)	We only used constant extra space
```

<br><br>
<a name="longestCommonPrefixDivideandConquer"></a>
## Divide and Conquer

The idea of the algorithm comes from the associative property of LCP operation. We notice that: 
LCP(S1 ... Sn) = LCP(LCP(S1 ... Sk), LCP(Sk+1 ... Sn)), where LCP(S1 ... Sn) is the longest common
prefix in a set of strings [S1 ... Sn], 1<k<n 

<br><br>
*Algorithm* 

To apply the previous observation, we use the divide and conquer technique, where we split the 
LCP(Si ... Sj) problem into two subproblems LCP(Si ... Smid) and LCP(Smid+1 ... Sj), where mid is 
(i+j)/2. We use their solutions lcpLeft and lcpRight to construct the solution of the main problem 
LCP(Si ... Sj). To accomplish this we compare one by one the characters of lcpLeft and lcpRight till 
there is no character match. The found common prefix of lcpLeft and lcpRight is the solution of the 
LCP(Si ... Sj) 


```
				{leetcode, leet, lee, le} 

				    /                \   
Divide 			{leetcode, leet}            {lee, le} 

Conquer				|			 | 

			     {leet} 		        {le} 

			         \                      /

				 	   {le} 

	Searching for the longest common prefix (LCP) in dataset {leetcode, leet, lee, le} 
```

```java
public String longestCommonPrefix(String[] strs) { 

	if (strs == null || strs.length ==0) return "";
		return longestCommonPrefix(strs, 0, strs.length-1); 

}

private String longestCommonPrefix(String[] strs, int l, int r) { 
	if (l==r) {
		return strs[l];
	}
	else {
		int mid=(l+r)/2; 
		String lcpLeft= longestCommonPrefix(strs,l, mid); 
		String lcpRight= longestCommonPrefix(strs,mid+1;r); 
		return commonPrefix(lcpLeft,lcpRight);
	}
}

String commonPrefix(String left, String right) {
	int min=Math.min(left.length(), right.length()); 
	for (int i=0; i<min; i++) {
		if (left.charAt(i) !=right.charAt(i) ){
			return left.substring(0, i);
		}
	}
	return left.substring(0, min);
}
```

**Complexity Analysis**

In the worst case we have n equal strings with length m

```
Time Complexity: O(S)		where S is the number of all characters in the array, S=m*n so time
				complexity is 2*T(n/2)+O(m). Therefore time complexity is O(S). In the
				best case the algorithm performs O(minLen * n) comparisons, where
				minLen is the shortest string of the array 

Space Complexity: O(m*log(n))	There is a memory overhead since we sotre recursive call in the 
				execution stack. There are log(n) recursive calls, each store needs m
				space to store the result so space complexity is O(m*log(n))
```

<br><br>
<a name="longestCommonPrefixBinarySearch"></a>
## Binary Search

The idea is to apply binary search method to find the string with maximum value L, which is common 
prefix of all the strings. The algorithm searches the space in the interval (0 ... minLen), where 
minLen is minimum string length and the maximum possible common prefix. Each time search space is 
divided in two equal parts, one of them is discarded because it is sure that it doesn't contain the 
solution. There are two possible cases: 

* S[1...mid] is not a common string. This means that for each j>i, S[1...j] is not a common string and we discard the second half of the search space
* S [1...mid] is common string. This means that for each i<j, S[1...i] is a common string and we discard the first half of the search space, because we try to find longer common prefix 

```
 				{leets, leetcode, leetc, leeds} 

						|
					      
					     "leets"
					    /        \
					 "lee"      "ts"

					     midpoint 
				
				"lee" in "leetcode" : yes
				"lee" in "leetc" : yes
				"lee" in "leeds" : yes

						|

					     "leets"
					     /     \
					  "lee"    "ts"
					    |      /   \

					  "lee"   "t"   "s"
					        
						   midpoint


						   "leet" in "leetcode" : yes
						   "leet" in "leetc" : yes 
						   "leet" in "leeds" : no

						   LCP= "lee" 
```

```java
public String longestCommonPrefix(String[] strs) {
	if (strs==null || strs.length==0)
		return "";
	int minLen=Integer.MAX_VALUE; 
	for (String str: strs)
		minLen=Math.min(minLen, str.length());
	int low=1; 
	int high=min Len; 
	while (low<=high) {
		int middle=(low+high)/2;
		if (isCommonPrefix(strs, middle)
			low=middle+1;
		else 
			high=middle-1;
	}
	return strs[0].substring(0, (low + high)/2);
} 

private boolean isCommonPrefix(String[] strs, int len) {
	String str1=strs[0].substring(0,len);
	for (int i=1; i<strs.length; i++)
		if (!strs[i].startsWith(str1))
			return false;
	return true;
}
```

**Complexity Analysis

In the worst case we have n equal strings with length m 

```
	Time complexity: 	O(S * log(n)), where S is the sum of all characters in all strings. The
				algorithm makes log(n) iterations, for each of them there are S=m*n 
				comparisons, which gives in total O(S * log(n)) time complexity

	Space complexity: 	O(1). We only used constant extra space 
```
<br><br>
<a name="longestCommonPrefixFurtherThoughts"></a>
## Further Thoughts 

Considering a slightly different problem: 
```
	Given a set of keys S= [S1, S2 ... Sn], find the longest common prefix among a string q and S.
	This LCP query will be called frequently
```
We coule optimize LCP queries by storing the set of keys S in a Trie. See this for [Trie 
implementation](#trie). In a Trie, each node descending from the root represents a common prefix of some keys. But we need to 
find the longest common prefix of a string q and all key strings. This means that we have to find the
deepest path from the root, which satisfies the following conditions 

* it is a prefix of query string q
* each node along the path must contain only one child element. Otherwise the found path will not be a
  common prefix among all strings
* the path doesn't comprise of nodes which are marked as end of key. Otherwise the path couldn't be a
  prefix of a key which is shorter than itself

<br><br>
*Algorithm* 

The only question left is how to find the deepest path in the Trie, that fulfills the requirements 
above. The most effective way is to build a trie from {S1 ... Sn] strings. Then find the prefix of 
query string q in the Trie. We traverse the Trie from the root, till it is impossible to continue the
path in the Trie because one of the conditions above is not satisfied. 


```
Searching for the longest common prefix of string "le" in a Trie from dataset {lead, leet}

			Root

			 1

	l   ===========>  \  l

			     2

	e   ===============>   \ e

LCP "le" FOUND	=============>   3   

			     a	/  \ e    End of Key "lee" 
				     
			      6      4

			 d  /	       \ t
				        
END OF KEY "lead"	  7		 5   End of key "leet"
```



```
public String longestCommonPrefix(String q, String[] strs) {
    if (strs == null || strs.length == 0)
         return "";  
    if (strs.length == 1)
         return strs[0];
    Trie trie = new Trie();      
    for (int i = 1; i < strs.length ; i++) {
        trie.insert(strs[i]);
    }
    return trie.searchLongestPrefix(q);
}

class TrieNode {

    // R links to node children
    private TrieNode[] links;

    private final int R = 26;

    private boolean isEnd;

    // number of children non null links
    private int size;    
    public void put(char ch, TrieNode node) {
        links[ch -'a'] = node;
        size++;
    }

    public int getLinks() {
        return size;
    }
    //assume methods containsKey, isEnd, get, put are implemented as it is described
   //in  https://leetcode.com/articles/implement-trie-prefix-tree/)
}

public class Trie {

    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

//assume methods insert, search, searchPrefix are implemented
    private String searchLongestPrefix(String word) {
        TrieNode node = root;
        StringBuilder prefix = new StringBuilder();
        for (int i = 0; i < word.length(); i++) {
            char curLetter = word.charAt(i);
            if (node.containsKey(curLetter) && (node.getLinks() == 1) && (!node.isEnd())) {
                prefix.append(curLetter);
                node = node.get(curLetter);
            }
            else
                return prefix.toString();

         }
         return prefix.toString();
    }
}
```

**Complexity Analysis**
```
In the worst case query q has length m and is equal to all n strings of the array 

Time Complexity:   O(S)   where S is the number of all characters in the array, LCP query O(m) 
  			  Trie build has O(S) time complexity. To find the common prefix of q 
			  in the Trie takes in the worst O(m). 

Space complexity:  O(S)   we only used additional S extra space for the Trie. 
```


<br><br><br>
***
<a name="threeSum"></a>
# 15-3Sum


Given an array "nums" of n integers, are there elements a, b, c in nums such that a+b+c=0? Find all 
unique triplets in the array which gives the sum of zero. 

Note: 

The solution set must not contain duplicate triplets 

```
Example: 

Given array nums = [-1, 0, 1, 2, -1, -4]. 

A solution set is: 
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```
<br><br>
<a name="threeSumSortedArray"></a>
## Sorted Array


The method is to sort an input array and then run through all indices of a possible first element of a
triplet. For each element we make another 2Sum sweep of the remaining part of the array. Also we want
to skip elements to avoid duplicates in the answer without expending extra memory. 

```
public List<List<Integer>> threeSum(int[] num) {
    
    //Arrays.sort re-arranges the array of integers in ascending order
    //ex. [1, 2, 3, 4]

    Arrays.sort(num);
    List<List<Integer>> res = new LinkedList<>(); 
    for (int i = 0; i < num.length-2; i++) {
        if (i == 0 || (i > 0 && num[i] != num[i-1])) {
            
	    //This lets us skip some of the duplicate entries in the array
	    
	    int lo = i+1, hi = num.length-1, sum = 0 - num[i];

	    //This is for the 2 Sum sweep 

            while (lo < hi) {
                if (num[lo] + num[hi] == sum) {
                    res.add(Arrays.asList(num[i], num[lo], num[hi]));
                    while (lo < hi && num[lo] == num[lo+1]) lo++;
                    while (lo < hi && num[hi] == num[hi-1]) hi--;

		    //This lets us skip some of the duplicate entries in the array

                    lo++; hi--;
                } else if (num[lo] + num[hi] < sum) lo++;
                else hi--;

		//This allows us to optimize slightly since we know that the array is sorted
           }
        }
    }
    return res;
}
```

**Complexity Analysis**
```
Time Complexity:  O(n^2)   We go through a maximum of n elements for the first element of a triplet, 
			   and then when making a bi-directional 2Sum sweep of the remaining part of 
			   the array we also go through a maxiumum of n elements. 

Space Complexity: O(1)	   If we assume the return linked list is not extra space, then we do not 
			   allocate any significant extra space
```



<br><br><br>
***
<a name="threeSumClosest"></a>
# 16-3Sum Closest

Given an array nums of n integers and an integer target, find three integers in nums such that the sum
is closest to target. Return the sum of the three integers. You may assume that each input would have
exactly one solution. 

```
Example:

Given array nums=[-1, 2, 1, -4], and target=1.

The sum that is closest to the target is 2. (-1+2+1=2)
```

<br><br>
<a name="threeSumClosestThreePointers"></a>
## 3 Pointers

Similar to the previous 3Sum problem, we use three pointers to point to the current element, next 
element and the last element. If the sum is less than the target, it means that we need to add a larger
element so next element move to the next. If the sum is greater, it means we have to add a smaller 
element so last element move to the second last element. Keep doing this until the end. Each time 
compare the difference between sum and target, if it is less than minimum difference so far, then 
replace result with it, otherwise continue iterating. 

```
public class Solution {
		public int threeSumClosest(int[] num, int target) {
		int result=num[0] + num[1] + num[num.length-1];
		Arrays.sort(num);
		for (int i=0; i<num.length -2; i++) {
			int start= i+1, end = num.length -1;
			while (start < end) {
				int sum = num[i] + num[start] + num[end];
				if (sum > target) {
					end--;
				} else {
					start++;
				}
				if (Math.abs(sum-target) < Math.abs(result-target)) {
					result=sum;
				}
			}
		}
		return result;
	}
}
```


<br><br><br>
***
<a name="letterCombinationsofaPhoneNumber"></a>
# 17-Letter Combinations of a Phone Number 

Given a string contianing digits from 2-9 inclusive, return all possible letter combinations that the 
number could represent. 

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not
map to any letters. 

```
2 - abc 	3 - def 	4 - ghi		5 - jkl		6 - mno		7 - pqrs 	8 - tuv
				
						9 - wxyz
```


```
Example: 


Input: "23" 

Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]. 
```


*Note: The above answer is in lexicographical order but the answer can be in any order*

<br><br>
<a name="letterCombinationsofaPhoneNumberBacktracking"></a>
## Backtracking 


Backtracking is an algorithm for finding all solutions by exploring all potential candidates. If the 
solution candidate turns to not be a solution (or at least not the last one), backtracking algorithm 
discards it by making some changes on the previous step, ie *backtracks* and then tries again. 

Here is a backtrack function backtrack(combination, next_digits) which takes as arguments an ongoing 
letter combination and the next digits to check. 

* If there are no more digits to check that means the current combination is done 
* If there are still digits to check: 
	* Iterate over the letters mapping to the next available digit
	* Append the current letter to the current combination and proceed to check next digits: 


```
	  combination = combination + letter

	  backtrack(combination + letter, next_digits[1:]).
```


**Visual Representation** 

```
					
						"2 3"

						 
						  2
						
					      /   |   \
                                            
					     a    b    c
                                       

				         /        |        \

                                       
				      3           3            3

				    / | \       / | \        / | \

				   d  e  f     d  e  f      d  e  f

				
			["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

```java 
class Solution {
	Map<String, String> phone = new HashMap<String, String>() {{
		put("2", "abc"); 
		put("3", "def");
		put("4", "ghi");
		put("5", "jkl"); 
		put("6", "mno");
		put("7", "pqrs");
		put("8", "tuv");
		put("9", "wxyz");
	}}; 

	List<String> output = new ArrayList<String>(); 

	public void backtrack(String combination, String next_digits) {
		
		
		//if there are no more digits to check 
		if (next_digits.length()==0) {
			
			//the combination is done 
			output.add(combination);
		}

		

		//if there are still digits to check 
		else { 
		
			//iterate over all letters which map the next available digit 
			String digit = next_digits.substring(0,1); 
			String letters = phone.get(digit);
			for (int i=0; i<letters.length(); i++) {
				String letter = phone.get(digit).substring(i, i+1);
				//append the current letter to the combination and proceed to next
				backtrack(combination + letter, next_digits.substring(1));
			}
		}

	}

	public List<String> letterCombinations(String digits) { 
		if (digits.length() !=0) {
			backtrack("", digits);
		}
		return output;
	}
}
```

**Complexity Analysis** 

```

Time Complexity: 	O(3^N * 4^M) 	where N is the number of digits in the input that maps to 3
					letters (eg. 2, 3, 4, 5, 6, 8) and M is the number of digits 
					in the input that maps to 4 letters (eg. 7, 9) and N+M is the 
					total number digits in the input 

Space Complexity: 	O(3^N * 4^M)	since one has to keep 3^N * 4^M solutions 
```



<br><br>
<a name="letterCombinationsofaPhoneNumberFIFOQueue"></a>
## First In First Out (FIFO) Queue 

This solution utilizes the Single Queue Breadth First Search (BFS) which is an algorithm for traversing
or searching tree or graph data structures. It starts at the tree root and explores all of the neighbor
nodes. 


```java 
public List<String> letterCombinations(String digits) {
	
	LinkedList<String> ans = new LinkedList<String>();
	if (digits.isEmpty()) return ans; 
	String[] mapping = new String[] {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", {wxyz"};
	ans.add(""); 
	for (int i = 0; i<digits.length(); i++) {
		int x = Character.getNumericValue(digits.charAt(i)); 
		
		//we terminate the while loop when we encounter a new-formed string which is more than
		//the current level i 
		
		//peek retrieves the first value of the linked list
		while (ans.peek().length==i){
			
			//removes the head or the first value in the linkedlist
			String t = ans.remove(); 
			for (char s : mapping[x].toCharArray()) {
				ans.add(t+s);
				//this works because add appends to the end of the list
			}
		}
		return ans; 
	}
}
```

**Complexity Analysis**

```

Time Complexity: 	O(3^N * 4^M) 	where N is the number of digits in the input that maps to 3
					letters (eg. 2, 3, 4, 5, 6, 8) and M is the number of digits 
					in the input that maps to 4 letters (eg. 7, 9) and N+M is the 
					total number digits in the input 

Space Complexity: 	O(3^N * 4^M)	since one has to keep 3^N * 4^M solutions 
```

<br><br><br>
***
<a name="fourSum"></a>
# 18-4Sum

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such
that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target



*Note:*
The solution set must not contain duplicate quadruplets 


```
Example: 


Given array nums = [1, 0, -1, 0, -2, 2], and target = 0


A solution set is: 

[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```


<br><br>
<a name="fourSumSortedArray"></a>
## Sorted Array  

The idea is the same as the other numbered sum problems like 2sum and 3sum. We sort the array and then
proceed to interate through the values until we end up with a result that we are looking for. 

```java 
public class Solution {
	public List<List<Integer>> fourSum(int[] num, int target) {
		
		ArrayList<List<Integer>> ans = new ArrayList<>();
		
		if (num.length<4) {
			
			return ans;
		}
		Arrays.sort(num); 
		
		for (int i=0; i<num.length-3; i++) {   //picking the first candidate must leave room
						       //for the other values 
			
			if (num[i]+num[i+1]+num[i+2]+num[i+3]>target) {
				
				break;
				//first candidate too large, search finished
			}

			if (num[i]+num[num.length-1]+num[num.length-2]+num[num.length-3]<target) {
				
				continue;
				//first candidate too small 
			}

			if(i>0 && num[i]==num[i-1]) {
				
				continue;
				//prevents duplicate in ans list
			}
			
			for (int j=i+1; j<num.length-2; j++) {   //picking the second candidate must
								 //leave room for other values 
				
				if (num[i]+num[j]+num[j+1]+num[j+2]>target) {
					
					break;
					//second candidate too large
				}

				if (num[i]+num[j]+num[num.length-1]+num[num.length-2]<target) {
				
					continue;
					//second candidate too small
				}

				if(j>i+1 && num[j]==num[j-1]) {
					
					continue;
					//prevents duplicate results in ans list
				}

				int low=j+1, high=num.length-1;
				
				//two pointer search
				while(low<high) {
					
					int sum=num[i]+num[j]+num[low]+num[high];
					if (sum==target) {
						
						ans.add(Arrays.asList(num[i],num[j],num[low],num[high]));
						while(low<high&&num[low]==num[low+1]) {
							low++; //skipping over duplicates
						}

						while(low<high && num[high]==num[high-1] {
							high--; //skipping over duplicates 
						}
						low++;
						high--;
					}

					//moving window
					else if (sum<target) {
						low++;
					}

					else {
						high--;
					}
				}
			}
		}
		return ans;
	}
}
```






<br><br><br>
***
<a name="removeNthNodefromEndofList"></a>
# 19-Remove Nth Node From End of List 

Given a linked list, remove the n-th node from the end of the list and return its head

```
Example: 

Given linked list: 1 -> 2 -> 3 -> 4 -> 5, and n=2 


After removing the second node from the end, the linked list becomes 
		   
		   1 -> 2 -> 3 -> 5
```

**Note:**
Given n will always be valid 

**Follow up:**
Could you do this in one pass? 









<br><br>
<a name="removeNthNodefromEndofListTwoPassAlgorithm"></a>
## Two Pass Algorithm


**Intuition**

We notice that the problem could be simply reduced to another one: Remove the (L-n+1)th node from the
beginning of the list, where L is the list length. This problem is easy to solve once we found the 
list length L. 





<br><br>
**Algorithm** 

First we will add an auxiliary "dummy" node, which points to the list head. The "dummy" node is used to
simplify some corner cases such as a list with only one node or removing the head of the list. On the 
first pass, find the list length L. Then we set a pointer to the dummy node and start to move it 
through the list till it comes to the (L-n)th node. We relink next pointer of the (L-n)th node to the
(L-n+2)th node and we are done. 


```
	D -> 1 -> 2 -> 3 -> 4 -> NULL

		    |
		    v

	D -> 1 -> 2 -> 4 -> NULL
```



```java 
public ListNode removeNthFromEnd(ListNode head, int n) {
	
	ListNode dummy = new ListNode(0); 
	dummy.next = head; 
	int length =0; 
	ListNode first = head; 
	
	while (first!=null) {
		
		length++;
		first=first.next;
	}

	length -= n; 
	first = dummy;
	while (length>0) {
		
		length--;
		first=first.next;
	}
	first.next=first.next.next;
	return dummy.next; 
}
```

**Complexity Analysis** 
```
Time Complexity: 	O(L) 	The algorithm makes two traversals of the list, first to calculate the 
				list length L and second to find the (L-n)th node. There are 2L-n 
				operations and time complexity is O(L)

Space Complexity: 	O(1) 	We only used constant extra space
```





<br><br>
<a name="removeNthNodefromEndofListOnePassAlgorithm"></a>
## One Pass Algorithm

The previous algorithm could be optimized to one pass. Instead of one pointer, we could use two 
pointers. The first pointer advances the list by n+1 steps from the beginning, while the second pointer
starts from the beginning of the list. Now, both pointers are separated by exactly n nodes. We maintain
this constant gap by advancing both pointers together until the first pointer arrives past the last 
node. The second pointer will be pointing at the nth node counting from the last. We relink the next
pointer of the node referenced by the second pointer to point to the node's next next node. 



```
Maintaining N=2 nodes apart between the first and second pointer 

	D	-> 1 -> 2 -> 3 -> 4 -> 5 -> NULL

       first 	 Head 
       second 

			   


Move the first pointer N+1 steps 


			     |
			     v


	D	-> 1 -> 2 -> 3 -> 4 -> 5 -> NULL

      second     Head       First


Move the first and second pointers together until the first pointer arrives past the last node 


			     |
			     v


	D	-> 1 -> 2 -> 3 -> 4 -> 5 -> NULL
		
		 Head      Second           First

Second pointer points to the nth node counting from last so link node to the node's next next node 



				  |
				  v


	D	-> 1 -> 2 -> 3 ->   -> 5 -> NULL
	         
		 Head      Second           First
```


```java 
public ListNode removeNthFromEnd(ListNode head, int n) {
	
	ListNode dummy = new ListNode(0);
	dummy.next = head; 
	ListNode first = dummy; 
	ListNode second = dummy;
	
	//Moves the first pointer so that the first and second nodes are separated by n nodes
	
	for (int i=1; i<=n+1; i++) {
		
		first = first.next;
	}

	//Move first to the end, maintaining the gap

	while (first!=null) {

		first=first.next;
		second=second.next;
	}

	second.next=second.next.next;
	return dummy.next;
}
```



**Complexity Analysis** 

```
Time Complexity: 	O(L) 	The algorithm makes one traversal of the list of L nodes. Therefore
				time complexity is O(L)

Space Complexity: 	O(1)	Only constant extra space was used 
```







<br><br><br>
***
<a name="validParentheses"></a>
# 20-Valid Parentheses










<br><br><br><br><br>
***
<br><br><br>

<a name="trie"></a>
# Trie 

Implement a trie with insert, search, and startsWith methods
```
Example: 
	Trie trie=new Trie(); 

	trie.insert("apple");
	trie.search("apple");		//returns true 
	trie.search("app");		//returns false
	trie.startsWith("app");		//returns true
	trie.insert("app");
	trie.search("app"); 		//returns true

Note 

* You may assume that all inputs consist of lowercase letters a-z
* All inputs are guaranteed to be non-empty strings 
```

<br><br>
## Solution 


Trie (we pronounce "try") or prefix tree is a tree data structure which is used for the retrieval of a
key in a dataset of strings. THere are various applications of this very efficient data structure such
as: 

* Autocomplete
* Spell checker 
* IP routing (Longest prefix matching) 
* T9 predictive text (text on nine keys - used on phones during the late 1990s) 
* Solving word games 


There are several other data structures like balanced trees and hash tables which give us the 
possibility to search for a word in a dataset of strings so why do we use a trie? Althought a hash 
table has O(1) time complexity for looking for a key, it is not efficient in the following operations: 

* Finding all keys with a common prefix
* Enumerating a dataset of strings in lexicographical order

Another reason why the trie outperforms has table, is that as hash table increases in size, there are
lots of hash collisions and the search time complexity could deteriorate to O(n), where n is the 
number of keys inserted. Tries could use less space compared to Hash Table when storing many keys with
the same prefix. In this case using trie has only O(m) time complexity, where m is the key length.
Searching for a key in balanced tree costs O(m log n) time complexity. 


## Trie node structure 

Trie is a rooted tree. Its nodes have the following fields: 

* Maximum of R links to its children, where each link corresponds to one of R character values from
  dataset alphabet. In this article we assume that R is 26, the number of lowercase latin letters 

* Boolean field which specifies whether the node corresponds to the end of the key, or is just a 
  key prefix


```

Root 

		isEnd: false 
	a b c d e f g h i j k l m n o p q r s t u v w x y z
	                      
			      |
  			     
			     link 

	        isEnd: false
	a b c d e f g h i j k l m n o p q r s t u v w x y z

		|

	       link 

	        isEnd: false
	a b c d e f g h i j k l m n o p q r s t u v w x y z

		|

	       link 

	        isEnd: false
	a b c d e f g h i j k l m n o p q r s t u v w x y z

					      |

	       				     link 

	        isEnd: true 


Representation of a key "leet" in trie 
```

```java 
class TrieNode {

    // R links to node children
    private TrieNode[] links;

    private final int R = 26;

    private boolean isEnd;

    public TrieNode() {
        links = new TrieNode[R];
    }

    public boolean containsKey(char ch) {
        return links[ch -'a'] != null;
    }
    public TrieNode get(char ch) {
        return links[ch -'a'];
    }
    public void put(char ch, TrieNode node) {
        links[ch -'a'] = node;
    }
    public void setEnd() {
        isEnd = true;
    }
    public boolean isEnd() {
        return isEnd;
    }
}
```

Two of the most common operations in a trie are insertion of a key and search for a key

## Insertion of a key to a trie

We insert a key by searching into the trie. We start from the root and search a link, which corresponds
to the first key character. There are two cases: 

* A link exists. Then we move down the tree following the link to the next child level. The algorithm
  continues with searching for the next key character. 

* A link does not exist. Then we create a new node and link it with the parent's link matching the 
  current key character. We repeat this step until we encounter the last character of the key, then 
  we mark the current node as an end node and the algorithm finishes. 


```
Inserting "le" into the Trie


		Root
		 
		 1
  
                  \ l
		    
		    2
 
                      \ e
                     
		        3   End of Key "le"


```

```
Inserting "leet" into the Trie 




			Root

			 1

			  \  l

			     2

			       \ e

			         3   End of key "le"

				   \ e
				     
				     4

				       \ t
				        
					 5   End of key "leet"

```


```
Inserting "code" into the Trie 



				Root
				 
				  1

			      c	 / \  l

			       6     2
			     
			  o   /        \  e

			     7            3    End of key "le"
			 
		       d   /                \   e

			 8                    4

		    e  /                        \   t
		      
End of key "code"     9                           5   End of Key "root"


```

Building a Trie from dataset {le, leet, code}


```java
class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            char currentChar = word.charAt(i);
            if (!node.containsKey(currentChar)) {
                node.put(currentChar, new TrieNode());
            }
            node = node.get(currentChar);
        }
        node.setEnd();
    }
}
```

**Complexity Analysis**

```
	Time complexity:  O(m)  where m is the key length. In each iteration of this algorithm we 
	 			either create a node in the trie till we reach the end of the key. 
				This takes only m operations 

	Space complexity: O(m)  In the worst case newly inserted key doesn't share a prefix with the 
				keys already inserted in the trie. We have to add m new nodes, which 
				only takes us O(m) space
```


## Search for a Key in a Trie 


Each key is represented in the trie as a path from the root to the internal node or leaf. We start from
the root with the first key character. We examine the current node for a link corresponding to the key
character. There are two cases: 

* A link exists. We move to the next node in the path following this link, and proceed searching for
  the next key character 
* A link does not exist. If there are no available key characters and current node is marked as isEnd
  we return true. Otherwise there are two possible cases in each of them we return false: 

  * There are key characters left, but it is impossible to follow the key path in the trie, and the
    key is missing
  * No key characters left, but current node is not marked as isEnd. Therefore the search key is only
    a prefix of another key in the trie


```
Searching for key "leet" in the Trie

		                 Root
				 
				  1

			      c	 / \  l    <============================== l

			       6     2
			     
			  o   /        \  e   <=========================== e

			     7            3    End of key "le"
			 
		       d   /                \   e   <===================== e

			 8                    4

		    e  /                        \   t   <================= t
		      
End of key "code"     9                           5   End of Key "root"    <============ Key Found


```

```java
class Trie {
    ...

    // search a prefix or whole key in trie and
    // returns the node where search ends
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
           char curLetter = word.charAt(i);
           if (node.containsKey(curLetter)) {
               node = node.get(curLetter);
           } else {
               return null;
           }
        }
        return node;
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
       TrieNode node = searchPrefix(word);
       return node != null && node.isEnd();
    }
}
```

**Complexity Analysis**

```
	Time Complexity:   O(m)    In each step of the algorithm we search for the next key character.
	 			   In the worst case the algorithm performs m operations
	Space Complexity:  O(1)
```


## Search for a key prefix in a trie

The approach is very similar to the one we used for searching a key in a trie. We traverse the trie 
from the root, till there are no character left in key prefix or it is impossible to continue the path
in the trie with the current key character. The only difference with the mentioned above search for a 
key algorithm is that when we come to an end of the key prefix, we always return true. We don't need to
conside the isEnd mark of the current trie node, because we are searching for a prefix of a key, not
for a whole key. 


```
Searching for "co" in the Trie 


				Root
				 
				  1

      	c  ==============>    c	 / \  l

			       6     2
			     
 	o  ============>  o   /        \  e

	Prefix Found         7            3    End of key "le"
			 
		       d   /                \   e

			 8                    4

		    e  /                        \   t
		      
End of key "code"     9                           5   End of Key "root"
```

```java
class Trie {
    ...

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode node = searchPrefix(prefix);
        return node != null;
    }
}
```

**Complexity Analysis**
```
	Time Complexity:  O(m)
	Space Complexity: O(1)
```



