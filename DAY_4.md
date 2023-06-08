# Day 4

## Majority element
https://www.codingninjas.com/codestudio/problems/day-6-majority-element_8230731?challengeSlug=striver-sde-challenge&leftPanelTab=0

### Approach - 

finding element occuring more than n/2 using a counter and again checking whether it is occuring more greater than n/2.

```c++
#include <bits/stdc++.h>

int findMajorityElement(int nums[], int n) {
	// Write your code here.
	int count = 0;
        int element = 0;
        for(int i=0;i<n;i++){
            if(count == 0){
                element = nums[i];
                count++;
            } else {
                if(element == nums[i]){
                    count++;
                } else {
                    count--;
                }
            }
        }
        // return element;
		int cnt1 = 0;
		for(int i = 0;i<n;i++){
			if(nums[i] == element) cnt1++;
		}
		return (cnt1>n/2) ? element : -1;

}
```

## Majority element II


### Approach
finding element occuring more than n/3 times  
here will maintain frequence of 2 elements and according to logic if matches will increase their freqency  else decrase and if freq is zero will replace it with new element so this way will have two elements which can be occuring more than n/3 times will iterate in whole array again and check their occuring frequence and will add them in answer.

```
#include <bits/stdc++.h>

vector<int> majorityElementII(vector<int> &nums)
{
    // Write your code here.
   int num1 = 0;
        int num2 = 0;
        int f1 = 0;
        int f2 = 0;
        int n = nums.size();
        for(int i=0;i<n;i++){
            if(nums[i] == num1){
                f1++;
            }
            else if(nums[i] == num2){
                f2++;
            }
            else if(f1 == 0){
                num1 = nums[i];
                f1++;
            }
            else if (f2 == 0){
                num2 = nums[i];
                f2++;
            } else {
                f1--;
                f2--;
            }
        }
        int count1 = 0;
        int count2 = 0;
        for(int i=0;i<n;i++){
            if(num1 == nums[i]){
                count1++;
            } else if(num2 == nums[i]){
                count2++;
            }
        }
        vector<int> ans;
        if (count1 > n/3) ans.emplace_back(num1);
        if(count2 > n/3)  ans.emplace_back(num2);
        return ans;
}
```
