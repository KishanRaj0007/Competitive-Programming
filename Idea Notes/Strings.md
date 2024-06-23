# STRINGS

1. ## SUBSTRING CHECK
To check for substring s in sting x, we use x.find(s). It searches for the first occurrence of the substring s within the string x. It returns the starting index of the first occurrence of s
in x. If the substring s is not found, find returns a special constant value std::string::npos.

       if(x.find(s) == string::npos){
           cout << "Substring not found"<<endl;
       }
       else{
           cout << "s found in x at staring index "<< x.find(s) <<endl;
       }

---

2. ## DELETE CHARACTER(S) STARTING AT INDEX
    str.erase(start_index, frequency);

-----

3.  Suppose there is a string 10111010. Let l points to first index, and r points to last index. On iterating l towards right and r towards left simultaneously, at any point the value of
    r-l+1 will give the length of substring starting from l till r.

   EXAMPLE:- https://codeforces.com/problemset/problem/1791/C
---
4. ## Kishan's Dublet SubString Paradox
Theorem:
The frequency of the substring "ab" is equal to the frequency of the substring "ba" in a string composed solely of characters 'a' and 'b' if and only if the first and last characters 
of the string are the same. 
If the frequencies are not equal, this equality can be achieved by reversing either the first or the last character of the string.

Example - s = "abababa"
Here, the first and last characters are both 'a'. The frequency of substring 'ab' is 3, and the frequency of substring 'ba' is also 3. So, the statement holds true for this example.

Example s = "abababb"
Here, the first character is 'a' and the last character is 'b'. The frequency of substring 'ab' is 3, and the frequency of substring 'ba' is 2. According to the statement, we should reverse either
the first or last character. Let's reverse the last character:

s' = "abababa"
Now, the frequency of substring 'ab' is 3, and the frequency of substring 'ba' is also 3. So, the statement holds true for this example after the suggested modification.

             #include "bits/stdc++.h"
              using namespace std;
              int main()
              {
                  int t;
                  cin >> t;
                  while(t--){
                      string s;
                      cin >> s;
                      if(s[0] == s[s.length()-1]){
                          cout << s << endl;
                          continue;
                      }
                      if(s[0] == 'a'){
                          s[0] = 'b';
                      }
                      else{
                          s[0] = 'a';
                      }
                      cout << s << endl;
                  }
              }
https://codeforces.com/problemset/problem/1606/A
---
5. ## Palindrome String

A string s can be rearranged to form a palindrome if and only if "the number of letters with odd occurrences is not greater than 1".

https://codeforces.com/contest/1883/problem/B
---
6. To cound distinct letters or characters use set(for sorting purpose) or unordered_set.
https://codeforces.com/problemset/problem/1791/D
---


















