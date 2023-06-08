# DAY 5

## 2SUM / PAIR SUM
https://www.codingninjas.com/codestudio/problems/pair-sum_8230699?challengeSlug=striver-sde-challenge

### approach

using two pointer approach I find whether sum of both end points  i is start and j is end
if sum is greater j--  
if sum is smaller i++  
if sum is same then consider i is fixed and will check all possible pair with j and less than  
and will increment i++  


```
#include <bits/stdc++.h>

vector<vector<int>> pairSum(vector<int> &arr, int s){
   // Write your code here.
   // two approach hashmap  and two pointer
   sort(arr.begin(),arr.end());
   int i =0 , j = arr.size()-1;
   vector<vector<int> > answer;

   while(i<j){
      if(arr[i] + arr[j] < s){
         i++;
      }
      else if(arr[i] + arr[j] > s){
         j--;
      }else {
      // if(arr[i] + arr[j] == s){

      //    vector<int> temp(2);
      //    temp[0] = arr[i];
      //    temp[1] = arr[j];
      //    answer.emplace_back(temp);
      //    // i++;
      //    j--;
      // }
      // i is fixed
      int x = j;
      while (arr[i] + arr[x] == s && x > i) {
        
        vector<int> temp(2);
        temp[0] = arr[i];
        temp[1] = arr[x];
        answer.emplace_back(temp);
        x--;
      }
      i++;
      }
   }
   return answer;
}
```