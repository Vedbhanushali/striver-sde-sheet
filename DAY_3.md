# DAY 3

## Sort an array of 0's, 1's and 2's

https://www.codingninjas.com/codestudio/problems/sort-0-1-2_8230695?challengeSlug=striver-sde-challenge
sol -

### Approach
three pointer inplace sorting
will use three pointers low from which all elements left of it would be zero, mid pointer which have all left elements 1 mean if one encountered move forward, and high pointer where all elements right to it would be 2.  
we will only move mid pointer , if mid element is 1 do nothing move mid,  
if mid element is zero swap element with low pointer and move low++,  
if mid element is two swap element with high pointer and move high--;
### Code -
```
#include <bits/stdc++.h> 
void sort012(int *nums, int n)
{
   //   Write your code here
   int low=0,mid=0,high=n-1;
        while(mid<=high){
            if(nums[mid]==0){
                swap(nums[mid],nums[low]);
                low++;
                mid++;
            }
            else if(nums[mid]==1){
                mid++;
            } else if(nums[mid]==2){
                swap(nums[mid],nums[high]);
                high--;
            }
        }
}
```

## Find Duplicate in Array

approach in this we will swap values to their index and we before swaping we will check whther already an value is present or not 

```
#include <bits/stdc++.h>

int findDuplicate(vector<int> &nums, int n){
	// Write your code here.
	int temp = 0;
	for(int i=0;i<nums.size();i++){
            int index = nums[0];
            if(nums[index]==index){
                return index;
            } else {
                // swap(nums[0],nums[index]);
				temp = nums[0];
				nums[0] = nums[index];
				nums[index] = temp;
            }
            
        }
        return -1;
}

```