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

14. ## Fermat’s little theorem (application- (a/b) % M = (a % M)*(b inverse % M)) % M and b inverse = (b ^(M-2)) % M
    Here b ^(M-2) is solved by binary exponentiation in log N time.
    
    Fermat’s little theorem states that if p is a prime number, then for any integer a, the number a^p – a is an integer multiple of p.
    This theorem is used in Modular Multiplicative Inverse( a ^(m-1) ≡ 1 mod m) - if we divide lhs with m remainder is 1)
---
15. ## Euler's Totient Function(Application in (a^b) % M = (a ^(b mod phi(M))) % M
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
16. ## Binary Exponentiation O(log B)
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
17. ## Prime Factorization(rootN(log N))
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
18. ## Sieve of Eratosthenes for primes in some range in Nlog(log N) time:-
    ### (Not useful in query related problem N^2log(log N))
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

---
19.






