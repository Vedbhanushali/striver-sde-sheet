# Day - 1

## Question - Set Matrix Zeros 

https://www.codingninjas.com/codestudio/problems/set-matrix-zeros_8230862?challengeSlug=striver-sde-challenge

### CODE  

```
#include <bits/stdc++.h>

void setZeros(vector<vector<int>> &matrix)
{
	// Write your code here.
	vector<int> row;
	vector<int> col;

	for(int i=0;i<matrix.size();i++){
		for(int j=0;j<matrix[0].size();j++){
			if(matrix[i][j] == 0){
				row.emplace_back(i);
				col.emplace_back(j);
			}
		}
	}
	//converting all row
	for(auto i:row){
		for(int j=0;j<matrix[0].size();j++){
			matrix[i][j] = 0;
		}
	}

	//converting all column
	
	for(auto i:col){
		for(int j=0;j<matrix.size();j++){
			matrix[j][i] = 0;
		}
	}
}
```