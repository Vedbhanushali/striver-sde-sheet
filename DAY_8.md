# DAY 8

## Merge Intervals

https://www.codingninjas.com/studio/problems/merge-intervals_8230700?challengeSlug=striver-sde-challenge

### approach - 
will maintain a pair and will iterate all elements of itervals if they are intersecting then will update the pair which we are holding if not intersecting then will push that pair in answer.

### CODE - 
```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        pair<int,int> p;
        sort(intervals.begin(),intervals.end());
        p = {intervals[0][0],intervals[0][1]};
        vector<vector<int>> ans;
        for(int i = 1;i<intervals.size() ;i++){
            int new_start = intervals[i][0];
            int new_end = intervals[i][1];
            if(new_start >= p.first && new_start <=p.second){
                //mean inside
                p.second = max(new_end,p.second);
            } else {
                vector<int> temp = {p.first,p.second};
                ans.emplace_back(temp);
                p = {new_start,new_end};
            }
        }
        vector<int> temp = {p.first,p.second};
        ans.emplace_back(temp);
        return ans;
    }
};
```


## find the duplicate in an array of n integers

https://www.codingninjas.com/studio/problems/missing-and-repeating-numbers_8230733?challengeSlug=striver-sde-challenge

### approach - 
three pointer approach j pointing to end of arr2, i pointing to values of arr1 end of where last element is present and k which is pointing at index of arr1 which is last which will have largest element of both. and will move i , j and k left such that if element at i and j are compared and filled at place of k.

### CODE - 
```class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        /* Fake pass method 
        we are actually creating new array and swaping pointers of original
        vector<int> ans(m+n);
        int i = 0;
        int j = 0;
        int k = 0;
        while(i<m && j < n){
            if(nums1[i]<nums2[j]){
                ans[k++] = nums1[i++];
            } else {
                ans[k++] = nums2[j++];
            }
        }
        //if any one remains
        while(i<m){
            ans[k++] = nums1[i++];
        }
        while(j<n){
            ans[k++] = nums2[j++];
        }
        swap(nums1,ans);
        */

        /*
        * actual method
        */
        //two pointer approach considering from largest and placing at last till any arry is finished
        int i = m-1;
        int j = n-1;
        int k = m+n-1;

        while( i>=0 && j>=0){
            if(nums1[i] > nums2[j]){
                swap(nums1[k],nums1[i]);
                i--;k--;
            } else {
                swap(nums2[j],nums1[k]);
                j--;k--;
            }
        }

        while( i >=0 ){
            nums1[k--] = nums1[i--];
        }
        while( j>= 0){
            nums1[k--] = nums2[j--];
        }
    }
};

```

## Find the Duplicate Number

https://www.codingninjas.com/studio/problems/missing-and-repeating-numbers_8230733?challengeSlug=striver-sde-challenge

### approach

just like finding cycle in linked list and finding their intersection will use two pointers slow and fast, here movement will be based on value considered as index, when loop is find mean slow and fast meet to find duplicate we can find point of intersection by pointing fast at begining and moving both slow and fast 1 time so where they meet it is duplicate element.

