## Typical DP (Bottom up approach)
##### Time Complexity  :  O(w*n)  => As traversing through entire matrix is done
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

[Problem Set | Leetcode](https://leetcode.com/problems/target-sum/)

<br>
    Consider the array is (A1, A2, A3 ... An)<br>
    SUPPOSE the optimal solution is '+' for odd elements and '-' for even elements<br>
    Hence the desired array would be (+A1, -A2, +A3, -A4 ...)<br>
    We can rewrite the expression as (+A1+A3+A5... -(A2+A4+A6+....))<br>
    If (A1, A3, A5, ...) is a subset S1 and (A2, A4, A6, ...) is a subset S2<br>
    Then the overall expression is <br>
        S1 - S2 = givenSum<br>
    From here, the question reduces to count the subsets with given difference (previously discussed)<br>

<br>

```
// Discussed Previously
int countSubsetsWithGivenDifference(int a[], int difference, int n);

int targetSum(int a[], int n, int targetSumValue) {

    // As explained before
    countSubsetsWithGivenDifference(a, targetSumValue, n);
}
```

#### Observation: Same code as subset sum. The thing changed here is the way of asking the problem.
