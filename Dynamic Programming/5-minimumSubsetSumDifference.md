## Typical DP (Bottom up approach)
##### Time Complexity  :  O(w*n)  => As traversing through entire matrix is done
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

####    Here, we convert the recursive method to iterative approach, all the recursive calls are converted to just setting that value in matrix and all the conditions remain the same.

```
int minimumSubsetSumDifference(int a[], int arraySum, int n) {
    // Initialize dp array
    int dp[n+1][arraySum+1];

    // Without elements in array, there is no possible way to get the arraySum
    for(int j=1; j<=n; j++)
        dp[0][j] = 0;

    // For (sum=0), there is always one way possible to neglect all elements
    for(int i=0; i<=arraySum; i++)
        dp[i][0] = 1;        
    
    for(int i=1;i<=n;i++)
        for(int j=1;j<=arraySum;j++) {
            // Exclude that element as it exceeds the sum
            if(a[i-1]>j)
                dp[i][j] = dp[i-1][j];
            // Add the ways when element is excluded as well as included
            else
                dp[i][j] = dp[i-1][j-a[i-1]] + dp[i-1][j];
        }
    
    int diff = arraySum;

    // We begin with sum/2 cuz that could give us the least difference
    for(int j=arraySum/2; j>=0; j--) {
        if(dp[n][j]) {
            diff = arraySum - 2*i;
            break;
        }
    }

    return diff;
}
```

#### Observation: If you notice carefully, you will realize that it is almost same as subset sum problem. But instead of returning the last element in array, we iterate through the possible sums and return the one which has the least subset sum difference
