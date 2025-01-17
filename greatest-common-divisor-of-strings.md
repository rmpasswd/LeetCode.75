
- My Code:
  
![image](https://github.com/user-attachments/assets/f7fbcf5c-1d55-4d60-aca9-f1b8d6e7f9fe)

```go
func gcdOfStrings(str1 string, str2 string) string {
    if (strings.HasPrefix(str1,str2) || strings.HasPrefix(str2,str1)) == false{
        return ""
    }
    var gcdString string
    len1:= len(str1)
    len2:= len(str2)
    if (len2>len1) { 
        // string2 is larger
        gcdString = str1[:gcd(len2,len1)]
        if (crossmatch(str2, gcdString)) {
            return gcdString
        }
    }else {
        // string1 is larger
        gcdString = str2[:gcd(len2,len1)]
        if (crossmatch(str1, gcdString)) {
            return gcdString
        }
    }
    return ""
}

func gcd(big int, small int) int {

	if (big % small == 0) {
		return small
	}
	return	gcd(small, big % small)	
}
func  crossmatch(bigstr string, gcdstr string) bool {
    for i:=len(gcdstr);i<len(bigstr);i+=len(gcdstr) {

        if (bigstr[i:i+len(gcdstr)] != gcdstr) {
            return false
        }
    }
    return true
}

```


- **Other Robust solutions:**
```go
//Go
func gcdOfStrings(s1 string, s2 string) string {
    if s1 + s2 != s2 + s1 {
        return ""  // this filters out some test cases. For example: str1 = "ABABDE", str2 = "ABAB" should return "". and str1 = "ABCABC", str2 = "ABC" should pass through.

    }
    point := gcd(len(s1), len(s2))
    return s1[:point]
}

func gcd(a, b int) int {
    for b != 0 {
        a, b = b, a % b
    }
    return a
}
```
- C++ solution:
```c
class Solution {
public:
    string gcdOfStrings(const string& s1, const string& s2)
    {
	return (s1 + s2 == s2 + s1)  
		    ? s1.substr(0, gcd(size(s1), size(s2)))
			: "";
    }
};
int gcd(a,b) {
    while(b){ //assuming b is smaller
        return gcd(b,a%b)
    }
    return a
}
```
- C++ solution, _recursive_:
```c
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        if (str1.length() < str2.length()) {
            return gcdOfStrings(str2, str1);
        }

        if (str1 == str2) {
            return str2;
        }

        if (str1.substr(0, str2.length()) == str2) {
            return gcdOfStrings(str1.substr(str2.length()), str2);
        }

        return "";
    }
};
```
