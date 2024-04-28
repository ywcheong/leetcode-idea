# substring-with-concatenation-of-all-words
This is the step-by-step solution to solve the following problem on Leetcode.

* Substring with Concatenation of All Words - *Top Interview 150*
  * https://leetcode.com/problems/substring-with-concatenation-of-all-words

To solve the problem, we need an external class which handles the current total count of the word. This class utilizes hash to achieve `O(1)` time for pushing/poping.

To elaborate in details, this code conduct "segmentization", starting from the given `start_pos` of the given word s, by slicing it with the given word length `len(words[0])`. For example:

```
barfoothefoobarman : segment size 3, start from 0
> bar / foo / the / foo / bar / man

barfoothefoobarman : segment size 3, start from 1
> arf / oot / hef / oob / arm / an
```

The auxilary class, `WordCounter` assists using the sliding-window method in this problem. `WordCounter` class consumes a constant number of segments, and compare it with given `words` list. If the set of the consumed segments is equivalent to the `words` list, then it records the first position of the segments to the `result` list. Thanks to the hashing, this class's time complexity is `O(1)` on pushing and poping, and `O(len(words))` on comparing.

By applying this method from the starting position of 0 to `len(words[0]) - 1`, we can get a suitable result.

The following python code is the implementation.

```python
def get_segment(s, pos, word_length):
    return s[pos:pos+word_length]

class WordCounter:
    def __init__(self, words):
        self.word_count = dict()
        self.total_count = 0

        for word in words:
            self.pop(word)
    
    def push(self, s):
        if s == "":
            return
        if s not in self.word_count:
            self.word_count[s] = 1
        else:
            self.word_count[s] += 1
        self.total_count += 1
    
    def pop(self, s):
        if s == "":
            return
        if s not in self.word_count:
            self.word_count[s] = -1
        else:
            self.word_count[s] -= 1
        
    def is_zero(self):
        for key in self.word_count:
            if self.word_count[key] != 0:
                return False
        return True

class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        result = []
        word_count = len(words)
        word_length = len(words[0])
        substring_length = word_count * word_length

        for start_pos in range(word_length):
            counter = WordCounter(words)

            # adding stage: [start_pos : start_pos + substring_length]
            for pos in range(start_pos, start_pos + substring_length, word_length):
                pushing_segment = get_segment(s, pos, word_length)
                counter.push(pushing_segment)
            
            if counter.is_zero():
                result.append(start_pos)
            
            # moving stage: [pos : pos + substring_length] / pos window : word_length
            for pos in range(start_pos + substring_length, len(s), word_length):
                pushing_segment = get_segment(s, pos, word_length)
                poping_segment = get_segment(s, pos - substring_length, word_length)
                counter.push(pushing_segment)
                counter.pop(poping_segment)
                if counter.is_zero():
                    result.append(pos - substring_length + word_length)
            
        return sorted(result)
```
