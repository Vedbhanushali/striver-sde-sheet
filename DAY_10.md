# DAY 10

## Unique paths

https://www.codingninjas.com/studio/problems/unique-paths_8230802?challengeSlug=striver-sde-challenge  
https://leetcode.com/problems/unique-paths/description/  

### Approach 

1. DP approach  
there are two possibility going down or right for every block so recursively will call two ways from particular block is reached end will consider that path if down go beyound number of row return 0 or right go beyond number of column will return 0.

2. Mathematical approach  
here number of rows and number of columns = m, n so  
No. of ways ot going right is m -1  
and No. of ways of going down is n - 1  
so total ways will be m + n -2 where R and D will be permutation of them   
to solve thisNow I will be chossing from N boxes places for M (that is placing Down D)  
then automatically R will adjust in remaining places  
so finding NCR

### CODE
```
class Solution {
public: 
    int solveRE(int i,int j,int m,int n,vector<vector<int>> &dp){
        if(i==(m-1) && j==(n-1)) return 1;
        if(i>=m || j>=n) return 0;

        if(dp[i][j]!=-1) return dp[i][j];
        //down and right
        else return dp[i][j] = solveRE(i+1,j,m,n,dp) + solveRE(i,j+1,m,n,dp);
    }
    int uniquePaths(int m, int n) {
        //recursive solution DP
        // vector<vector<int> > dp(m,vector<int> (n,-1));
        // return solveRE(0,0,m,n,dp);

        //Mathematical solution 
        int N = m + n -2; // N is number of boxes where we will put D or R
        double r = m - 1; //Now I will be chossing from N boxes places for M (that is placing Down D)
        //then automatically R will adjust in remaining places
        //so finding NCR
        int res = 1;
        for(int i=1;i<=r;i++){
            res = res * (N-r+i) / i;
        }
        // 8 * 9 * 10 / 1 * 2 * 3
        return (int)res;
        
    }
};
```

## Reverse Pairs 

https://www.codingninjas.com/studio/problems/reverse-pairs_8230825?challengeSlug=striver-sde-challenge

### Approach

Similar approach as [Inversion pairs](DAY_9.md)  
using merge Sort finding the pairs such that it satisfies the condition arr[i] > arr[j]*2 , where i<j  

### CODE

```
class Solution {
public:
    int merge(vector<int> & arr,int low,int high){
        int mid = low + (high-low)/2;

        //left of mid and right of mid need to be merged
        vector<int> temp; // temporary array
        int left = low;      // starting index of left half of arr
        int right = mid + 1;   // starting index of right half of arr

        //Modification 1: cnt variable to count the pairs:

        //storing elements in the temporary array in a sorted manner//
        int i = mid;
        int j = high;
        int count = 0;
        while(i>=low && j>mid){
            if(arr[i] > (long long int)arr[j]*2){
                count = count + (j-mid);
                i--;
            } else {
                j--;
            }   
        }
        while (left <= mid && right <= high) {
            if (arr[left] <= arr[right]) {
                temp.emplace_back(arr[left]);
                left++;
            }
            else {
                temp.emplace_back(arr[right]);
                right++;
            }
        }

        // if elements on the left half are still left //

        while (left <= mid) {
            temp.emplace_back(arr[left]);
            left++;
        }

        //  if elements on the right half are still left //
        while (right <= high) {
            temp.emplace_back(arr[right]);
            right++;
        }

        // transfering all elements from temporary to arr //
        for (int i = low; i <= high; i++) {
            arr[i] = temp[i - low];
        }

        return count; // Modification 3
    }
    int mergeSort(vector<int> & nums,int low,int high){
        if(low >= high) return 0;
        int count = 0;
        int mid = low + (high-low)/2;
        count += mergeSort(nums,low,mid);
        count += mergeSort(nums,mid+1,high);
        count += merge(nums,low,high);
        return count;
    }
    int reversePairs(vector<int>& nums) {
        return mergeSort(nums, 0, nums.size() - 1);
    }
};
```
## Longest Consecutive Sequence

https://www.codingninjas.com/studio/problems/longest-consecutive-sequence_8230708?challengeSlug=striver-sde-challenge

### Approach 

approach wrritten in code 

### Code
```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n = nums.size();
        if(n==0 || n==1) return n;
        
        //approach 1 using sorting
        // O(nlogn) approach
        /*
        sort(nums.begin(),nums.end());
        int ans = 1;
        int maxi = 1;
        for(int i = 1;i<n;i++){
            if(nums[i]==nums[i-1]+1){
                maxi++;
            } else if(nums[i]==nums[i-1]){
                //do nothing
            } 
            else {
                maxi = 1;
            }
            ans = max(maxi,ans);
        }
        return ans;
        */

        //2nd approach using hashSet 
        /*
        * Time Complexity: The time complexity of the below approach is O(N) because 
        * we traverse each consecutive subsequence only once. (assuming HashSet takes O(1) to search)
        * Space Complexity: The space complexity of the above approach is O(N) because we are   
        * maintaining a HashSet.
        *
        *
        *
        */

        set<int> hashSet;
        for(auto i:nums){
            hashSet.insert(i);
        }

        int ans = 1;
        for(auto num:nums){
            if (!hashSet.count(num - 1)) { //mean is starting of sequence is found
                                           // for example 1 2 3 4 , 1 is starting 
                int maxi = 1;
                while(hashSet.count(num+1)){
                    num++;
                    maxi++;
                }
                ans = max(maxi,ans);
            }
        }
        return ans;
    }
};
```

## Longest Subarray with zero sum

https://www.codingninjas.com/studio/problems/longest-subarray-zero-sum_8230747?challengeSlug=striver-sde-challenge

### approach 

Using prefix SUM will calculate all prefix sum of array and will track element with index in hashmap and when traversing element if that element exist  in hashmap mean subarray between is zero or in one case if that prefix element is zero then from starting to that element subarray will become 0 and will update the distance accordingly.

### code

```
#include <bits/stdc++.h>

int LongestSubsetWithZeroSum(vector < int > arr) {
  if(arr.size()==0 || arr.size()==1){
    return arr.size();
  }
  // Write your code here
  int ans = 0;
  unordered_map<int,int> hashMap;
  hashMap[arr[0]] = 0; // 0 is index
  for(int i=1;i<arr.size();i++){
    arr[i] += arr[i-1];
    if(arr[i]==0){
      ans = max(ans,i+1);
    }
    if(hashMap.find(arr[i])!=hashMap.end()){
      //mean found first occurence
      ans = max(ans,i-hashMap[arr[i]]);
    } else {
      hashMap[arr[i]] = i;
    }
  }
  return ans;
}
```