## Method 1         :  Pure recursion
##### Time Complexity  :  O(2^n)  => Each problem has two sub problems
##### Space Complexity :  O(1)    => No extra memory is used



```
bool subsetSum(int a[], int n, int sum) { 
  
    // Base Case (when desired sum is achieved)
    if(sum == 0)
        return true;

    // Base Case(when no elements remain in array)              
    if (n == 0) 
        return false;
    
    // If weight of the nth item is more than the sum, then 
    // this item cannot be included in the optimal solution.
    // Hence, we check for array without this element by reducing last index by one.
    if (a[n - 1] > sum) 
        return subsetSum(a, n - 1, sum); 
  
    // If value of the nth item is <= desired value, then we compare following results:
    // 1) with the current last element included
    // 2) with the current last element excluded
    // And return the respective boolean value.
    else
        return subsetSum(a, n - 1, sum - a[n - 1]) || subsetSum(a, n - 1, sum);
} 
```



<br>

## Method 2         :  Memoization (DP top down approach)
##### Time Complexity  :  O(w*n)  => Calculate if not already done, else return if pre-calculated
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

#### Here we follow the same process as before but we store the computed values and use them whenever encoutered.

```
// Declare a matrix to store the results(The size could be bigger)
int dp[1001][1001];

// Helper function that returns the maximum value that  
// can be put in a knapsack of capacity W 
bool subsetSumUtil(int a[], int n, int sum) 
{
    // Base Case (when desired sum is achieved)
    if(sum == 0)
        return true;

    // Base Case(when no elements remain in array)              
    if (n == 0) 
        return false;

    // If the particular case is already precomputed, then return that
    // instead of recursing and wasting time.
    if(dp[n][sum]!=-1)
        return dp[n][sum];
        
    // Whole logic remains same as before but
    // store the values in the matrix before returning
    if (a[n - 1] > sum) {
        dp[n][sum] = subsetSumUtil(a, n - 1, sum); 
        return dp[n][sum];
    } else {
        dp[n][sum] = subsetSumUtil(a, n - 1, sum - a[n - 1]) || subsetSumUtil(a, n - 1, sum);
        return dp[n][sum];
    }
}

bool subsetSum(int a[], int n, int sum) 
{
    // Initialize matrix elements to -1
    memset(dp, 0, sizeof(dp));

    return subsetSumUtil(a, n - 1, sum); 
}
```



<br>

## Method 3         :  Typical DP (Bottom up approach)
##### Time Complexity  :  O(w*n)  => As traversing through entire matrix is done
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

####    Here, we convert the recursive method to iterative approach, all the recursive calls are converted to just setting that value in matrix and all the conditions remain the same.

```
bool subsetSum(int a[], int sum, int n) {
    // Initialize dp array
    bool dp[n+1][sum+1];

    // Declare initial values of dp array
    for(int j=1; j<=n; j++)
        dp[0][j] = false;

    // Setting (sum = 0) values as true because it will always be satisfied 
    for(int i=0; i<=sum; i++)
        dp[i][0] = true;        
    
    for(int i=1;i<=n;i++)
        for(int j=1;j<=sum;j++) {
            if(a[i-1]>j)
                dp[i][j] = dp[i-1][j];
            else
                dp[i][j] = dp[i-1][j-a[i-1]] || dp[i-1][j];
        }
    return dp[n][sum];
}
```

#### Observation: If you notice carefully, you will realize that it is almost same as knapsack problem with only logic changes in few lines.
