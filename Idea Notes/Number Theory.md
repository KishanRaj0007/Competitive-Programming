# NUMBER THEORY

## BASICS

1. **Type Hierarchy**:
   - `int = long int < float < long long int < double < long double` in terms of size or range of values it can store.
   - If you want `3.5` to `4`, then use `round((float)7/2)` or `round(7.0/2)`.

   For questions related to parity (odd, even), try to come up with a solution by analyzing odd as 1 and even as 0. For example, in an array having even frequency of odd numbers, it is always possible to divide the array into two parts such that the sum of both parts will have the same parity.

   **Example**: [Codeforces Problem 1857/A](https://codeforces.com/problemset/problem/1857/A)

   In the case of a binary string, if you replace `0` with `-1` and `1` with `1`, then the substring which makes the sum `0` is having the same number of `0` and `1`.

2. **Interval of Positive Integers**:
   To find the length of the largest interval `[l, r]` (which is `r - l + 1`) of positive integers (consecutive) such that, for every `i` in the interval (i.e., `l ≤ i ≤ r`), `n` is a multiple of `i` or `i` is a factor of `n`, we will simplify the problem by focusing on intervals starting from 1. If you find the smallest integer `x` that does not divide `n`, then the length of the interval `[1, x-1]` which is `((x-1) - 1 + 1) = x-1` is the required length.

   In other words, among a list of factors of a number, chances of getting the maximum length of consecutive factors that divide a number is good if we start from the beginning. This is because as we move ahead, the difference between factors increases. For example, factors of 40 are 1, 2, 4, 5, 8, 10, 20, 40. See that the sense of consecutiveness decreases as we move far away since the difference between factors increases as we move from left to right. So, the maximum length of consecutive factors will surely appear at the beginning.

   **Example**: [Codeforces Problem 1855/B](https://codeforces.com/problemset/problem/1855/B)

3. **Calculate GCD**:
   To calculate the GCD of a list of numbers stored in a vector, we can find pairwise GCD. The result will be the same.

   ```cpp
   int ans = 0;
   for (int i = 1; i <= n; ++i) {
       int x;
       cin >> x;
       ans = __gcd(ans, abs(x-i));
   }

https://codeforces.com/problemset/problem/1828/B
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
4. Suppose you got a question in which manupulation of division and multiplication is required- in that case try analyzing its prime factors.
   https://codeforces.com/problemset/problem/1374/B
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
5. Whenever you encounter a problem that involves maximizing distances within a rectangular grid, especially with constraints on movement to adjacent cells:the optimal strategy involves placing 
   these points in opposite corners of the grid. This is because the longest possible distance in a rectangular grid is achieved by traversing the perimeter of the grid from one corner to the
   opposite corner.  (the distance always being 2⋅(n−1)+2⋅(m−1)).

   https://codeforces.com/problemset/problem/1537/B   -   (In this question output of test cases are incorrectly given)
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
6. For two numbers a and b, if you want to maximize the gcd of a and b by simultaneously increasing OR decreasing(either one of them) a and b by 1, then maximum gcd possible is abs(a-b)

   https://codeforces.com/problemset/problem/1543/A
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
7. -For 32-bit integers, use int or int32_t.
   -For 64-bit integers, use long long or int64_t.
   -For unsigned 32-bit integers, use uint32_t.  (In C++, the unsigned keyword is used to declare an integer type that can only represent non-negative values.)
   -For unsigned 64-bit integers, use uint64_t.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
8. For finding divisors iterate from 1 to root n for each number i in this range. Check if i is divisor of n, if i is divisor then n/i is also a divisor. Collect both i and n/i as 
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
9. -[(a+b)/x] <= [a/x]+[b/x]
    -[] - ceil function
    -Do not forget to take x in float data type otherwise c++ will automatically round it. 

    https://codeforces.com/problemset/problem/1471/A
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
10.  ## Minimum LCM
         If b%a==0, then LCM(a,b)=b < n where n = a+b.
         If b % a≠0, then LCM(a,b) is at least 2b, and b is at least n/2, so in this case, the answer is at least n where n = a+b
         If a and b are numbers such that a+b = n then minimum lcm of a and b is possible if a is first factor of n and b=n-a.
https://codeforces.com/problemset/problem/1765/M   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
11. -k*b <= (∑⌊a/k⌋ = b) <= k*b + (k-1)*n. where [] means rounding off and summation a/k = [a1/k]+[a2/k]+....[an/k] = b
    https://codeforces.com/problemset/problem/1715/B
-----------------------------------------------------------------------------------------------------------------------------------------------------------------

12. ## Linear Diophantine Equations
   Given three integers a, b, c representing a linear equation of the form : ax + by = c. Determine if the equation has a solution such that x and y are both integral values.

      Find GCD of a and b
      Check if c % GCD(a ,b) ==0
      If yes then print Possible
      Else print Not Possible
   --------------------------------------------------------------------------------------
13. ## Prime Factorization
    ```cpp
    cout << "Hello world << endl;
-----------------------------------------------------------







