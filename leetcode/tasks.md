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

## 51. N-Queens H

The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle. You may return the answer in any order.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space, respectively.
![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)
```python
Example 1:

Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
Example 2:

Input: n = 1
Output: [["Q"]]
```

```python

```

## 52. N-Queens II H
The n-queens puzzle is the problem of placing n queens on an n x n chessboard such that no two queens attack each other.

Given an integer n, return the number of distinct solutions to the n-queens puzzle.
![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```python
Example 1:

Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.
Example 2:

Input: n = 1
Output: 1
```

```python

```

## 53. Maximum Subarray

Given an integer array nums, find the subarray which has the largest sum and return its sum.

```python
Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Example 2:

Input: nums = [1]
Output: 1
Example 3:

Input: nums = [5,4,-1,7,8]
Output: 23
```

```python

```

## 54. Spiral Matrix M

Given an m x n matrix, return all elements of the matrix in spiral order.
![](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)
![](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)
```python
Example 1:

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
Example 2:

Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

```python

```

## 55. Jump Game M

You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.

Return true if you can reach the last index, or false otherwise.

```python
Example 1:

Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

```python

```

## 56. Merge Intervals M

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

```python
Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

```python

```

## 57. Insert Interval M

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

```python
Example 1:

Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
Example 2:

Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

```python

```

## 58. Length of Last Word E

Given a string s consisting of words and spaces, return the length of the last word in the string.

A word is a maximal substring consisting of non-space characters only.

```python
Example 1:

Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
Example 2:

Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
Example 3:

Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

```python

```

## 59. Spiral Matrix II M

Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

![](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```python
Example 1:

Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
Example 2:

Input: n = 1
Output: [[1]]
```

```python

```

## 60. Permutation Sequence H

The set [1, 2, 3, ..., n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

```python
Example 1:

Input: n = 3, k = 3
Output: "213"
Example 2:

Input: n = 4, k = 9
Output: "2314"
Example 3:

Input: n = 3, k = 1
Output: "123"
```

```python

```

## 61. Rotate List M

Given the head of a linked list, rotate the list to the right by k places.

![](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)
![](https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg)

```python
Example 1:

Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
Example 2:

Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

```python

```

## 62. Unique Paths M

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 109.

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```python
Example 1:

Input: m = 3, n = 7
Output: 28
Example 2:

Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```

```python

```

## 63. Unique Paths II M

You are given an m x n integer array grid. There is a robot initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

An obstacle and space are marked as 1 or 0 respectively in grid. A path that the robot takes cannot include any square that is an obstacle.

Return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The testcases are generated so that the answer will be less than or equal to 2 * 109.
![](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)
![](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)
```python
Example 1:

Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
Example 2:

Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

```python

```

## 64. Minimum Path Sum M

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

![](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```python
Example 1:

Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
Example 2:

Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

```python

```

## 65. Valid Number

A valid number can be split up into these components (in order):

A decimal number or an integer.
(Optional) An 'e' or 'E', followed by an integer.
A decimal number can be split up into these components (in order):

(Optional) A sign character (either '+' or '-').
One of the following formats:
One or more digits, followed by a dot '.'.
One or more digits, followed by a dot '.', followed by one or more digits.
A dot '.', followed by one or more digits.
An integer can be split up into these components (in order):

(Optional) A sign character (either '+' or '-').
One or more digits.
For example, all the following are valid numbers: ["2", "0089", "-0.1", "+3.14", "4.", "-.9", "2e10", "-90E3", "3e+7", "+6e-1", "53.5e93", "-123.456e789"], while the following are not valid numbers: ["abc", "1a", "1e", "e3", "99e2.5", "--6", "-+3", "95a54e53"].

Given a string s, return true if s is a valid number.

```python
Example 1:

Input: s = "0"
Output: true
Example 2:

Input: s = "e"
Output: false
Example 3:

Input: s = "."
Output: false
```

```python

```

## 66. Plus One E

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

```python
Example 1:

Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
Example 2:

Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
Example 3:

Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```

```python

```

## 67. Add Binary

Given two binary strings a and b, return their sum as a binary string.

```python
Example 1:

Input: a = "11", b = "1"
Output: "100"
Example 2:

Input: a = "1010", b = "1011"
Output: "10101"
```

```python

```

## 68. Text Justification

Given an array of strings words and a width maxWidth, format the text such that each line has exactly maxWidth characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly maxWidth characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

Note:

A word is defined as a character sequence consisting of non-space characters only.
Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
The input array words contains at least one word.

```python
Example 1:

Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
Example 2:

Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
Example 3:

Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

```python

```

## 69. Sqrt(x) E

Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.

You must not use any built-in exponent function or operator.

For example, do not use pow(x, 0.5) in c++ or x ** 0.5 in python.

```python
Example 1:

Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.
Example 2:

Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
```

```python

```

## 70. Climbing Stairs E

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

```python
Example 1:

Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
Example 2:

Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

```python

```

## 71. Simplify Path

Given a string path, which is an absolute path (starting with a slash '/') to a file or directory in a Unix-style file system, convert it to the simplified canonical path.

In a Unix-style file system, a period '.' refers to the current directory, a double period '..' refers to the directory up a level, and any multiple consecutive slashes (i.e. '//') are treated as a single slash '/'. For this problem, any other format of periods such as '...' are treated as file/directory names.

The canonical path should have the following format:

The path starts with a single slash '/'.
Any two directories are separated by a single slash '/'.
The path does not end with a trailing '/'.
The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period '.' or double period '..')
Return the simplified canonical path.

