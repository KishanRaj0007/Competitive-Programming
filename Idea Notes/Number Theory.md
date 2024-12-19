# NUMBER THEORY

## BASICS

1. **Type Hierarchy**:
   - `int = long int < float < long long int < double < long double` in terms of size or range of values it can store.
   - If you want `3.5` to `4`, then use `round((float)7/2)` or `round(7.0/2)`.

   For questions related to parity (odd, even), try to come up with a solution by analyzing odd as 1 and even as 0. For example, in an array having even frequency of odd numbers, it is always possible to divide the array into two parts such that the sum of both parts will have the same parity.

Odd even problems can sometimes be solved by using XOR operator. For example if we are asked to find the element which occurs odd times in an array of elements all having even count except one, in O(1) SPACE AND O(N) time.
In that case just take XOR of all elements, final ans is required number which occurs odd times. 
small example = a^b^a = a^a^b=0^b=b (all even ones will be computed to 0 and 0 XOR ans = ans)

In this case Hashing will take O(N) SPACE AND O(1) time hence XOR method is optimal.

   **Example**: [Codeforces Problem 1857/A](https://codeforces.com/problemset/problem/1857/A)

   In the case of a binary string, if you replace `0` with `-1` and `1` with `1`, then the substring which makes the sum `0` is having the same number of `0` and `1`.

3. **Interval of Positive Integers**:
   To find the length of the largest interval `[l, r]` (which is `r - l + 1`) of positive integers (consecutive) such that, for every `i` in the interval (i.e., `l ≤ i ≤ r`), `n` is a multiple of `i` or `i` is a factor of `n`, we will simplify the problem by focusing on intervals starting from 1. If you find the smallest integer `x` that does not divide `n`, then the length of the interval `[1, x-1]` which is `((x-1) - 1 + 1) = x-1` is the required length.

   In other words, among a list of factors of a number, chances of getting the maximum length of consecutive factors that divide a number is good if we start from the beginning. This is because as we move ahead, the difference between factors increases. For example, factors of 40 are 1, 2, 4, 5, 8, 10, 20, 40. See that the sense of consecutiveness decreases as we move far away since the difference between factors increases as we move from left to right. So, the maximum length of consecutive factors will surely appear at the beginning.

   **Example**: [Codeforces Problem 1855/B](https://codeforces.com/problemset/problem/1855/B)

4. **Calculate GCD**:
   To calculate the GCD of a list of numbers stored in a vector, we can find pairwise GCD. The result will be the same.

   ```cpp
   int ans = 0;
   for (int i = 1; i <= n; ++i) {
       int x;
       cin >> x;
       ans = __gcd(ans, x);
   }

https://codeforces.com/problemset/problem/1828/B
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
5. Suppose you got a question in which manupulation of division and multiplication is required- in that case try analyzing its prime factors.
   https://codeforces.com/problemset/problem/1374/B
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
6. Whenever you encounter a problem that involves maximizing distances within a rectangular grid, especially with constraints on movement to adjacent cells:the optimal strategy involves placing 
   these points in opposite corners of the grid. This is because the longest possible distance in a rectangular grid is achieved by traversing the perimeter of the grid from one corner to the
   opposite corner.  (the distance always being 2⋅(n−1)+2⋅(m−1)).

   https://codeforces.com/problemset/problem/1537/B   -   (In this question output of test cases are incorrectly given)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
7. For two numbers a and b, if you want to maximize the gcd of a and b by simultaneously increasing OR decreasing(either one of them) a and b by 1, then maximum gcd possible is abs(a-b)

   https://codeforces.com/problemset/problem/1543/A
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
8. -For 32-bit integers, use int or int32_t.
   -For 64-bit integers, use long long or int64_t.
   -For unsigned 32-bit integers, use uint32_t.  (In C++, the unsigned keyword is used to declare an integer type that can only represent non-negative values.)
   -For unsigned 64-bit integers, use uint64_t.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
9. For finding divisors iterate from 1 to root n for each number i in this range. Check if i is divisor of n, if i is divisor then n/i is also a divisor. Collect both i and n/i as 
   divisor. Handle the edge case when both i and n/i is same to avoid duplicates(it can be done using sets).
   ```cpp
     Shortcut to check if a number has odd divisor:-
     // Function to check if n has an odd divisor greater than 1
      bool hasOddDivisorGreaterThanOne(long long n) {
       // Keep dividing n by 2 while it is even
       while (n % 2 == 0) {
           n /= 2;
       }
       // After all divisions by 2, if n becomes 1, it had no odd divisors
       // If n is greater than 1, it means there was an odd divisor
       return n > 1;
   }

https://codeforces.com/problemset/problem/1475/A
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
10. -[(a+b)/x] <= [a/x]+[b/x]
    -[] - ceil function
    -Do not forget to take x in float data type otherwise c++ will automatically round it. 

    https://codeforces.com/problemset/problem/1471/A
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
11.  ## Minimum LCM
         If b%a==0, then LCM(a,b)=b < n where n = a+b.
         If b % a≠0, then LCM(a,b) is at least 2b, and b is at least n/2, so in this case, the answer is at least n where n = a+b
         If a and b are numbers such that a+b = n then minimum lcm of a and b is possible if a is first factor of n and b=n-a.
https://codeforces.com/problemset/problem/1765/M   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
12. -k*b <= (∑⌊a/k⌋ = b) <= k*b + (k-1)*n. where [] means rounding off and summation a/k = [a1/k]+[a2/k]+....[an/k] = b
    https://codeforces.com/problemset/problem/1715/B
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
13. ## Linear Diophantine Equations For existence of solution of ax+by=c
   Given three integers a, b, c representing a linear equation of the form : ax + by = c. Determine if the equation has a solution such that x and y are both integral values.

      Find GCD of a and b
      Check if c % GCD(a ,b) ==0
      If yes then print Possible
      Else print Not Possible
   --------------------------------------------------------------------------------------
14. ## Modular Multiplicative inverse of A under M
    ### CASE 1: When A and M are coprime ( ## Extended Euclid Algorithm)
    ```cpp
    int findInverse(int a,int m){ //MMI of a wrt m using Extended Euclid
     int m0 = m, t, q; 
     int x0 = 0, x1 = 1; 
   
     if (m == 1) return 0;
     // Apply extended Euclid Algorithm 
     while (a > 1) {  
         q = a / m; 
         t = m; 
         m = a % m;
         a = t; 
        t = x0; 
         x0 = x1 - q * x0; 
         x1 = t; 
     } 
     // Make x1 positive.
     if (x1 < 0) x1 += m0;
     return x1;
    }
   ### CASE 2: When M is prime (## Application of Fermat Little Theorem and Binary exponentiation)
   In this case A inverse = (A^(M-2)) % M and which can be done by binary exponentiation.
    ```cpp

        //finding MMI of a under b
        //from Fermat Little theorem and binary exponentiation
        //A inverse = (A^(M-2)) % M
        ll findInverse(ll a, ll b){ 
            ll result = 1;
            ll exponent = b-2;
            while(exponent){
                if(exponent & 1){
                    result = (result*1ll*a) % b;
                }
                a = (a*1ll*a) % b;
                exponent >>= 1;
            }
            return result;
        }
      
      int main() {
            ll ans = findInverse(3,11);
            cout << ans << endl;
      }
---
15. ## Fermat little theorem (application- (a/b) % M = (a % M)*(b inverse % M)) % M and b inverse = (b ^(M-2)) % M
    Here b ^(M-2) is solved by binary exponentiation in log N time.
    
    Fermat’s little theorem states that if p is a prime number, then for any integer a, the number a^p – a is an integer multiple of p.
    This theorem is used in Modular Multiplicative Inverse( a ^(m-1) ≡ 1 mod m) - if we divide lhs with m remainder is 1)
---
16. ## Euler's Totient Function(Application in (a^b) % M = (a ^(b mod phi(M))) % M
    Euler’s Totient function Φ(n) for an input n is the count of numbers in {1, 2, 3, …, n-1} that are relatively prime to n, i.e., the numbers whose GCD (Greatest 
    Common Divisor) with n is 1.
    The idea is based on Euler’s product formula:-
    In this formula p is distinct prime factors.
    ![image](https://github.com/KishanRaj0007/Competitive-Programming/assets/142702439/1c7b8b84-b31c-4bef-b8f6-3e96d3afcc64)
    ```cpp
    int phi(int n)
    {
    
    float result = n; 
    for(int p = 2; p * p <= n; ++p)
    {
        
        if (n % p == 0)
        {
            while (n % p == 0){
                n /= p;
            }
            result *= (1.0 - (1.0 / (float)p));
        }
    }
    if (n > 1) result -= result / n;      
    return (int)result;
    }
**Properties of ETF**

0. **Euler Theorem** : (a^b) % M = a ^ (b%⋅ϕ(M)) % M (It is used if b is very very large as in a^b^c)
1. If p is prime then ϕ(p)=p–1
2. For two prime numbers a and b ϕ(a⋅b)=ϕ(a)⋅ϕ(b)=(a–1)⋅(b–1)
3. For a prime number p, ϕ(p ^ k )=p ^k –p ^ k–1
4. For any two number a and b ϕ(a⋅b) = ϕ(a)⋅ϕ(b) ⋅ 𝑔𝑐𝑑(𝑎,𝑏)/𝜙(𝑔𝑐𝑑(𝑎,𝑏))
5. Sum of values of totient functions of all divisors of n is equal to n. 
​
---
17. ## Binary Exponentiation O(log B)
    ```cpp
       const int M = 1e9+7;
      //if a = 2 and b = 63 then overflow for ll will occur hence Modulo is must in 
      //this type of problem
      ll binExp(ll a, ll b){
          ll result = 1;
          while(b){
              if(b & 1){
                  result = result * 1LL* a % M;  //separat it when odd comes
              }
              a = a*1ll*a % M;
              b >>= 1;
          }
          return result;
      }
Applications:-
1. a raised to the power b and b is very very large(1e9).
2. product of two very large numbers(just replace * with + and result = 0.
3. applying permutaion P to S.
---
18. ## Prime Factorization(rootN(log N))
    ### (Not effecient in query problems as overall complexity will be t*rootN(Log N).
    concept:-
    1. Smallest divisor of any number is always prime(except 1)
    2. For a composite number N, there exist at least one prime number p such that 2 <= p <= sqrt(N) and p divides N.
    ```cpp      
      void findPrimeFactors(long long n){
          vector<long long> x;
          //the smallest divisor of a number is always prime except 1
          for (long long i = 2; i * i <= n; ++i) {
              while(n % i == 0){
                  x.push_back(i);
                  n = n / i;
              }
          }
          // if n > 1 it means n has only even factors
          if(n > 1) x.push_back(n);
          for(auto a : x){
              cout << a << " ";
          }
      }
-----------------------------------------------------------
19. ## Sieve of Eratosthenes for getting primes in some range in Nlog(log N) time:-
    ```cpp
    int main() {
    int n = 1e7+7;
    int l, r;
    cin >> l >> r;
    vector<bool> isprime(n,1);
    isprime[0] = isprime[1] = false;
    for (int i = 2; i < n; ++i)
    {
        if(isprime[i]){
            for (int j = i*2; j < n; j+=i)
            {
                isprime[j] = false;
            }
        }        
    }
    
    for (int i = l; i <= r; ++i)
    {
        if(isprime[i]){
            cout << i << " ";
        }
    }
}

---------------------
20. ## Prime Factorization in log N using Sieve
    ### (Effecient in case of queries - NLog(Log N) + t*Log N is more effecient than t*rootN(Log N))
    ```cpp
    #include<bits/stdc++.h>
      using namespace std;
      #define ll long long
      
      const int N = 1e7+7;
      vector<int> spf(N,1); //stores smallest primefactor of every number
      
      void precomputeSPFBySieve(){ // NLog(Log N)
          spf[0] = 0;
          spf[1] = 1;
          for (int i = 2; i < N; ++i)
          {
              if(spf[i] == 1){
                  for (int j = i; j < N; j+=i)
                  {
                      if(spf[j] == 1) spf[j] = i;
                  }
              }
          }
      }
      //Log N time
      vector<int> getPrimeFactors(int num){
          vector<int> ans;
          while(num != 1){
              ans.push_back(spf[num]);
              num = num/spf[num];
          }
          return ans;
      }
      
      //NLog(Log N) + t*Log N
      int main() {
          precomputeSPFBySieve(); //precompute outside query
          int t;
          cin >> t;
          while(t--){
              int n;
              cin >> n;
              cout << "PF of " << n << ":- ";
              vector<int> ret = getPrimeFactors(n);
              for(auto x : ret){
                  cout << x << " ";
              }
              cout << endl;
          }
      }    
---
21. ## Chinese Remainder Theorem
![Screenshot 2024-06-14 094540](https://github.com/KishanRaj0007/Competitive-Programming/assets/142702439/037866bd-6ec9-4e3d-b58b-899c31427e6f)
### Problem is to find minimum value of x.
Note that gcd of 3, 4 and 5 is one and chinese remainder theorem is valid only if they are pairwise coprime.
Chinese Remainder Theorem states that there always exists an x that satisfies given congruences:- 

 x ≡ y (mod productOfNumbers) i.e., All those x when divided by product(3*4*5) will always give same remainder.
 But we use following formula to find value of x:-
 
 x =  ( Σ(rem[i]*pp[i]*inv[i]) ) % prod  (To visualize see this video - https://www.youtube.com/watch?v=ru7mWZJlRQg )
   Where 0 <= i <= n-1
   
   1. rem[i] is given array of remainders
   2. prod is product of all given numbers (prod = num[0] * num[1] * ... * num[k-1], remember their pairwise gcd is 1)
   3. pp[i] is product of all divided by num [i] (pp[i] = prod / num[i])
   4. inv[i] = Modular Multiplicative Inverse of pp[i] with respect to num[i].
      
### NOTE: Do not use Inverse formula derived by Fermat Little Theorem instead use Extended Euclid Algorithm.
   We cannot use A inverse = (A^(M-2)) % M to find inverse of A which is implemented by binary exponentiation because nums[i]
   is not necessarily prime and This formula is used only if M is prime.

      //NLog N time
      ```cpp
      int findInverse(int a,int m){ //inv of a wrt m using Extended Euclid
        int m0 = m, t, q; 
        int x0 = 0, x1 = 1; 
      
        if (m == 1) return 0;
        // Apply extended Euclid Algorithm 
        while (a > 1) {  
            q = a / m; 
            t = m; 
            m = a % m;
            a = t; 
            t = x0; 
            x0 = x1 - q * x0; 
            x1 = t; 
        } 
        // Make x1 positive 
        if (x1 < 0) x1 += m0;
        return x1;
      }
      
      int minX(vector<int> nums, vector<int> rem, int size){ //nums is pairwise coprime
          int pro = 1;
          for(auto i : nums){
              pro *= i;
          }
          int ans = 0;
          for (int i = 0; i < size; ++i)
          {
              int pp = pro/nums[i];
              ans += rem[i]* pp *(findInverse(pp,nums[i]));
          }
          ans %= pro;
          return ans;
      }
      
      int main() {
            vector<int> nums = {3,4,5};
            vector<int> rem = {2,2,1};
            int res = minX(nums, rem, nums.size());
            cout << res << endl;
      }
   ---
22. ## Bit Manipulation
       1. 1<<n = 2^n (It has only nth bit set eg: 4 = 100)
       2. Number just before 2^n i.e., 2^n - 1 has only 1 in its binary representation (eg: 3 = ..011)
       3. Check whether n is power of 2 : return  ((n & (n - 1)) == 0); //100 & 011 = 000
       4. n<<k = multiply by 2 k times
       5. n>>k = divide by 2 k times
       6. n&1 = check for odd
       7. (upperCaseLetter | ' ') = corresponding lowercase letter
       8. (lowerCaseLetter & '_') = corresponding uppercase letter
       9. x^x = 0, x^0 = x, x^y^z = x^z^y = y^x^z
       10. Range of unsigned int is greater than signed int because it stores only non negative values and hence 1 bit of signed int gets wasted in sign.
       11. Convert binary to decimal
           ```cpp
           int binaryToDecimal(int n)
            {
                int dec_value = 0;
                int base = 1;
                while (n) {
                    int last_digit = n % 10;
                    dec_value += last_digit * base;
                    base = base * 2;
                    n = n/10;
                }
                return dec_value;
            }
       13. For printing binary representation of a number:-
           ```cpp
             void printBinary(int n){
              for (int i = 10; i >= 0; --i)
              {
                cout << ((n >> i)&1);
              }
           }
       14. If n & (1<<i) != 0 then ith bit of n is set.(alternate method - 1ll & (n >> i))
       15. To set ith bit : n = n | (1<<i)
       16. To unset ith bit : n = n & ~(1<<i)
       17. To toggle ith bit : n = n ^ (1<<i)
       18.  result += (1<<i); //This is used to form complete binary representation of a desired number bit by bit.
       19.  ```cpp
            #pragma GCC target("popcnt") //use this otherwise these functions will run slowly in gcc and even in cpp 20
            __builtin_ffs(int) // finds the position(not index) of the first (most right) set bit eg 00010010100-->3
            __builtin_clz(unsigned int) the count of leading zeros
            __builtin_ctz(unsigned int) the count of trailing zeros
            __builtin_parity(x) the parity (even or odd) of the number of ones in the bit representation
       20.  ### Clear the right-most set bit
          The expression n & (n-1) is used to turn off the rightmost set bit of a number n.  This works because the bitwise expression of n-1
          has all the digits flipped after the rightmost set bit of n including rightmost set bit.
          1. n =   1 1 0 1 0 0 0
          2. n-1 = 1 1 0 0 1 1 1
       18.  In most of the problems involving bit manipulation it is better to work bit by bit i.e., break down the problem into individual bits.
            Focus on solving the problem for a single bit position before moving on to the next.
       20. To find bitcount(Total number of setbits) :-
           1. __builtin_popcount(n) - for integers
           2. __builtin_popcountll(n) - for long long int
           3. if((a&(1<<i)) != 0) count++; (check if ith bit is set or not)
           4. ## Brian Kernighan's algorithm
              The idea is to consider only the set bits of an integer by turning off its rightmost set bit (after counting it), so the next iteration of the loop 
              considers the Next Rightmost bit.
                 ```cpp
                 int countSetBits(int n)
                  {
                      int count = 0;
                      while (n)
                      {
                          n = n & (n - 1);
                          count++;
                      }
                      return count;
                  }
       21. ### Bitwise operation in a range:
           (for example to find Bitwise AND for all elements of an array between position 2 and 4)
           In these type of problem we will use precomputation to solve in O(1) time. Store all 32 bits of n numbers in 2d array. Then Precompute
           all bits, store result in other array and apply operations(&, OR XOR) accordingly.
           #### For example in & -
           If the count of numbers with the j-th bit set in the range [l, r] is equal to the range size (r – l + 1), it means that
           all numbers in that range have their j-th bit set.
           #### In case of XOR:
           If the count of numbers with the j-th bit set in the range [l, r] is odd, it means that the j-th bit of the result should be set to 1. If the count is even, 
           the j-th bit of the result should be set to 0.
           
           ```cpp
           vector<vector<int>> prefixSum(vector<int> nums){
           int n = nums.size();
           //fill the array with bits
           vector<vector<int>> temp(n + 1, vector<int>(32, 0));
           /**  nth bit  n-1 n-2 ....1 0th bit
            * n1 _  _    _    _
            * n2 _  _    _    _   
            * n3
           */
           for (int i = 1; i <= n; ++i){
             int number = nums[i-1];
             for(int j = 0; j < 32; ++j){
               if((number & (1<<j)) != 0){ //precedence issue alert
                 temp[i][j] = 1;
               }
             }
           }
           //calculate prefix sum
           vector<vector<int>> ans(n+1, vector<int>(32,0));
           for (int i = 0; i < 32; ++i)
           {
             for (int j = 1; j <= n; ++j)
             {
               ans[j][i] = ans[j-1][i]+temp[j][i];
             }
           }
           return ans;
           }
            // finding AND from l to r
            int bitOperationInRange(vector<vector<int>> psum, int l, int r){
              int range = r-l+1;
              int result = 0;
              for(int i =0; i < 32; ++i){
                if((psum[r][i] - psum[l-1][i]) == range){
                  result += (1<<i);
                }
              }
              return result;
            }
            
            int main(){
              vector<int> nums = {13,11,2,3,6};
              int l = 3;
              int r = 5;
              vector<vector<int>> psum = prefixSum(nums);
              int res = bitOperationInRange(psum,l,r);
              cout << res << endl;
            }
    22. ### Check if a number is divisible by power of 2
        ```cpp
        bool isDivisibleByPowerOf2(int n, int k) {
             int powerOf2 = 1 << k;
             return (n & (powerOf2 - 1)) == 0;
         }
---
   22. ### Check if an integer is a power of 2
       1. 32 = 1 0 0 0 0 0
       2. 31 = 0 1 1 1 1 1
       So if & of both the number is 0 then number is power of 2. You can use this in code:-
       ```cpp
       bool isPowerOfTwo(unsigned int n) {
          return n && !(n & (n - 1));
       }
---
   23. ## Some other tricks
       1. n & (n+1) removes all trailing ones 1 1 0 1 1 1--->1 1 0 0 0 0
       2. n | (n+1) sets the last cleared bit 1 1 0 1 0 1--->1 1 0 1 1 1
       3. The result of 𝑛 & −𝑛 gives you a number that has only the lowest set bit of 𝑛 set to 1.  1 1 0 1 0 0--->0 0 0 1 0 0      
---
   24. ## Bitwise practice problems (Div 2 B)
       1. https://codeforces.com/contest/1973/problem/B
       2. https://codeforces.com/contest/1994/problem/B
       3. https://codeforces.com/contest/1884/problem/B
       4. https://codeforces.com/contest/1870/problem/B
       5. https://codeforces.com/contest/1867/problem/B
       6. https://codeforces.com/contest/1847/problem/B
       7. https://codeforces.com/contest/1842/problem/B
---
25. # Binary Search

    ## Binary Search: Finding Maximum and Minimum `x` for `f(x) = true`

      Binary search can be adapted to find either the **maximum** or **minimum** value of `x` that satisfies a condition represented by `f(x)`. Below are the two main 
      algorithms and when to use them.
      For more details go to - https://usaco.guide/silver/binary-search?lang=cpp#implementation-1
      
      ## 1. Finding the Maximum `x` Such That `f(x) = true`
      
      ### Concept
      - **Goal**: Find the highest value of `x` in the range `[lo, hi]` for which `f(x)` is `true`.
      - **Usage**: Use this when `f(x)` transitions from `true` to `false` as `x` increases (monotonically decreasing behavior).

      ### Code Implementation
      ```cpp
      #include <bits/stdc++.h>
      using namespace std;
      
      int last_true(int lo, int hi, function<bool(int)> f) {
          lo--; // Start with an invalid value to handle no valid case
          while (lo < hi) {
              int mid = lo + (hi - lo + 1) / 2; // Round up to avoid infinite loop
              if (f(mid)) {
                  lo = mid; // Move up if `f(mid)` is true
              } else {
                  hi = mid - 1; // Move down if `f(mid)` is false
              }
          }
          return lo;
      }
      
   ---
   ## 2. Finding the Minimum `x` Such That `f(x) = true`

   ### Concept
   - **Goal**: Find the lowest value of `x` in the range `[lo, hi]` for which `f(x)` is `true`.
   - **Usage**: Use this when `f(x)` transitions from `false` to `true` as `x` increases (monotonically increasing behavior).

      ### Code Implementation
      ```cpp
      #include <bits/stdc++.h>
      using namespace std;
      
      int first_true(int lo, int hi, function<bool(int)> f) {
          hi++; // Move `hi` up to handle no valid case
          while (lo < hi) {
              int mid = lo + (hi - lo) / 2; // Standard mid calculation
              if (f(mid)) {
                  hi = mid; // Move down if `f(mid)` is true
              } else {
                  lo = mid + 1; // Move up if `f(mid)` is false
              }
          }
          return lo;
      }
---
26. ## Binary Search Problems
    1. https://codeforces.com/problemset/problem/1873/E
    2. https://codeforces.com/problemset/problem/1850/E
    3. 




 
         








