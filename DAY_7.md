# DAY 7

## Next permutation

https://www.codingninjas.com/codestudio/problems/next-permutation_8230741?challengeSlug=striver-sde-challenge

### Approach
Step 1: Linearly traverse array from backward such that ith index value of the array is less than (i+1)th index value. Store that index in a variable.

Step 2: If the index value received from step 1 is less than 0. This means the given input array is the largest lexicographical permutation. Hence, we will reverse the input array to get the minimum or starting permutation. Linearly traverse array from backward. Find an index that has a value greater than the previously found index. Store index is another variable.

Step 3: Swap values present in indices found in the above two steps.

Step 4: Reverse array from index+1 where the index is found at step 1 till the end of the array.

```
#include <bits/stdc++.h> 
vector<int> nextPermutation(vector<int> &A, int n)
{
    //  Write your code here.
    int index  = -1;
    for(int i=n-2;i>=0;i--){
        //finding the element left of peak element
        if(A[i] < A[i+1]){
            index = i;
            break;
        }
    }
    if(index == -1){
        reverse(A.begin(),A.end());
        return A;
    }
    //finding element just bigger than index element
    for(int i = n-1;i > index ;i--){
        if(A[i] > A[index]){
            swap(A[i],A[index]);
            break;
        }
    }
    //reversing so that it becomes the smallest lexigraphical during next permutation
    reverse(A.begin() + index + 1,A.end());
    return A;

}
```

## Maximum subarray sum / Kadane's algorithm

https://www.codingninjas.com/codestudio/problems/maximum-subarray-sum_8230694?challengeSlug=striver-sde-challenge

### Approach

In this will iterate through all elements and will add them in sum and check whether sum is zero then no need to consider this element and will consider next element to be part of the subarray or else if past sum is positive even if that element is negative will add because in future we might get any positive number were overall subarray will contribute to be maximum

### Code
```
#include <bits/stdc++.h> 
long long maxSubarraySum(int arr[], int n)
{
    int start = -1;
    int ansStart = -1;
    int ansEnd = -1;
    long long sum = 0;
    long long maxi = LONG_MIN;
    for(int i=0;i<n ;i++){
        if(sum == 0) start = i;
        sum +=arr[i];

        if(sum > maxi){
            maxi = sum;
            ansStart = start;
            ansEnd = i;
        }
        if(sum < 0){
            sum = 0;
        }
    }
    //ansStart and ansEnd will be containg subarry start and end index with maximum sum
    return (maxi < 0) ? 0 : maxi;
}
```

## Stock Buy and Sell
https://www.codingninjas.com/codestudio/problems/best-time-to-buy-and-sell-stock_8230746?challengeSlug=striver-sde-challenge

### Approach
iterating from start to end and keeping track of minimum occured till so that from that element we can decide how much profit we can make , if profit is better than previous profit will update the profit.

### CODE

```
#include <bits/stdc++.h> 
int maximumProfit(vector<int> &A){
    // Write your code here.
    int mini = A[0];
    int profit = 0;
    for(int i = 1; i < A.size();i++){
        int cost = A[i] - mini;
        profit = max(profit , cost); //if neg profit will be zero only mean buy and sell on same day
        
        mini = min(mini,A[i]);
    }
    return profit;
}
```

## Rotate Image
https://leetcode.com/problems/rotate-image/

## Approach
step 1 transpose matrix  
step 2 reverse all rows of matrix  

### CODE
```
        //Step 1
        int n = matrix.size(); // n x n matrix
        for(int i = 0 ; i< n-1 ;i++){ //row traversal
            for(int j = i + 1 ; j<n ;j++){
                swap(matrix[i][j] , matrix[j][i]);
            }
        }

        //step 2
        for(int i=0;i<n;i++){
            reverse(matrix[i].begin(),matrix[i].end());
        }
```


## Rotate matrix clockwise

https://www.codingninjas.com/codestudio/problems/rotate-matrix_8230774?challengeSlug=striver-sde-challenge

## Approach 

using traversal like spiral , we will update elements of previous element

```

void rotateMatrixHelper(vector<vector<int>> &mat, int rowStart, int colStart, int rowEnd, int colEnd)
{
    // Base Condition
    if(rowStart >= rowEnd or colStart >= colEnd)
    {
        return; 
    }

    if (rowStart >= rowEnd - 1 || colStart >= colEnd - 1)
    { 
        return; 
    }

    int previous = mat[rowStart + 1][colStart]; 
    int current;
        
    // Move elements of first row from the remaining rows
    for (int i = colStart; i < colEnd; i++) 
    { 
        current = mat[rowStart][i]; 
        mat[rowStart][i] = previous; 
        previous = current; 
    } 

    rowStart++; 

    // Move elements of last column from the remaining columns 
    for (int i = rowStart; i < rowEnd; i++) 
    { 
        current = mat[i][colEnd-1]; 
        mat[i][colEnd-1] = previous; 
        previous = current; 
    } 
    colEnd--; 

    // Move elements of last row from the remaining rows 
    if (rowStart < rowEnd) 
    { 
        for (int i = colEnd - 1; i >= colStart; i--) 
        { 
            current = mat[rowEnd-1][i]; 
            mat[rowEnd-1][i] = previous; 
            previous = current; 
        } 
    } 
    rowEnd--; 

    // Move elements of first column from the remaining rows 
    if (colStart < colEnd) 
    { 
        for (int i = rowEnd-1; i >= rowStart; i--) 
        { 
            current = mat[i][colStart]; 
            mat[i][colStart] = previous; 
            previous = current; 
        } 
    } 
    colStart++; 

    // Recursively rotate inner rings
    rotateMatrixHelper(mat, rowStart, colStart, rowEnd, colEnd);

}

void rotateMatrix(vector<vector<int>> &mat, int n, int m)
{
    // Recursive function to rotate the matrix
	rotateMatrixHelper(mat, 0, 0, n, m);
}
```