```python
Example 1:

Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
Example 2:

Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
Example 3:

Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

```python

```

## 72. Edit Distance H

Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

Insert a character
Delete a character
Replace a character


```python
Example 1:

Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
Example 2:

Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

```python

```

## 73. Set Matrix Zeroes M

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.
![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)
![](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)
```python
Example 1:

Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
Example 2:

Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

```python

```


## 74. Search a 2D Matrix M

Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)
![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)
```python
Example 1:

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
Example 2:

Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

```python

```


## 75. Sort Colors M

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

```python
Example 1:

Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Example 2:

Input: nums = [2,0,1]
Output: [0,1,2]
```

```python

```


## 76. Minimum Window Substring M

Given two strings s and t of lengths m and n respectively, return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

```python
Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```

```python

```


## 77. Combinations M

Given two integers n and k, return all possible combinations of k numbers chosen from the range [1, n].

You may return the answer in any order.

```python
Example 1:

Input: n = 4, k = 2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Explanation: There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.
Example 2:

Input: n = 1, k = 1
Output: [[1]]
Explanation: There is 1 choose 1 = 1 total combination.
```

```python

```


## 78. Subsets M

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

```python
Example 1:

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
Example 2:

Input: nums = [0]
Output: [[],[0]]
```

```python

```


## 79. Word Search M

Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.
![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)
![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)
```python
Example 1:

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
Example 2:

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

```python

```


## 80. Remove Duplicates from Sorted Array II M

Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

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

Input: nums = [1,1,1,2,2,3]
Output: 5, nums = [1,1,2,2,3,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
Example 2:

Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3,_,_]
Explanation: Your function should return k = 7, with the first seven elements of nums being 0, 0, 1, 1, 2, 3 and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

```python

```


## 81. Search in Rotated Sorted Array II M

There is an integer array nums sorted in non-decreasing order (not necessarily with distinct values).

Before being passed to your function, nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,4,4,5,6,6,7] might be rotated at pivot index 5 and become [4,5,6,6,7,0,1,2,4,4].

Given the array nums after the rotation and an integer target, return true if target is in nums, or false if it is not in nums.

You must decrease the overall operation steps as much as possible.

```python
Example 1:

Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
Example 2:

Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

```python

```


## 82. Remove Duplicates from Sorted List II M

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.
![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)
![](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)
```python
Example 1:

Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
Example 2:

Input: head = [1,1,1,2,3]
Output: [2,3]
```

```python

```


