# DAY 9

## Missing and repeating numbers

https://www.codingninjas.com/studio/problems/missing-and-repeating-numbers_8230733?challengeSlug=striver-sde-challenge

### Approach

xor all - x  
x ^ ( 1 to n xor 1 ^ 2 ^ ... ^ n) - y  
x ^ y = ans  
separate in 2 block (of nums) where msb is set and msb is not set of ans  
this way missing will be separated in one bucket and another will not contain repeating  
now xor this two buckets from 1 to n (separated from msb of ans) this way they will only remain because one  
one bucket contains repeating char 2 times and one more gets add in 3 total so one remains and other buckets doesn't have that number at all which is missing
so one number remains their as well  

### CODE

```
#include <bits/stdc++.h>

pair<int,int> missingAndRepeating(vector<int> &nums, int n)
{
	
	int sum = 0;
	for(int i = 0;i<nums.size();i++){
		sum = sum ^ nums[i];
		sum = sum ^ (i+1);
	}
	//right most 1 bit and 0 bit differentiator
	int bit_diff = sum & ~(sum-1);
	int missing = 0;
	int repeating = 0;
	for(int i = 0;i<nums.size();i++){
		if(bit_diff & nums[i]){
			//bit set
			missing = missing ^ nums[i];
		} else {
			repeating = repeating ^ nums[i];
		}
		if(bit_diff & (i+1)){
			missing = missing ^ (i+1);
		} else {
			repeating = repeating ^ (i+1);
		}
	}
	int r_cnt = 0,m_cnt = 0;
	for(int i=0;i<nums.size();i++){
		if(nums[i]==repeating) r_cnt++;
		if(nums[i]==missing) m_cnt++;
	}
	if(r_cnt < m_cnt ) swap(repeating,missing);
	return {missing,repeating};
}

```

## Count Inversion

https://www.codingninjas.com/studio/problems/count-inversions_8230680?challengeSlug=striver-sde-challenge

### approach

in given 2 sorted array   
arr1 - 3 5 4 5 and arr2 - 1 2 3 3   
i pointing at index 0 of arr1   
j pointing at index 0 of arr2  
if arr1[i] > arr2[j] mean all element after arr1[i] will be greater than arr2[j] mean (n(size of arr1) - i) element satisfies   

we will use this concept to find inversion using merge sort  

[2 5 1]|[ 3 4]  

[2 5]| [1]       [3]|[4]  
 
[2]|[5]    [1]     [3]   [4]  

applying logic in [2] [5] , i , j , count = 0;  
[25]    [1]       [3]    [4]  
25   1 logic apply count = 2   and 3   4 logic apply count = 0  
[125]     [34]  
125 and 34 logic apply where (i at 5 and j at 3 count = 1) and (i at 5 and j at 4 count = 1)  
total ans  = 4. (all count summation)  

### CODE
```
#include <bits/stdc++.h> 
int merge(long long *arr,int low,int high){
    int mid = low + (high-low)/2;

    //left of mid and right of mid need to be merged
    vector<int> temp; // temporary array
    int left = low;      // starting index of left half of arr
    int right = mid + 1;   // starting index of right half of arr

    //Modification 1: cnt variable to count the pairs:
    int cnt = 0;

    //storing elements in the temporary array in a sorted manner//

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left]);
            left++;
        }
        else {
            temp.push_back(arr[right]);
            cnt += (mid - left + 1); //Modification 2
            right++;
        }
    }

    // if elements on the left half are still left //

    while (left <= mid) {
        temp.push_back(arr[left]);
        left++;
    }

    //  if elements on the right half are still left //
    while (right <= high) {
        temp.push_back(arr[right]);
        right++;
    }

    // transfering all elements from temporary to arr //
    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }

    return cnt; // Modification 3
}
int mergeSort(long long *arr,int low,int high){
    if(low >= high) return 0;
    int count = 0;
    int mid = low + (high-low)/2;
    count += mergeSort(arr,low,mid);
    count += mergeSort(arr,mid+1,high);
    count += merge(arr,low,high);
    return count;
}
long long getInversions(long long *arr, int n){ 
    // Write your code here.
    return mergeSort(arr, 0, n - 1);
}
```

## Search in 2D matrix

https://www.codingninjas.com/studio/problems/search-in-a-2d-matrix_8230773?challengeSlug=striver-sde-challenge

### approach

normal binary search considering m x n matrix as liner 0 to (m*n)-1 element mid is between them
not to find corrdinates of that element between them row = mid/n (n is no of column) and col = mid % n  

### CODE

```
bool searchMatrix(vector<vector<int>>& mat, int target) {
    int m = mat.size();
    int n = mat[0].size();
    // n x m matrix
    int total =n * m;

    int low = 0 ;
    int high =  total -1;
    int mid = low + (high - low)/2;
    while(low <= high){
        int row = mid / n;
        int col = mid % n;
        if(mat[row][col]==target) return true;
        else if(mat[row][col] < target){
            low = mid + 1;
        } else {
            high = mid - 1;
        }
        mid = low + (high-low)/2;
    }
    return false;
}
```

## Pow(x,n)

### approach 
using exponential divide and conqure method    
example - pow(10,5) - 10 * 10 * 10 * 10  
can be written as   
(10 * 10) * (10 * 10) * 10  
here 10 is computed which will not be calculated again  
another example pow(9,10)  
can be written as   
(9 * 9 * 9 * 9 * 9) * (9 * 9 * 9 * 9 * 9)  
and pow(9,5) will be calculated as above this way we save many operations by dividing similar steps  

### CODE

```
#include <bits/stdc++.h>
long long int solve(int x,int n,int m){
	if(n==0) return 1;

        long long int ans = solve(x,n/2,m);
        if(n<0){
            //went inside
            cout<<"went inside"<<endl;
            if(n&1){
                return ((ans * ans) /x)%m;
            } else {
                return (ans * ans)%m;
            }
        } else {
            if(n&1){ //odd
            	return (((ans * ans)%m) * x)%m;
            } else {
                return (ans * ans)%m;
            }
        }
}
int modularExponentiation(int x, int n, int m) {
	// Write your code here.
	return solve(x,n,m)%m;
}
```