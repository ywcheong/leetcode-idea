# ransom-note
This is the step-by-step solution to solve the following problem on Leetcode.

* Ransom Note - *Top Interview 150*
  * https://leetcode.com/problems/ransom-note

To solve the problem, we need a hashmap method. By hashing all characters in the `magazine`, we can verify if every character in `ransomNote` by `O(1)` time per character. If `len(magazine) == m` and `len(ransomNote) == n`, this algorithm has linear time of `O(n + m)` time complexity.

The following python code is the implementation.

```python
def increase_one(hashmap, key):
    if key not in hashmap:
        hashmap[key] = 1
    else:
        hashmap[key] += 1

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        magazine_hash = dict()
        for c in magazine:
            increase_one(magazine_hash, c)

        for c in ransomNote:
            if c in magazine_hash and magazine_hash[c] > 0:
                magazine_hash[c] -= 1
            else:
                return False
        return True
```

Alternative solution: just count every characters in each string... (slower but memory-friendly!)

```py
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        for c in ransomNote:
            if ransomNote.count(c) > magazine.count(c):
                return False
        return True
```