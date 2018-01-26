# Leetcode: Reconstruct Original Digits from English     :BLOG:Amusing:


---

Reconstruct Original Digits from English  

---

Given a non-empty string containing an out-of-order English representation of digits 0-9, output the digits in ascending order.  

Note:  
Input contains only lowercase English letters.  
Input is guaranteed to be valid and can be transformed to its original digits. That means invalid inputs such as "abc" or "zerone" are not permitted.  
Input length is less than 50,000.  

    Example 1:
    Input: "owoztneoer"
    
    Output: "012"

    Example 2:
    Input: "fviefuro"
    
    Output: "45"

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/reconstruct-original-digits-from-english)  

Credits To: [leetcode.com](https://leetcode.com/problems/reconstruct-original-digits-from-english/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: http://brain.dennyzhang.com/reconstruct-original-digits-from-english
    ## Basic Ideas: Nature of english numbers.
    ##         'z': ['0']
    ##         'u': ['4'],
    ##         'w': ['2'],
    ##         'g': ['8'],
    ##         'x': ['6']
    ##         'h': ['3', '8'],
    ##         's': ['7', '6'],
    ##         'r': ['0', '3', '4'],
    ##         'v': ['5', '7'],
    ##         'f': ['5', '4'],
    ##         't': ['3', '2', '8'],
    ##         'o': ['0', '1', '2', '4'],
    ##         'r': ['0', '3', '4']
    ##         'i': ['5', '6', '9', '8'],
    ##         'n': ['1', '7', '9', '9'],
    ##         'e': ['0', '1', '3', '3', 5', '7', '7', '9', '8'],
    ## Complexity: Time O(n), Space O(1)
    class Solution(object):
        def originalDigits(self, s):
            """
            :type s: str
            :rtype: str
            """
            l = [0]*10
            for ch in s:
                if ch == 'z': l[0] += 1
                if ch == 'w': l[2] += 1
                if ch == 'u': l[4] += 1
                if ch == 'x': l[6] += 1
                if ch == 'g': l[8] += 1
                if ch == 's': l[7] += 1 # 7 - 6
                if ch == 'f': l[5] += 1 # 5-4
                if ch == 'r': l[3] += 1 # 3-4-0
                if ch == 'o': l[1] += 1 # 1-0-2-4                
                if ch == 'i': l[9] += 1 # 9-5-6-8
    
            l[7] = l[7] - l[6]
            l[5] = l[5] - l[4]
            l[3] = l[3] - l[4] - l[0]
            l[1] = l[1] - l[0] - l[2] - l[4]
            l[9] = l[9] - l[5] - l[6] - l[8]
            res = ''
            for i in xrange(10):
                if l[i] != 0:
                    res = '%s%s' % (res, str(i)*l[i])
            return res
    
    s = Solution()
    print s.originalDigits('owoztneoer') # 012
    print s.originalDigits('fviefuro') # 45
    print s.originalDigits('xsi') # 6
    print s.originalDigits('nnei') # 9