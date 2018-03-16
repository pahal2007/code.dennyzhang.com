# Leetcode: Group Shifted Strings     :BLOG:Medium:


---

Group Shifted Strings  

---

Similar Problems:  
-   [Group Anagrams](https://brain.dennyzhang.com/group-anagrams)
-   [Tag: #hashmap](https://brain.dennyzhang.com/tag/hashmap)

---

Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep "shifting" which forms the sequence:  

    "abc" -> "bcd" -> ... -> "xyz"

Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.  

For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"],  
A solution is:  

    [
      ["abc","bcd","xyz"],
      ["az","ba"],
      ["acef"],
      ["a","z"]
    ]

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/group-shifted-strings)  

Credits To: [leetcode.com](https://leetcode.com/problems/group-shifted-strings/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: https://brain.dennyzhang.com/group-shifted-strings
    ## Basic Ideas: hashmap
    ##
    ## From ["az", "ba"] we know, it's a rotated shift
    ## The order doesn't matter
    ##
    ## Complexity: Time O(n), Space O(n)
    class Solution:
        def groupStrings(self, strings):
            """
            :type strings: List[str]
            :rtype: List[List[str]]
            """
            import collections
            m = collections.defaultdict(lambda:)
            for string in strings:
                if string == "":
                    m[()].append(string)
                    continue
                # ba -> (0, 25)
                # az -> (0, 25)
                tup = tuple([(ord(ch)-ord(string[0]))%26 for ch in string])
                m[tup].append(string)
            return [m[key] for key in m]