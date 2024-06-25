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
7. ## Knuth-Morris-Pratt (KMP) Algorithm [O(n+m)]
   Use when: You need to find all occurrences of a pattern string within a text string efficiently (with preprocessing).
   ```cpp
   // Preprocess the pattern to create the lps array
       vector<int> computeLPSArray(string pattern) {
           int m = pattern.length();
           vector<int> lps(m, 0);
           int len = 0;
           int i = 1;
           while (i < m) {
               if (pattern[i] == pattern[len]) {
                   len++;
                   lps[i] = len;
                   i++;
               } else {
                   if (len != 0) {
                       len = lps[len - 1];
                   } else {
                       lps[i] = 0;
                       i++;
                   }
               }
           }
           return lps;
       }

   // KMP search algorithm
       void KMPSearch(string text, string pattern) {
           int n = text.length();
           int m = pattern.length();
           vector<int> lps = computeLPSArray(pattern);
           int i = 0;
           int j = 0;
           while (i < n) {
               if (pattern[j] == text[i]) {
                   i++;
                   j++;
               }
               if (j == m) {
                   cout << "Found pattern at index " << i - j << endl;
                   j = lps[j - 1];
               } else if (i < n && pattern[j] != text[i]) {
                   if (j != 0) {
                       j = lps[j - 1];
                   } else {
                       i++;
                   }
               }
           }
       }
---
8. ## Z-Algorithm [O(n+m)]
   Use when: You need to find all occurrences of a pattern within a text string or want to compute matching prefixes efficiently.
   ```cpp
   // Z-Algorithm to compute Z array
       vector<int> computeZArray(string s) {
           int n = s.length();
           vector<int> Z(n, 0);
           int L = 0, R = 0, K;
           for (int i = 1; i < n; ++i) {
               if (i > R) {
                   L = R = i;
                   while (R < n && s[R] == s[R - L])
                       R++;
                   Z[i] = R - L;
                   R--;
               } else {
                   K = i - L;
                   if (Z[K] < R - i + 1)
                       Z[i] = Z[K];
                   else {
                       L = i;
                       while (R < n && s[R] == s[R - L])
                           R++;
                       Z[i] = R - L;
                       R--;
                   }
               }
           }
           return Z;
       }
   // Z search algorithm
       void ZSearch(string text, string pattern) {
           string concat = pattern + "$" + text;
           vector<int> Z = computeZArray(concat);
           int patternLength = pattern.length();
           for (int i = 0; i < Z.size(); ++i) {
               if (Z[i] == patternLength) {
                   cout << "Found pattern at index " << i - patternLength - 1 << endl;
               }
           }
       }
---
9. ## Rabin-Karp Algorithm [O(n*m) - Worst case]
    Use when: You need to find occurrences of a pattern within a text string using hashing (useful when dealing with multiple pattern searches).
   ```cpp
   #define d 256
   #define q 101 // A prime number

    void RabinKarpSearch(string pattern, string text) {
    int m = pattern.length();
    int n = text.length();
    int i, j;
    int p = 0; // hash value for pattern
    int t = 0; // hash value for text
    int h = 1;

    // The value of h would be "pow(d, m-1)%q"
    for (i = 0; i < m - 1; i++)
        h = (h * d) % q;

    // Calculate the hash value of pattern and first window of text
    for (i = 0; i < m; i++) {
        p = (d * p + pattern[i]) % q;
        t = (d * t + text[i]) % q;
    }

    // Slide the pattern over text one by one
    for (i = 0; i <= n - m; i++) {
        // Check the hash values of current window of text and pattern
        if (p == t) {
            // Check for characters one by one
            for (j = 0; j < m; j++) {
                if (text[i + j] != pattern[j])
                    break;
            }
            if (j == m)
                cout << "Pattern found at index " << i << endl;
        }

        // Calculate hash value for next window of text
        if (i < n - m) {
            t = (d * (t - text[i] * h) + text[i + m]) % q;
            if (t < 0)
                t = (t + q);
        }
    }
   }
---
10. ### Handling ahead and back index at same time
    ```cpp
        // Ensure no digit comes after a letter
    bool foundLetter = false;
    for (char ch : s) {
        if (isalpha(ch)) //isalphs(ch) is inbuilt function
            foundLetter = true;
        else if (foundLetter && isdigit(ch)) //isdigit(ch) is also a inbuilt function
            return false;
    } //is_sorted(s.begin(),s.end()) is also an inbuilt function
---

