### code
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        //Actual method of solving
        // just like finding cycle in linked list and finding their intersection will use two pointers slow and fast, here movement will be based on value considered as index, when loop is find mean slow and fast meet to find duplicate we can find point of intersection by pointing fast at begining and moving both slow and fast 1 time so where they meet it is duplicate element.
        // int n = nums.size();
        // int slow = 0; //pointing at first element
        // int fast = 0; //pointing at first element
        // // 1 4 3 2 , n = 4 
        // while(fast!=n){
        //     slow = nums[slow];
        //     fast = nums[nums[fast]];
        //     if(slow == fast) break;
        // }
        // if(fast==n) return -1; //mean no duplicate find
        // else{
        //     //slow == fast;
        //     fast = 0; //pointing at beginning and move again
        //     while(slow != fast){
        //         slow = nums[slow];
        //         fast = nums[fast];
        //     }
        //     return nums[slow];
        // }

        int slow = nums[0];
        int fast = nums[0];
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);
        fast = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
        // 1st approoach using sort - no to use beacuse we are modifying the array
        // TC - O(nlogn)
        // SC - O(n)
        // sort(nums.begin(),nums.end());
        // for(int i=0;i<nums.size()-1;i++){
        //     if(nums[i]==nums[i+1]){
        //         return nums[i];
        //     }
        // }
        // return -1;

        //-------------------------
        //2nd approach negatiing visited solutions
        // int index = 0;
        // for(int i=0;i<nums.size();i++){
        //     if(nums[i]<0){
        //         index = -nums[i];
        //     } else {
        //         index = nums[i];
        //     }
        //     if(nums[index]<0){
        //         // return nums[i]<0?-nums[i]:nums[i];
        //         return index;
        //     } else {
        //         nums[index] = -nums[index];
        //     }
        //     // for(auto i : nums){
        //     //     cout<<" "<<i;
        //     // }
        //     // cout<<endl;
        // }
        // return -1;

        //-------------------------------------
        //3rd approach in this we will swap values to their index and we before swaping we will check whther already an value is present or not 
        // for(int i=0;i<nums.size();i++){
        //     int index = nums[0];
        //     if(nums[index]==index){
        //         return index;
        //     } else {
        //         swap(nums[0],nums[index]);
        //     }
            
        // }
        // return -1;

        // long long int maxi = INT_MIN;
        // long long int sum = 0;
        // for(int i=0;i<nums.size();i++){
        //     // maxi = max(nums[i],maxi);
        //     if(nums[i] > maxi){
        //         maxi = nums[i];
        //     }
        //     sum += nums[i];
        // }
        // long long int actualsum = ((maxi+1)*(maxi))/2;
        // return sum - actualsum;
    }
};
```

## FourSum

https://www.codingninjas.com/studio/problems/find-four-elements-that-sums-to-a-given-value_8230785?challengeSlug=striver-sde-challenge

### Approach
sorting nums so that we can remove duplicate entries for uniqueness   
1 loop for considering 1st element  
2 loop for considering 2nd element which will be after 1st in nums  
and 3rd and 4th element can be found using 2 pointer approach of 2 sum where new_target is target-arr[i]-arr[j]  

### CODE
```
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        //TC - O(n3) using hashmap method
        // sort(nums.begin(),nums.end());
        // set<vector<int> > ans;
        // vector<vector<int> > answer;
        // int n = nums.size();
        // for(int i = 0;i<n;i++){
        //     for(int j = i+1;j<n;j++){

        //         unordered_set<long long int> hashSet;
        //         long long sum = (long)target - nums[i] - nums[j];
        //         for(int k = j+1 ; k<n ;k++ ){
        //             if(hashSet.find(sum - nums[k])!=hashSet.end()){
        //                 //mean found
        //                 vector<int> temp = {nums[i],nums[j],nums[k],(int)sum-nums[k]};
        //                 ans.insert(temp);
        //             }
        //             hashSet.insert(nums[k]);
        //         }
        //     }
        // }
        // for(auto i : ans){
        //     answer.emplace_back(i);
        // }
        // return answer;


        //method using two pointer
        vector<vector<int>> ans;
        int n = nums.size();
        sort(nums.begin(), nums.end());
        
        for (int i = 0; i < n - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1])
                continue; //for uniqueness 1st
            
            for (int j = i + 1; j < n - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1])
                    continue; //for uniqueness 2nd
                
                int left = j + 1;
                int right = n - 1;
                
                while (left < right) {
                    long long sum = nums[i];
                      sum += nums[j];
                      sum += nums[left];
                      sum += nums[right];
                    
                    if (sum == target) {
                        ans.push_back({nums[i], nums[j], nums[left], nums[right]});
                        left++;
                        right--;
                        
                        while (left < right && nums[left] == nums[left - 1])
                            left++;
                        while (left < right && nums[right] == nums[right + 1])
                            right--;
                    } else if (sum < target) {
                        left++;
                    } else {
                        right--;
                    }
                }
            }
        }
        
        return ans;   
    }
};
```
