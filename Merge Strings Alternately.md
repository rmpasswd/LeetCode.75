[link](https://leetcode.com/problems/merge-strings-alternately/description/?source=submission-ac)
> You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.
  Return the merged string.

>  **Input**: word1 = "ab", word2 = "pqrs"
  **Output**: "apbqrs"
  **Explanation**: Notice that as word2 is longer, "rs" is appended to the end.

### Solution in Golang
```go
func mergeAlternately(word1 string, word2 string) string {
	var i int
	var merged string
	for i = 0; i < len(word2) && i < len(word1); i++ {
		merged += string(word1[i]) + string(word2[i])
	}
	merged += word2[i:] + word1[i:]
	return merged
}
```

- From Editorial:
- `return ''.join(c for pair in zip_longest(word1, word2, fillvalue='') for c in pair)`. This uses python itertools package.
-  Using built-in zip function=>
-  zip function lazy loads the tuples, we will get the generator object only this way: `print(c for pair in list(zip("abc","word2")) for c in pair )`
-
- ```python
   for pair in list(zip("abc","word2")):
        for c in pair:
            print(c) # prints the charcter individually
  #equivalent one-line=>
  print(c for pair in list(zip("abc","word2")) for c in pair )
  # prints this: <generator object mergeAlternately.<locals>.<genexpr> at 0x000002BFD5B14820>
   ```
- zip itself is a generator expression. See the hint "yield" below... ![image](https://github.com/user-attachments/assets/933800c5-ef22-4785-b247-f36c4e4ea81d)
- `print(generator_expression)` prints the generator object itself because print() does not iterate over it. **this is why** the code block above printed the generator object. But worked fine when we did the iteration 'manually'

- `"".join(generator_expression)` **iterates** over the generator, collects its items, and produces a string. Thus this works: `print("".join(c for pair in list(zip("abc","word2")) for c in pair )) # prints awbocr`
### Solution in Python3
*with unnecessary sugar
```python
def mergeAlternately(self, word1: str, word2: str) -> str:
  return "".join(c for pair in list(zip(word1,word2)) for c in pair ) \
                    + {True:word1[len(word2):], False: word2[len(word1):]} [len(word1) > len(word2)]
```


  
- 
