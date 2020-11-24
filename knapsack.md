## Method 1         :  Pure recursion
##### Time Complexity  :  O(2^n)  => Each problem has two sub problems
##### Space Complexity :  O(1)    => No extra memory is used



```
int knapSack(int totalWeight, int weight[], int value[], int index) { 
  
    // Base Case (when no elements remain in array)
    if (index == 0 || totalWeight == 0) 
        return 0; 
  
    // If weight of the nth item is more than total capacity, then 
    // this item cannot be included in the optimal solution.
    // Hence, we check for array without this element by reducing last index by one.
    if (weight[index - 1] > totalWeight) 
        return knapSack(totalWeight, weight, value, index - 1); 
  
    // If weight of the nth item is <= total capacity, then we compare following results:
    // 1) with the current last element included
    // 2) with the current last element excluded
    // And return the bigger value.
    else
        return max(
                    value[index - 1] + knapSack(totalWeight - weight[index - 1], weight, value, index - 1), 
                    knapSack(totalWeight, weight, value, index - 1)
                ); 
} 
```



<br>

## Method 2         :  Memoization (DP top down approach)
##### Time Complexity  :  O(w*n)  => Calculate if not already done, else return if pre-calculated
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

#### Here we follow the same process as before but we store the computed values and use them whenever encoutered.

```
// Declare a matrix to store the results
int dp[1001][1001];

// Helper function that returns the maximum value that  
// can be put in a knapsack of capacity W 
int knapSackUtil(int W, int wt[], int val[], int n) 
{
    // Base case as said earlier
    if(W==0 || n==0)
        return 0;

    // If the particular case is already precomputed, then return that
    // instead of recursing and wasting time.
    if(dp[n][W]!=-1)
        return dp[n][W];
        
    // Whole logic remains same as before but
    // store the values in the matrix before returning
    if(wt[n-1] > W) {
        dp[n][W] = knapSackUtil(W, wt, val, n-1);
        return dp[n][W];
    } else {
        dp[n][W] = max(val[n-1] + knapSackUtil(W - wt[n-1], wt, val, n-1), 
                        knapSackUtil(W, wt, val, n-1));
        return dp[n][W];
    }
}

int knapSack(int W, int wt[], int val[], int n) 
{
    // Initialize matrix elements to -1
    memset(dp, -1, sizeof(dp));

    return knapSackUtil(W, wt, val, n);
}
```



<br>

## Method 3         :  Typical DP (Bottom up approach)
##### Time Complexity  :  O(w*n)  => As traversing through entire matrix is done
##### Space Complexity :  O(w*n)  => WxN Matrix is used for storing

####    Here, we convert the recursive method to iterative approach, all the recursive calls are converted to just setting that value in matrix and all the conditions remain the same.

```
int knapSack(int W, int wt[], int val[], int n) 
{
    // Declare matrix
    int dp[n+1][W+1];

    // Initialize all elements to -1
    memset(dp, -1, sizeof(dp));

    for(int i=0;i<=n;i++)
        for(int j=0;j<=W;j++) {
            // 
            if(i==0 || j==0)
                dp[i][j] = 0;
            else if(wt[i-1] > j)
                dp[i][j] = dp[i-1][j];
            else
                dp[i][j] = max(val[i-1] + dp[i-1][j - wt[i-1]], dp[i-1][j]);
        }
    return dp[n][W];
}
```
