## 1. Two Sum E


Учитывая массив целых чисел nums и целочисленное целевое значение, верните индексы двух чисел так, чтобы в сумме они составляли целевое значение.

Вы можете предположить, что каждый вход будет иметь ровно одно решение, и вы не можете использовать один и тот же элемент дважды.

Вы можете вернуть ответ в любом порядке.


```python
Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]
```

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    for i in range(len(nums)):
        for j in range(i, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```


## 2. Add Two Numbers M

<img src = "https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg">

Вам даны два непустых связанных списка, представляющих два неотрицательных целых числа. Цифры хранятся в обратном порядке, и каждый из их узлов содержит одну цифру. Сложите два числа и верните сумму в виде связанного списка.

Вы можете предположить, что эти два числа не содержат начальных нулей, кроме самого числа 0.


```python
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        left = 0
        dummy = cur = ListNode(-1)
        while l1 or l2 or left:
            left, sm = divmod(sum(l and l.val or 0 for l in (l1, l2)) + left, 10)
            cur.next = cur = ListNode(sm)
            l1 = l1 and l1.next
            l2 = l2 and l2.next
        return dummy.
```


## 3. Longest Substring Without Repeating Characters M


Для заданной строки s найдите длину самой длинной подстроки без повторяющихся символов.



```python
Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
Example 2:

Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```python

class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        mx, start, chars = 0, 0, {}
        for i in range(len(s)):
            if s[i] in chars and start <= chars[s[i]]: start = chars[s[i]] + 1
            else: mx = max(mx, i - start + 1)
            chars[s[i]] = i
        return mx
```


## 4. Median of Two Sorted Arrays H


Учитывая два отсортированных массива nums1 и nums2 размера m и n соответственно, вернуть медиану двух отсортированных массивов.

Общая сложность времени выполнения должна быть O(log (m+n)).


```python
Example 1:

Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
Example 2:

Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

```python

class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        arr = sorted(nums1 + nums2)
        if len(arr) % 2 == 0: return (arr[len(arr) // 2] + arr[len(arr) // 2 - 1]) / 2
        else: return arr[len(arr) // 2]
```


## 5. Longest Palindromic Substring M


Учитывая строку s, вернуть самую длинную палиндромную подстроку в s.



```python
Example 1:

Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
Example 2:

Input: s = "cbbd"
Output: "bb"
```

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def check(l, r):
            while 0 <= l <= r < len(s) and s[l] == s[r]:
                l -= 1
                r += 1
            return s[l + 1:r]
        pals = [check(i, i) for i in range(len(s))] + [check(i, i + 1) for i in range(len(s) - 1) if s[i] == s[i + 1]]
        return sorted(pals, key = len)[-1] if pals else ''
```


## 6. Zigzag Conversion M


Строка «PAYPALISHIRING» записывается зигзагообразным узором в заданном количестве строк, например так: (вы можете отобразить этот узор фиксированным шрифтом для лучшей читаемости)

P   A   H   N
A P L S I I G
Y   I   R

А потом читать построчно: "ПАХНАПЛСИИГЙИР"

Напишите код, который будет принимать строку и выполнять это преобразование с заданным количеством строк:

string convert(string s, int numRows);


```python
Example 1:

Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
Example 2:

Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
Example 3:

Input: s = "A", numRows = 1
Output: "A"
```

```python
class Solution:
    def convert(self, s, numRows):
        if numRows == 1 or numRows >= len(s): return s
        row, direction, res = 0, -1, [""] * numRows
        for char in s:
            res[row] += char
            if row == 0 or row == numRows - 1: direction *= -1 
            row += direction
        return "".join(res) 
```


## 7. Reverse Integer M

```python
Example 1:

Input: x = 123
Output: 321
Example 2:

Input: x = -123
Output: -321
Example 3:

Input: x = 120
Output: 21
```

```python
class Solution:
    def reverse(self, x):
        x = int(str(x)[::-1]) if x >= 0 else int("-" + str(x)[::-1][:-1]); return -2 ** 31 <= x <= 2 ** 31 - 1 and x or 0
```


## 8. String to Integer (atoi) M 


реализовать функцию myAtoi(string s), которая преобразует строку в 32-битное целое число со знаком (аналогично функции atoi C/C++).

Алгоритм для myAtoi(string s) следующий:

Прочтите и игнорируйте начальные пробелы.
Проверьте, является ли следующий символ (если он еще не находится в конце строки) «-» или «+». Прочтите этот символ, если он есть. Это определяет, будет ли окончательный результат отрицательным или положительным соответственно. Предположим, что результат положительный, если ни один из них не присутствует.
Считайте следующие символы, пока не будет достигнут следующий нецифровой символ или конец ввода. Остальная часть строки игнорируется.
Преобразуйте эти цифры в целое число (например, «123» -> 123, «0032» -> 32). Если цифры не были прочитаны, то целое число равно 0. При необходимости измените знак (из шага 2).
Если целое число выходит за пределы диапазона 32-битных целых чисел со знаком [-231, 231 - 1], зафиксируйте целое число, чтобы оно оставалось в диапазоне. В частности, целые числа меньше -231 должны быть сжаты до -231, а целые числа больше 231-1 должны быть сжаты до 231-1.
Возвращает целое число в качестве окончательного результата.
Примечание:

Только символ пробела ' ' считается символом пробела.
Не игнорируйте никакие символы, кроме начального пробела или остальной части строки после цифр.


```python
Example 1:

Input: s = "42"
Output: 42
Explanation: The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "42" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-231, 231 - 1], the final result is 42.
Example 2:

Input: s = "   -42"
Output: -42
Explanation:
Step 1: "   -42" (leading whitespace is read and ignored)
            ^
Step 2: "   -42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -42" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-231, 231 - 1], the final result is -42.
Example 3:

Input: s = "4193 with words"
Output: 4193
Explanation:
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "4193 with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-231, 231 - 1], the final result is 4193.
```

```python
class Solution:
    def myAtoi(self, str):
        r = [int(c) for c in re.findall(r"^[-+]?\u005Cd+", str.lstrip())]
        return (r and 2 ** 31 - 1 < r[0] and 2 ** 31 - 1) or (r and r[0] < -2 ** 31 and -2 ** 31) or (r and r[0]) or 0
```


## 9. Palindrome Number E


Учитывая целое число x, вернуть true, если x является палиндромом, и false в противном случае.


```python
Example 1:

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
Example 2:

Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

```python
class Solution:
    def isPalindrome(self, x):
        return str(x) == str(x)[::-1]    
```


## 10. Regular Expression Matching H


Имея входную строку s и шаблон p, реализуйте сопоставление регулярных выражений с поддержкой '.' и где:

'.' Соответствует любому одиночному символу.
'*' Соответствует нулю или более предшествующих элементов.
Сопоставление должно охватывать всю входную строку (не частичную).


```python
Example 1:

Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
Example 3:

Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

```python
class Solution:
    def isMatch(self, s, p):
        return bool(re.match(r"%s" %p, s)) and re.match(r"%s" %p, s).group(0) == s 
```


## 11. Container With Most Water M

<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg">


Вам дан целочисленный массив высоты длины n. Нарисовано n вертикальных линий, две конечные точки i-й линии равны (i, 0) и (i, height[i]).

Найдите две линии, которые вместе с осью абсцисс образуют контейнер, содержащий наибольшее количество воды.

Возвращает максимальное количество воды, которое может храниться в контейнере.

Обратите внимание, что вы не можете наклонять контейнер.


```python
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
Example 2:

Input: height = [1,1]
Output: 1
```

```python
class Solution:
    def maxArea(self, height):
        left, right, mx = 0, len(height) - 1, 0
        while left < right:
            mx = max(mx, (right - left) * min(height[left], height[right]))
            if height[left] < height[right]: 
                left += 1
            else: 
                right -= 1
        return mx
```


## 12. Integer to Roman M


Римские цифры представлены семью различными символами: I, V, X, L, C, D и M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

Например, 2 записывается как II римскими цифрами, просто две единицы сложены вместе. 12 записывается как XII, то есть просто X + II. Число 27 записывается как XXVII, то есть XX + V + II.

Римские цифры обычно пишутся слева направо от большего к меньшему. Однако цифра четыре не IIII. Вместо этого цифра четыре пишется как IV. Так как единица предшествует пятерке, мы вычитаем ее и получаем четыре. Тот же принцип применим к числу девять, которое пишется как IX. Есть шесть случаев, когда используется вычитание:

I можно поставить перед V (5) и X (10), чтобы получились 4 и 9.
X можно поставить перед L (50) и C (100), чтобы получилось 40 и 90.
C можно поставить перед D (500) и M (1000), чтобы получились 400 и 900.
Дано целое число, преобразовать его в римскую цифру.


```python
Example 1:

Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
Example 2:

Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
Example 3:

Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

```python
class Solution:
    def intToRoman(self, num):
        s = "M" * (num // 1000)
        s += "CM" if num % 1000 >= 900 else "D" *((num % 1000) // 500)
        s += "CD" if num % 500 >= 400 and s[-2:] != "CM" else "C" * ((num % 500) // 100)  if num % 500 < 400 else ""
        s += "XC" if num % 100 >= 90 else "L" * ((num % 100) // 50)
        s += "XL" if num % 50 >= 40 and s[-2:] != "XC" else "X" * ((num % 50) // 10)  if num % 50 < 40 else ""
        s += "IX" if num % 10 >= 9 else "V" * ((num % 10) // 5)
        s += "IV" if num % 5 >= 4 and s[-2:] != "IX" else "I" * ((num % 5) // 1) if num % 5 < 4 else ""
        return s
```


## 13. Roman to Integer E


Римские цифры представлены семью различными символами: I, V, X, L, C, D и M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000

Например, 2 записывается как II римскими цифрами, всего две единицы, сложенные вместе. 12 записывается как XII, то есть просто X + II. Число 27 записывается как XXVII, то есть XX + V + II.

Римские цифры обычно пишутся слева направо от большего к меньшему. Однако цифра четыре не IIII. Вместо этого цифра четыре пишется как IV. Так как единица предшествует пятерке, мы вычитаем ее и получаем четыре. Тот же принцип применим к числу девять, которое пишется как IX. Есть шесть случаев, когда используется вычитание:

I можно поставить перед V (5) и X (10), чтобы получились 4 и 9.
X можно поставить перед L (50) и C (100), чтобы получилось 40 и 90.
C можно поставить перед D (500) и M (1000), чтобы получились 400 и 900.
Дана римская цифра, преобразовать ее в целое число.


```python
Example 1:

Input: s = "III"
Output: 3
Explanation: III = 3.
Example 2:

Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 3:

Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

```python
class Solution:
    def romanToInt(self, s):
        table = {"M": 1000, "D": 500, "C": 100, "L": 50, "X": 10, "V": 5, "I": 1}
        sm, pre = 0, 'I'
        for c in s[::-1]: 
            if table[c] < table[pre]:
                sm, pre = sm - table[c], c  
            else:
                sm, pre = sm + table[c], c
        return sm
```


## 14. Longest Common Prefix E


Напишите функцию, которая находит самую длинную строку общего префикса среди массива строк.

Если общего префикса нет, вернуть пустую строку "".


```python
Example 1:

Input: strs = ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

```python
class Solution:
    def longestCommonPrefix(self, s: List[str]) -> str:
        j = 0
        while s and all(j < len(s[i]) and j < len(s[i - 1]) and s[i][j] == s[i - 1][j] for i in range(len(s))):
            j += 1
        return s[0][:j] if j else ''
```


## 15. 3Sum M


Для массива целых чисел nums вернуть все триплеты [nums[i], nums[j], nums[k]] такие, что i != j, i != k и j != k, и nums[i] + числа [j] + числа [k] == 0.

Обратите внимание, что в наборе решений не должно быть повторяющихся триплетов.


```python
Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
```

```python
class Solution:
    def threeSum(self, nums):
        res, res_set = [], set()
        nums.sort()
        for i in range(len(nums) - 2):
            l, r = i + 1, len(nums) - 1
            while l < r:
                sm = nums[i] + nums[l] + nums[r] 
                if sm < 0: l += 1
                elif sm > 0: r -= 1
                elif (nums[i], nums[l], nums[r]) not in res_set: 
                    res.append([nums[i], nums[l], nums[r]])
                    res_set.add((nums[i], nums[l], nums[r])) 
                else: l, r = l + 1, r - 1
        return res
```


## 16. 3Sum Closest M


Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.


```python
Example 1:

Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
Example 2:

Input: nums = [0,0,0], target = 1
Output: 0
Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).
```

```python
class Solution:
    def threeSumClosest(self, nums, target):
        res = diff = float("inf")
        nums.sort()
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i - 1]: continue
            l, r = i + 1, len(nums) - 1
            while l < r:
                sm = nums[i] + nums[l] + nums[r]
                if abs(sm - target) < diff: diff, res = abs(sm - target), sm 
                if sm < target: l += 1
                elif sm > target: r -= 1
                else: return res
        return res
```


## 17. Letter Combinations of a Phone Number M


Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.


<img src = "https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png">

```python
Example 1:

Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
Example 2:

Input: digits = ""
Output: []
Example 3:

Input: digits = "2"
Output: ["a","b","c"]
```

```python
class Solution:
    def letterCombinations(self, digits):
        dic, res = { '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}, [""]
        for dig in digits:
            tmp = []
            for y in res: 
                for x in dic[dig]: tmp.append(y + x)
            res = tmp 
        return res if any(res) else []
```

## 18. 4Sum M


Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.


```python
Example 1:

Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
Example 2:

Input: nums = [2,2,2,2,2], target = 8
Output: [[2,2,2,2]]
```

```python
class Solution:
    def fourSum(self, nums, target):
        res, res_set = [], set()
        nums.sort()
        for i in range(len(nums) - 1):
            if i > 0 and nums[i] == nums[i - 1]: continue
            for j in range(i + 1, len(nums)):
                l, r = j + 1, len(nums) - 1
                while l < r:
                    sm = nums[i] + nums[j] + nums[l] + nums[r] 
                    if sm < target: l += 1
                    elif sm > target: r -= 1
                    elif (nums[i], nums[j], nums[l], nums[r]) not in res_set:
                        res.append([nums[i], nums[j], nums[l], nums[r]]); res_set.add((nums[i], nums[j], nums[l], nums[r])) 
                    else: l, r = l + 1, r - 1
        return res
```

## 19. Remove Nth Node From End of List M


Given the head of a linked list, remove the nth node from the end of the list and return its head.

<img src = "https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg">
```python
Example 1:

Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Example 2:

Input: head = [1], n = 1
Output: []
Example 3:

Input: head = [1,2], n = 1
Output: [1]
```

```python
class Solution:
    def fourSum(self, nums, target):
        res, res_set = [], set()
        nums.sort()
        for i in range(len(nums) - 1):
            if i > 0 and nums[i] == nums[i - 1]: continue
            for j in range(i + 1, len(nums)):
                l, r = j + 1, len(nums) - 1
                while l < r:
                    sm = nums[i] + nums[j] + nums[l] + nums[r] 
                    if sm < target: l += 1
                    elif sm > target: r -= 1
                    elif (nums[i], nums[j], nums[l], nums[r]) not in res_set:
                        res.append([nums[i], nums[j], nums[l], nums[r]]); res_set.add((nums[i], nums[j], nums[l], nums[r])) 
                    else: l, r = l + 1, r - 1
        return res
```

## 20. Valid Parentheses E


Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.


```python
Example 1:

Input: s = "()"
Output: true
Example 2:

Input: s = "()[]{}"
Output: true
Example 3:

Input: s = "(]"
Output: false
```

```python
class Solution:
    def isValid(self, s):
        brackets_stack, lefts, rights = [], ("(", "[", "{"), (")", "]", "}") 
        for char in s:
            if char in lefts: 
                brackets_stack.append(char)
            elif not brackets_stack or lefts.index(brackets_stack.pop()) != rights.index(char): 
                return False
        return not brackets_stack 
```

## 21. Merge Two Sorted Lists E


You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

<img src = "https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg">
```python
Example 1:

Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
Example 2:

Input: list1 = [], list2 = []
Output: []
Example 3:

Input: list1 = [], list2 = [0]
Output: [0]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2
        elif not l2: return l1
        if l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```

## 22. Generate Parentheses M


Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.


```python
Example 1:

Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
Example 2:

Input: n = 1
Output: ["()"]
```

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        bfs = [(0, 0, '')]
        for c in range(n * 2):
            bfs = [(l + 1, r, s + '(') for l, r, s in bfs if l + 1 <= n] + [(l, r + 1, s + ')') for l, r, s in bfs if l - r] 
        return [s for l, r, s in bfs]
```

## 23. Merge k Sorted Lists H


You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.


```python
Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
Example 2:

Input: lists = []
Output: []
Example 3:

Input: lists = [[]]
Output: []
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists):
        q = []
        for i in range(len(lists)):
            while lists[i]:
                q += lists[i],
                lists[i] = lists[i].next
        root = cur = ListNode(0)
        for h in sorted(q, key = lambda x: x.val):
            cur.next = cur = h
        return root.next
```

## 24. Swap Nodes in Pairs M


Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)


![im1](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)
```python
Example 1:

Input: head = [1,2,3,4]
Output: [2,1,4,3]
Example 2:

Input: head = []
Output: []
Example 3:

Input: head = [1]
Output: [1]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if not head or not head.next: return head
        first = head.next
        second = head
        second.next = self.swapPairs(first.next)
        first.next = second
        return first
```

## 25. Reverse Nodes in k-Group H


Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)
![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)
```python
Example 1:

Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
Example 2:

Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    def reverseKGroup(self, head, k):
        dummy = last = ListNode(0)
        cur = head
        while cur:
            first, cnt = cur, 1
            while cnt < k and cur:
                cur, cnt = cur.next, cnt + 1
            if cnt == k and cur:
                cur, prev = first, None
                for _ in range(k):
                    prev, cur.next, cur = cur, prev, cur.next
                last.next, last = prev, first
            else:
                last.next = first
        return dummy.next   
```

## 26. Remove Duplicates from Sorted Array E


Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Custom Judge:

The judge will test your solution with the following code:
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.


```python
Example 1:

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

```python
class Solution:
    def removeDuplicates(self, nums):
        n = len(nums)
        return n - len([nums.pop(i) for i in range(n -1, 0, -1) if nums[i] == nums[i - 1]])
```

## 27. Remove Element E


Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.


```python
Example 1:

Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for num in nums:
            if num != val:
                nums[i] = num
                i += 1
        return i
```

## 28. Find the Index of the First Occurrence in a String M


Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.


```python
Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
Example 2:

Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```

```python
class Solution:
    def strStr(self, haystack, needle):
        return haystack.find(needle)
```

## 29. Divide Two Integers M


Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.

The integer division should truncate toward zero, which means losing its fractional part. For example, 8.345 would be truncated to 8, and -2.7335 would be truncated to -2.

Return the quotient after dividing dividend by divisor.

Note: Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For this problem, if the quotient is strictly greater than 231 - 1, then return 231 - 1, and if the quotient is strictly less than -231, then return -231.


```python
Example 1:

Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = 3.33333.. which is truncated to 3.
Example 2:

Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = -2.33333.. which is truncated to -2.
```

```python
class Solution:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        positive = (dividend < 0) is (divisor < 0)
        dividend, divisor, res = abs(dividend), abs(divisor), 0
        while dividend >= divisor:
            temp, i = divisor, 1
            while dividend >= temp:
                dividend -= temp
                res += i
                i <<= 1
                temp <<= 1
        if not positive: res = -res
        return min(max(-2 ** 31, res), 2 ** 31 - 1)
```

## 30. Substring with Concatenation of All Words H


You are given a string s and an array of strings words. All the strings of words are of the same length.

A concatenated substring in s is a substring that contains all the strings of any permutation of words concatenated.

For example, if words = ["ab","cd","ef"], then "abcdef", "abefcd", "cdabef", "cdefab", "efabcd", and "efcdab" are all concatenated strings. "acdbef" is not a concatenated substring because it is not the concatenation of any permutation of words.
Return the starting indices of all the concatenated substrings in s. You can return the answer in any order.




```python
Example 1:

Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Since words.length == 2 and words[i].length == 3, the concatenated substring has to be of length 6.
The substring starting at 0 is "barfoo". It is the concatenation of ["bar","foo"] which is a permutation of words.
The substring starting at 9 is "foobar". It is the concatenation of ["foo","bar"] which is a permutation of words.
The output order does not matter. Returning [9,0] is fine too.
Example 2:

Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
Explanation: Since words.length == 4 and words[i].length == 4, the concatenated substring has to be of length 16.
There is no substring of length 16 is s that is equal to the concatenation of any permutation of words.
We return an empty array.
Example 3:

Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
Explanation: Since words.length == 3 and words[i].length == 3, the concatenated substring has to be of length 9.
The substring starting at 6 is "foobarthe". It is the concatenation of ["foo","bar","the"] which is a permutation of words.
The substring starting at 9 is "barthefoo". It is the concatenation of ["bar","the","foo"] which is a permutation of words.
The substring starting at 12 is "thefoobar". It is the concatenation of ["the","foo","bar"] which is a permutation of words.
```

```python
class Solution:
    def findSubstring(self, s, words):
        if not s or not words: return []
        cnt, l_words, l_word, cnt_words, res = collections.Counter(words), len(words[0]) * len(words), len(words[0]), len(words), []
        for i in range(len(s) - l_words + 1):
            cur, j = dict(cnt), i
            for _ in range(cnt_words):
                w = s[j:j + l_word]
                if w in cur:
                    if cur[w] == 1: cur.pop(w)
                    else: cur[w] -= 1
                else: break
                j += l_word
            if not cur: res += i,
        return res
```

## 31. Next Permutation M


A permutation of an array of integers is an arrangement of its members into a sequence or linear order.

For example, for arr = [1,2,3], the following are all the permutations of arr: [1,2,3], [1,3,2], [2, 1, 3], [2, 3, 1], [3,1,2], [3,2,1].
The next permutation of an array of integers is the next lexicographically greater permutation of its integer. More formally, if all the permutations of the array are sorted in one container according to their lexicographical order, then the next permutation of that array is the permutation that follows it in the sorted container. If such arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

For example, the next permutation of arr = [1,2,3] is [1,3,2].
Similarly, the next permutation of arr = [2,3,1] is [3,1,2].
While the next permutation of arr = [3,2,1] is [1,2,3] because [3,2,1] does not have a lexicographical larger rearrangement.
Given an array of integers nums, find the next permutation of nums.

The replacement must be in place and use only constant extra memory.


```python
Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]
Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]
Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]
```

```python
class Solution:
    def nextPermutation(self, nums):
        perm, l = False, len(nums) - 2
        while 0 <= l:
            r = len(nums) - 1  
            while l < r and nums[r] <= nums[l]: 
                r -= 1
            if r <= l: 
                l -= 1
            else:
                nums[l], nums[l + 1:], perm = nums[r], sorted(nums[l + 1:r] + [nums[l]] + nums[r + 1:]), True
                break
        if not perm: nums.sort()
```

## 32. Longest Valid Parentheses H


Given a string containing just the characters '(' and ')', return the length of the longest valid (well-formed) parentheses substring.


```python
Example 1:

Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
Example 2:

Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
Example 3:

Input: s = ""
Output: 0
```

```python
class Solution:
    def longestValidParentheses(self, s):
        stack, mx = [], 0
        for i, c in enumerate(s):
            if c == ")" and stack and s[stack[-1]] == "(": stack.pop()
            else: stack.append(i)
        stack = [-1] + stack + [len(s)]
        for i1, i2 in zip(stack, stack[1:]): mx = max(mx, i2 - i1 - 1)
        return mx if len(stack) > 2 else len(s)
```

## 33. Search in Rotated Sorted Array M


There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.


```python
Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
Example 3:

Input: nums = [1], target = 0
Output: -1
```

```python
class Solution:
    def search(self, nums, target):
        l, r = 0, len(nums) - 1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] == target: 
                return mid
            elif sum((target < nums[l], nums[l] <= nums[mid], nums[mid] < target)) == 2: 
                l = mid + 1
            else: 
                r = mid - 1
        return -1
```

## 34. Find First and Last Position of Element in Sorted Array M


Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

You must write an algorithm with O(log n) runtime complexity.


```python
Example 1:

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
Example 2:

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
Example 3:

Input: nums = [], target = 0
Output: [-1,-1]
```

```python
class Solution(object):
    def searchRange(self, nums, target):
        l, r = bisect.bisect_left(nums, target), bisect.bisect_right(nums, target) - 1
        return [l, r] if 0 <= l <= r else [-1, -1]
```

## 35. Search Insert Position E


Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.


```python
Example 1:

Input: nums = [1,3,5,6], target = 5
Output: 2
Example 2:

Input: nums = [1,3,5,6], target = 2
Output: 1
Example 3:

Input: nums = [1,3,5,6], target = 7
Output: 4
```

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        return bisect.bisect_left(nums, target)
```

## 36. Valid Sudoku E


Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
Note:

A Sudoku board (partially filled) could be valid but is not necessarily solvable.
Only the filled cells need to be validated according to the mentioned rules.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
```python
Example 1:

Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
Example 2:

Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

```python
class Solution:
    def isValidSudoku(self, board):
        rows, cols, triples = collections.defaultdict(set), collections.defaultdict(set), collections.defaultdict(set)
        for i, row in enumerate(board):
            for j, c in enumerate(row):
                if c != "." and c in rows[i] or c in cols[j] or c in triples[(i //3, j // 3)]: 
                    return False
                elif c != ".": 
                    rows[i].add(c); cols[j].add(c); triples[(i // 3, j // 3)].add(c)
        return True
```

## 37. Sudoku Solver H


Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy all of the following rules:

Each of the digits 1-9 must occur exactly once in each row.
Each of the digits 1-9 must occur exactly once in each column.
Each of the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.
The '.' character indicates empty cells.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)
![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)
```python
Example 1:


Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:
```

```python
class Solution:
    def solveSudoku(self, board):
        rows, cols, triples, visit = collections.defaultdict(set), collections.defaultdict(set), collections.defaultdict(set), collections.deque([])
        for r in range(9):
            for c in range(9):
                if board[r][c] != ".":
                    rows[r].add(board[r][c])
                    cols[c].add(board[r][c])
                    triples[(r // 3, c // 3)].add(board[r][c])
                else:
                    visit.append((r, c))
        def dfs():
            if not visit:
                return True
            r, c = visit[0]
            t = (r // 3, c // 3)
            for dig in {"1", "2", "3", "4", "5", "6", "7", "8", "9"}:
                if dig not in rows[r] and dig not in cols[c] and dig not in triples[t]:
                    board[r][c] = dig
                    rows[r].add(dig)
                    cols[c].add(dig)
                    triples[t].add(dig)
                    visit.popleft()
                    if dfs():
                        return True
                    else:
                        board[r][c] = "."
                        rows[r].discard(dig)
                        cols[c].discard(dig)
                        triples[t].discard(dig)
                        visit.appendleft((r, c))
            return False
        dfs()
```

## 38. Count and Say M


The count-and-say sequence is a sequence of digit strings defined by the recursive formula:

countAndSay(1) = "1"
countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.
To determine how you "say" a digit string, split it into the minimal number of substrings such that each substring contains exactly one unique digit. Then for each substring, say the number of digits, then say the digit. Finally, concatenate every said digit.

For example, the saying and conversion for digit string "3322251":


Given a positive integer n, return the nth term of the count-and-say sequence.

![](https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg)
```python
Example 1:

Input: n = 1
Output: "1"
Explanation: This is the base case.
Example 2:

Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

```python
class Solution:
    def countAndSay(self, n):
        curr = "1"
        for i in range(n - 1):
            tmp, cnt = "", 1
            for j, c in enumerate(curr):
                if j > 0 and curr[j - 1] == c: 
                    cnt += 1
                elif j > 0: 
                    tmp += str(cnt) + curr[j - 1]
                    cnt = 1
                if j == len(curr) - 1: 
                    tmp += str(cnt) + curr[j] 
            curr = tmp
        return curr
```

## 39. Combination Sum M


Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.


```python
Example 1:

Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
Example 2:

Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
Example 3:

Input: candidates = [2], target = 1
Output: []
```

```python
class Solution:
    def combinationSum(self, c, t):
        res, stack, n = [], [(0, [], 0)], len(c)
        while stack:
            sm, tmp, r = stack.pop()
            for i in range(r, n):
                if sm + c[i] < t: 
                    stack.append((sm + c[i], tmp + [c[i]], i))
                elif sm + c[i] == t: 
                    res.append(tmp + [c[i]])
        return res
```

## 40. Combination Sum II M


Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.


```python
Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
Example 2:

Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

```python
class Solution: 
    def combinationSum2(self, candidates, target):   
        res = []
        self.dfs(sorted(candidates), target, 0, [], res)
        return res
    def dfs(self, nums, target, index, path, res):    
        if target < 0:
            return 
        if target == 0 and path not in res:
            res.append(path)
            return 
        for i in range(index, len(nums)):
            if i>1 and nums[i] == nums[i-1]:
                continue
            self.dfs(nums[:i] + nums[i+1:], target-nums[i], i, path+[nums[i]], res)
```

## 41. First Missing Positive H


Given an unsorted integer array nums, return the smallest missing positive integer.

You must implement an algorithm that runs in O(n) time and uses constant extra space.


```python
Example 1:

Input: nums = [1,2,0]
Output: 3
Explanation: The numbers in the range [1,2] are all in the array.
Example 2:

Input: nums = [3,4,-1,1]
Output: 2
Explanation: 1 is in the array but 2 is missing.
Example 3:

Input: nums = [7,8,9,11,12]
Output: 1
Explanation: The smallest positive integer 1 is missing.
```

```python
class Solution:
    def firstMissingPositive(self, nums: List[int], res: int = 1) -> int:
        for num in sorted(nums):
            res += num == res
        return res
        
```

## 42. Trapping Rain Water H 


Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
```python
Example 1:

Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
Example 2:

Input: height = [4,2,0,3,2,5]
Output: 9
```

```python
class Solution:
    def trap(self, height):
        res, left, l, r = 0, {}, 0, 0
        for i, h in enumerate(height):
            left[i] = l
            if h > l: 
                l = h
        for i in range(len(height) - 1, -1, -1):
            roof = min(left[i] , r)
            if roof > height[i]:
                res += roof - height[i]
            if height[i] > r:
                r = height[i]
        return res
```

## 43. Multiply Strings M


Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.

Note: You must not use any built-in BigInteger library or convert the inputs to integer directly.


```python
Example 1:

Input: num1 = "2", num2 = "3"
Output: "6"
Example 2:

Input: num1 = "123", num2 = "456"
Output: "56088"
```

```python
class Solution:
    def multiply(self, num1, num2):
        dic, l1, l2 = {str(i): i for i in range(10)}, len(num1) - 1, len(num2) - 1
        return str(sum([dic[n1] * (10**(l1-i)) for i, n1 in enumerate(num1)]) * sum([dic[n2] * (10**(l2-j)) for j, n2 in enumerate(num2)]))
```

## 44. Wildcard Matching H


Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*' where:

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).


```python
Example 1:

Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input: s = "aa", p = "*"
Output: true
Explanation: '*' matches any sequence.
Example 3:

Input: s = "cb", p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

```python
class Solution:
    def isMatch(self, s, p):
        sp = pp = match = 0
        star = -1
        while sp < len(s):
            if (pp < len(p) and (s[sp] == p[pp] or p[pp] == '?')):
                sp +=1
                pp +=1
            elif pp < len(p) and p[pp] == '*':
                star = pp
                match = sp
                pp +=1
            elif star != -1:
                pp = star + 1
                match +=1
                sp = match
            else:
                return False
        while(pp < len(p) and p[pp] == '*'):
            pp += 1
        return pp == len(p)
```

## 45. Jump Game II M


You are given a 0-indexed array of integers nums of length n. You are initially positioned at nums[0].

Each element nums[i] represents the maximum length of a forward jump from index i. In other words, if you are at nums[i], you can jump to any nums[i + j] where:

0 <= j <= nums[i] and
i + j < n
Return the minimum number of jumps to reach nums[n - 1]. The test cases are generated such that you can reach nums[n - 1].


```python
Example 1:

Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: nums = [2,3,0,1,4]
Output: 2
```

```python
class Solution:
    def jump(self, nums):
        last = cur = jump = i = 0
        while cur < len(nums) - 1:
            while i <= last:
                if i + nums[i] > cur: cur = i + nums[i]
                i += 1
            last = cur
            jump += 1
        return jump
```

## 46. Permutations M


Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.


```python
Example 1:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Example 2:

Input: nums = [0,1]
Output: [[0,1],[1,0]]
Example 3:

Input: nums = [1]
Output: [[1]]
```

```python
class Solution:
    def permute(self, nums): return list(itertools.permutations(nums))
```

## 47. Permutations II M


Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.


```python
Example 1:

Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
Example 2:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

```python
class Solution:
    def permuteUnique(self, nums):
        dic = set()
        for p in itertools.permutations(nums):
            if p not in dic: 
                dic.add(p)
        return list(dic)
```

## 48. Rotate Image M


You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)
![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)
```python
Example 1:

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
Example 2:

Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

```python
class Solution:
    def rotate(self, matrix):
        matrix[:] = [[row[i] for row in matrix[::-1]] for i in range(len(matrix))]
```

## 49. Group Anagrams M


Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.


```python
Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
Example 2:

Input: strs = [""]
Output: [[""]]
Example 3:

Input: strs = ["a"]
Output: [["a"]]
```

```python
class Solution:
    def groupAnagrams(self, strs):
        dic = collections.defaultdict(list)
        for s in strs: 
            dic["".join(sorted(s))].append(s)
        return list(dic.values())
```

## 50. Pow(x, n) M


Implement pow(x, n), which calculates x raised to the power n (i.e., xn).


```python
Example 1:

Input: x = 2.00000, n = 10
Output: 1024.00000
Example 2:

Input: x = 2.10000, n = 3
Output: 9.26100
Example 3:

Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            n *= -1
            x = 1 / x
        elif not n:
            return 1
        half = self.myPow(x, n // 2)
        return x * half * half if n % 2 else half * half
```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

## 



```python

```

```python

```

