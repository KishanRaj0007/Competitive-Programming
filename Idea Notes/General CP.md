
0. ## SILLY MISTAKES

         a.> Do not forget to observe the range of input values. Accordingly decide the data type. For example interger can store upto 1e9, long can store upto 1e12 and long long can store upto 
          1e18.
         b.> Also note that most questions should be solved within 1s of time, which happens only if your max intraion is of the order of 1e7.
         c.> You should also not forget to clear the vector or map after each test case using mp.clear() or arr.clear()
         d.> When you declare int sum; its initial value is indeterminate, meaning it could contain any random value. So initialize it to sum = 0 before proceeding to code logic.
         e.> Store value of boolean expression in bool data type and not in int data type(Example - https://www.codechef.com/START136D/problems/FIRSTGEO)
         f.>We should use int a = s[i] - 'a' to convert the character to an index from 0 to 25 where s[i] is indexing of some string.
         g.>vector<int> arr(n, 0) initializes a vector named arr with n elements, all set to 0
         h.> ios_base::sync_with_stdio(false);
          cin.tie(nullptr);
          cout.tie(nullptr);
          It ensures faster input and output operations, which is crucial for handling large input sizes efficiently.
         i.> vector<vector<int>> grid(n, vector<int>(m)); //for 2d array

---
0. Given two arrays, A and B, both of the same size 𝑛, you are required to find the minimum possible value of the sum of products of corresponding elements of the two a 
   arrays.
   
  Sol: To solve this arrange first array in ascending order and second one in descending order.

2. We can use inbuilt map data structure to store frequency of each element of an array or vector while taking the input from user:-

  https://codeforces.com/problemset/problem/1890/A
  https://codeforces.com/problemset/problem/1807/D

    ```cpp
        map<int, int> freq;
              int x;
              for (int i = 0; i < n; ++i)
              {
                  cin >> x;
                  freq[x]++;
              }
      //to find maximum frequency(alternatively we can find key with maximum frequency)
      int maxFreq = 0;
              for (auto &[x, y] : freq) {
                  maxFreq = max(maxFreq, y);
              }
---

2. Sometimes in questions of Yes or No, you do not have to look for every edge case, instead look to more vulnerable one and rest all cases will fall in other one.
  
Example - https://codeforces.com/problemset/problem/1878/A
---

3. If you are getting TLE and you think that algo is good, then try applying precomputation technique. It will work sometimes because precomputing at constraind length and storing your answers 
in vector saves much time if compared to brute worst case. By precomputation you are now just required to print you answer only in constant or linear time.
  
Example - https://codeforces.com/problemset/problem/1766/A
The total time complexity is O(t NlogN) where t is 1e4 and N is 999999 which leads to TLE because 1e7 iterations take about 1second and here is 1e10 iterations
BRUTE FORCE:-
    
    ```cpp
    
      while(t--){
          int n;
          cin >> n;
          int count = 0;
          int answer = 0;
          for (int i = 1; i <= n; ++i) {
              count = 0;
              int temp = i;
              while(temp != 0){
                  int r = temp % 10;
                  if(r != 0){
                      count++;
                  }
                  temp = temp/10;
              }
              if(count == 1){
                  answer++;
              }
          }
          cout << answer <<endl;
      }
  
---
OPTIMIZED: PRECOMPUTATION
    ```cpp
    
      int compute(int i){
              int count = 0;
              int temp = i;
              while(temp != 0){
                  int r = temp % 10;
                  if(r != 0){
                      count++;
                  }
                  temp = temp/10;
              }
              return (count == 1);
      }
      
      int main() {
          int t;
          cin >> t;
          vector<int> round;
          for (int i = 0; i < 999999; ++i)
          {
              if(compute(i)){
                  round.push_back(i);
              }
          }
          
          while(t--){
              int n;
              cin >> n;
              int count = 0;
              for(auto x: round){
                  if(x <= n) count++; 
              }
              cout<< count << endl;
          }
      }

For each test case, we count how many precomputed numbers are ≤𝑛. This is 𝑂(𝑚), where 𝑚 is the number of precomputed extremely round numbers (a constant, at most 54 for the given range).
Thus, the time complexity per test case is 𝑂(𝑚), and for 𝑡 test cases, the total time complexity is 𝑂(𝑡⋅𝑚). Since 𝑚 is a small constant, this simplifies to 𝑂(𝑡).

---
4. TRACKING MAXIMUM SUBARRAY LENGTH SATISFYING SOME CONDITION.
   ```cpp
   
   int ans = 1;
   int count = 1;
   for(int i = 0;i<n; ++i){
      if(condition) count++;
      else count = 1
      ans = max(ans,count);
    }

1. https://codeforces.com/problemset/problem/1837/B
2. https://codeforces.com/problemset/problem/1850/D

---
5. To find the length of the longest consecutive sequence of identical elements in an array we will find an array f whose a[i] will give the frequency count of element i, algo is:-

   input - a: 1 2 2 2 2
   output - fa :- fa: [0, 1, 4, 0, 0, 0, 0, 0, 0, 0, 0]  (indexing starts from 1)
    
    vector<int> fa(n + n + 1); //will store the maximum lengths of consecutive identical elements and store in i. fa[2] will give frequency of longest consecutive 2
    int p = 1; // p variable tracks the start of the current segment of identical elements.
    // This loop traverses the array a and calculates the longest subarray for each unique element.
   ```cpp
       for (int i = 2; i <= n; ++i)
    {
        if (a[i] != a[i - 1])
        {
            fa[a[i - 1]] = max(fa[a[i - 1]], i - p);
            p = i;
        }
    }
    fa[a[n]] = max(fa[a[n]], n - p + 1);
---
6. ## Josephus Problem:
   Consider a game where there are n children (numbered 1,2,...,n) in a circle. During the game, repeatedly k children are skipped and one child is removed from the 
   circle.  The process stops when one number remains. It is required to find the last number.

   example - for n = 7 and k = 2, order is 3 6 2 7 5 1 4 , hence last element is 4.

   If k = 1 then you can also use queue implementation:-
   https://cses.fi/paste/35ed8e010e844a749277fa/
   
   ### kLog(N)
       ```cpp
       int josephus(int n, int k) {
             if (n == 1)
                 return 0;
             if (k == 1)
                 return n-1;
             if (k > n)
                 return (josephus(n-1, k) + k) % n;
             int cnt = n / k;
             int res = josephus(n - cnt, k);
             res -= n % k;
             if (res < 0)
                 res += n;
             else
                 res += res / (k - 1);
             return res;
         }
   
   ### O(N)
   ```cpp
   //0 based indexing so if k=2 then pass k = 3 to get 4
   int josephus(int n, int k) {
    int res = 0;
    for (int i = 1; i <= n; ++i)
      res = (res + k) % i;
    return res + 1;
   }

---
7. ## Finding number of elements in sorted array greater than number x in O(Log N).
   ```cpp
    vector<int> a = {1,2,3,4,5,6}; //array must be sorted
    int x = 4;
    auto justGreaterVal = upper_bound(a.begin(),a.end(),x);//returns iterator of 5
    int index = justGreaterVal-a.begin();//iterator converted to index
    cout << a.size()-index << endl;

#### practice problem --> https://codeforces.com/problemset/problem/1827/A
---










