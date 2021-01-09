## Typical DP (Bottom up approach)
##### Time Complexity  :  O(w*n)  => As traversing through entire matrix is done
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

<br>
    Consider two non-intersecting subsets with sum S1 & S2 of array with sum A.<br>
    S1 + S2 = A<br>
    The equation deduced from p-set is<br>
        S1 - S2 = x (x = difference)<br>
    From previous equation,<br>
        A - S2 - S2 = x<br>
        A - 2*S2 = x<br>
        S2 = (A + x)/2<br><br>
    We simply find the count of subsets with sum S2.

<br>

```
// Discussed Previously
int countOfSubsetSum(int a[], int sum, int n);

int countSubsetsWithGivenDifference(int a[], int difference, int n) {
    int sum=0; 
    for(int i=0; i<n; i++) 
        sum += a[i];

    int sumToBeFound = (sum + difference)/2;

    return countofSubsetSum(a, sumToBeFound, n);
}
```

#### Observation: Same code as subset sum. The thing changed here is the way of asking the problem.
