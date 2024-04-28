# group-anagrams
This is the step-by-step solution to solve the following problem on Leetcode.

* Group Anagrams - *Top Interview 150*
  * https://leetcode.com/problems/group-anagrams

To solve the problem, we need a hashing method.

The main idea is to extract the common key, which is not affected by the character order in the word. To achive the goal, we sorted the character order in the word and use that as a key. This process is implemented as a function `get_key(word)`.

The following python code is the implementation.

```python
def push(group, key, value):
    if key not in group:
        group[key] = [value]
    else:
        group[key].append(value)

def get_key(word):
    word = sorted(list(word))
    key = ""
    for c in word:
        key += c
    return key

class Solution:
    def groupAnagrams(self, str_list: List[str]) -> List[List[str]]:
        group = dict()
        for word in str_list:
            key = get_key(word)
            push(group, key, word)

        # unserialize dict -> list (without key)
        result = []
        for key in group:
            result.append(group[key])
        return result
```