## 83. Remove Duplicates from Sorted List E

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.
![](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)
![](https://assets.leetcode.com/uploads/2021/01/04/list2.jpg)
```python
Example 1:

Input: head = [1,1,2]
Output: [1,2]
Example 2:

Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

```python

```


## 84. Largest Rectangle in Histogram H

Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.
![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)
![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)
```python
Example 1:

Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
Example 2:

Input: heights = [2,4]
Output: 4
```

```python

```


## 85. Maximal Rectangle H

Given a rows x cols binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.
![](https://assets.leetcode.com/uploads/2020/09/14/maximal.jpg)
```python
Example 1:

Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 6
Explanation: The maximal rectangle is shown in the above picture.
Example 2:

Input: matrix = [["0"]]
Output: 0
Example 3:

Input: matrix = [["1"]]
Output: 1
```

```python

```


## 86. Partition List

Given the head of a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.
![](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)
```python
Example 1:

Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
Example 2:

Input: head = [2,1], x = 2
Output: [1,2]
```

```python

```


## 87. Scramble String H

We can scramble a string s to get a string t using the following algorithm:

If the length of the string is 1, stop.
If the length of the string is > 1, do the following:
Split the string into two non-empty substrings at a random index, i.e., if the string is s, divide it to x and y where s = x + y.
Randomly decide to swap the two substrings or to keep them in the same order. i.e., after this step, s may become s = x + y or s = y + x.
Apply step 1 recursively on each of the two substrings x and y.
Given two strings s1 and s2 of the same length, return true if s2 is a scrambled string of s1, otherwise, return false.

```python
Example 1:

Input: s1 = "great", s2 = "rgeat"
Output: true
Explanation: One possible scenario applied on s1 is:
"great" --> "gr/eat" // divide at random index.
"gr/eat" --> "gr/eat" // random decision is not to swap the two substrings and keep them in order.
"gr/eat" --> "g/r / e/at" // apply the same algorithm recursively on both substrings. divide at random index each of them.
"g/r / e/at" --> "r/g / e/at" // random decision was to swap the first substring and to keep the second substring in the same order.
"r/g / e/at" --> "r/g / e/ a/t" // again apply the algorithm recursively, divide "at" to "a/t".
"r/g / e/ a/t" --> "r/g / e/ a/t" // random decision is to keep both substrings in the same order.
The algorithm stops now, and the result string is "rgeat" which is s2.
As one possible scenario led s1 to be scrambled to s2, we return true.
Example 2:

Input: s1 = "abcde", s2 = "caebd"
Output: false
Example 3:

Input: s1 = "a", s2 = "a"
Output: true
```

```python

```


## 88. Merge Sorted Array E

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

```python
Example 1:

Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
Example 2:

Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
Example 3:

Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```

```python

```


## 89. Gray Code M

An n-bit gray code sequence is a sequence of 2n integers where:

Every integer is in the inclusive range [0, 2n - 1],
The first integer is 0,
An integer appears no more than once in the sequence,
The binary representation of every pair of adjacent integers differs by exactly one bit, and
The binary representation of the first and last integers differs by exactly one bit.
Given an integer n, return any valid n-bit gray code sequence.

```python
Example 1:

Input: n = 2
Output: [0,1,3,2]
Explanation:
The binary representation of [0,1,3,2] is [00,01,11,10].
- 00 and 01 differ by one bit
- 01 and 11 differ by one bit
- 11 and 10 differ by one bit
- 10 and 00 differ by one bit
[0,2,3,1] is also a valid gray code sequence, whose binary representation is [00,10,11,01].
- 00 and 10 differ by one bit
- 10 and 11 differ by one bit
- 11 and 01 differ by one bit
- 01 and 00 differ by one bit
Example 2:

Input: n = 1
Output: [0,1]
```

```python

```


## 90. Subsets II M

Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

```python
Example 1:

Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
Example 2:

Input: nums = [0]
Output: [[],[0]]
```

```python

```


## 91. Decode Ways M

A message containing letters from A-Z can be encoded into numbers using the following mapping:

'A' -> "1"
'B' -> "2"
...
'Z' -> "26"
To decode an encoded message, all the digits must be grouped then mapped back into letters using the reverse of the mapping above (there may be multiple ways). For example, "11106" can be mapped into:

"AAJF" with the grouping (1 1 10 6)
"KJF" with the grouping (11 10 6)
Note that the grouping (1 11 06) is invalid because "06" cannot be mapped into 'F' since "6" is different from "06".

Given a string s containing only digits, return the number of ways to decode it.

The test cases are generated so that the answer fits in a 32-bit integer.

```python
Example 1:

Input: s = "12"
Output: 2
Explanation: "12" could be decoded as "AB" (1 2) or "L" (12).
Example 2:

Input: s = "226"
Output: 3
Explanation: "226" could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
Example 3:

Input: s = "06"
Output: 0
Explanation: "06" cannot be mapped to "F" because of the leading zero ("6" is different from "06").
```

```python

```


## 92. Reverse Linked List II M

Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.
![](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```python
Example 1:

Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
Example 2:

Input: head = [5], left = 1, right = 1
Output: [5]
```

```python

```


## 93. Restore IP Addresses M

A valid IP address consists of exactly four integers separated by single dots. Each integer is between 0 and 255 (inclusive) and cannot have leading zeros.

For example, "0.1.2.201" and "192.168.1.1" are valid IP addresses, but "0.011.255.245", "192.168.1.312" and "192.168@1.1" are invalid IP addresses.
Given a string s containing only digits, return all possible valid IP addresses that can be formed by inserting dots into s. You are not allowed to reorder or remove any digits in s. You may return the valid IP addresses in any order.

```python
Example 2:

Input: s = "0000"
Output: ["0.0.0.0"]
Example 3:

Input: s = "101023"
Output: ["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

```python

```


## 94. Binary Tree Inorder Traversal E

Given the root of a binary tree, return the inorder traversal of its nodes' values.
![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```python
Example 1:

Input: root = [1,null,2,3]
Output: [1,3,2]
Example 2:

Input: root = []
Output: []
Example 3:

Input: root = [1]
Output: [1]
```

```python

```


## 95. Unique Binary Search Trees II M

Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.
![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```python
Example 1:

Input: n = 3
Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
Example 2:

Input: n = 1
Output: [[1]]
```

```python

```


## 96. Unique Binary Search Trees M

Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.
![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```python
Example 1:

Input: n = 3
Output: 5
Example 2:

Input: n = 1
Output: 1
```

```python

```


## 97. Interleaving String M

Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where s and t are divided into n and m substrings respectively, such that:

s = s1 + s2 + ... + sn
t = t1 + t2 + ... + tm
|n - m| <= 1
The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...
Note: a + b is the concatenation of strings a and b.
![](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

```python
Example 1:


Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
Explanation: One way to obtain s3 is:
Split s1 into s1 = "aa" + "bc" + "c", and s2 into s2 = "dbbc" + "a".
Interleaving the two splits, we get "aa" + "dbbc" + "bc" + "a" + "c" = "aadbbcbcac".
Since s3 can be obtained by interleaving s1 and s2, we return true.
Example 2:

Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
Explanation: Notice how it is impossible to interleave s2 with any other string to obtain s3.
Example 3:

Input: s1 = "", s2 = "", s3 = ""
Output: true
```

```python

```


## 98. Validate Binary Search Tree

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)
![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```python
Example 1:

Input: root = [2,1,3]
Output: true
Example 2:

Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

```python

```


## 99. Recover Binary Search Tree M

You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.
![](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)
![](https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg)
```python
Example 1:


Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.
Example 2:


Input: root = [3,1,4,null,null,2]
Output: [2,1,4,null,null,3]
Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.
```

```python

```


## 100. Same Tree E

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.
![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)
![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)
![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)
```python
Example 1:

Input: p = [1,2,3], q = [1,2,3]
Output: true
Example 2:

Input: p = [1,2], q = [1,null,2]
Output: false
Example 3:

Input: p = [1,2,1], q = [1,1,2]
Output: false
```

```python

```


