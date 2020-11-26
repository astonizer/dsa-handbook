## Method           :  Subset Sum (Minor Add-On)
##### Time Complexity  :  Depends on subsetSum program complexity
##### Space Complexity :  Depends on subsetSum program complexity



```
// Discussed previously
bool subsetSum(int a[], int n, int sum);

bool equalPartition(int a[], int n) { 
    int sum = 0;
    
    // Calculating sum of array elements
    for(int i=0; i<n; i++)
        sum += a[i];

    // To have equal sum(S and S), total sum should be 2*S. Hence if sum is odd, equal partition is not possible
    if(sum % 2)
        return false;

    // If sum is even, check for subset with totalSum(= sum/2) using subsetSum algorithm
    return subsetSum(a, n, sum / 2);
} 
```
