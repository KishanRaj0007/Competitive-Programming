## Pattern 1
Problem Name: Three Activities codeforces. (Div 3 D)
```
a -> 30 20 10 1
b -> 30 5 15 20
c -> 30 25 10 10
```
You have to select 1 element from row 1, one from row 2 and one from row 3 such that:-
- sum of three elements is maximum possible
- slected elements should be from different columns.

Solution:-
```
vector<int> tempA = solve(a);
vector<int> tempB = solve(b);
vector<int> tempC = solve(c);        
for(int i : tempA){
    for(int j : tempB){
        for(int k : tempC){
            if(i!=j && j!= k && i!=k) res = max(res, a[i]+b[j]+c[k]);
        }
    }
}
cout << res << endl;

// finding the index of top 3 numbers and storing in tempA, tempB and tempC
vector<int> solve(vector<int> nums){
    vector<int> arr(3);
    int mx1 = -1, mx2 = -1, mx3 = -1;
    for(int i = 0; i<nums.size(); i++){
        if(mx1 == -1 || nums[i]>nums[mx1]){
            mx3 = mx2;
            mx2 = mx1;
            mx1 = i;
        }
        else if(mx2 == -1 || nums[i] > nums[mx2]){
            mx3 = mx2;
            mx2 = i;
        }
        else if(mx3 == -1 || nums[i] > nums[mx3]){
            mx3 = i;
        }
    }
    arr[0] = mx1;
    arr[1] = mx2;
    arr[2] = mx3;
    return arr;
}
```
---

## Pattern 2
 Whenever you think x≡y(mod m), it means x−y is an integer multiple of m

---

## Pattern 3


