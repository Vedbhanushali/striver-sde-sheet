# DAY 6

## Reverse a word in string

https://www.codingninjas.com/codestudio/problems/reverse-words-in-a-string_8230698?challengeSlug=striver-sde-challenge&leftPanelTab=0

approach - 
1. we will first reverse whole string and one by will reverse each words/
```
reverse(s.begin(),s.end());
        //manually triming space;
        int x = 0;
        while(s[x]==' '){
            x++;
        }
        s = s.substr(x,s.length()-x);
        //back trim
        x = s.length() - 1;
        while(s[x]==' '){
            x--;
        }
        s = s.substr(0,x+1);
        int start = 0;
        int i;
        for(i=0;i<s.length();i++){
            char ch = s[i];
            if(ch==' ' && s[i-1]==' '){
                s = s.substr(0,i) + s.substr(i+1,s.length());
                i--;
            }
            if(ch==' ' && s[i-1]!=' '){
                reverse(s.begin()+start,s.begin()+i);
                start = i+1;
            } 
        }
        if(start<i){
            reverse(s.begin()+start,s.begin()+i);
        }
        return s;
```

### 2nd approach

2. traverse from start and store the all strings and append next word before ans so it gets reversed

CODE
```     
        //manually triming space;
        int x = 0;
        while(s[x]==' '){
            x++;
        }
        s = s.substr(x,s.length()-x);
        //back trim
        x = s.length() - 1;
        while(s[x]==' '){
            x--;
        }
        s = s.substr(0,x+1);
        
        //traverse the string
        int end = s.size();
        int start = 0;
        string temp="";
        string ans="";
        //triming from start
        int i=0;
        while(s[i]==' '){
            i++;
        }
        for(;i<end;i++){
            char ch = s[i];
            // cout<<ch<<" ";
            if(ch!=' '){
                temp = temp + ch;
                // cout<<temp<<endl;/
            } else if(ch==' ') {
                cout<<temp<<" "<<endl;
                if(ans=="") ans = temp;
                else if(ans!="" && temp!="") ans = temp +" "+ ans;
                
                temp = "";
                // coutM
            }
        }
        if(temp!="") {
            if(ans!="") ans = temp + " " + ans;
            else ans = temp;
        } 
        return ans;
```

## Longest Palindromic Substring



### approach - 
two pointer approach will expand two cases odd and even  
for every letter in string one by one will try to expand from that letter 
if s = cbbbdcand index = 2
odd expansion is  
b  
bbb  
cbbbd - stop as c and d not equal  
even expansion is   
bb  
cbbb - stop as c and b not equal  
and this way storing max string.  

### CODE
```
class Solution {
public:
    void expandAroundIndex(string &s,int i,int j,string &ans){
        
        int count = 0;
        if(i==j) {i--;j++;count++;}
        while(i>=0 && j<s.length() && s[i] == s[j]){
            count+=2;
            i--;
            j++;
        }
        // cout<<ans<<" "<<count<<" - before"<<i<<" : "<<j<<endl;
        if(count > ans.length()){
            // if((j-i) & 1){
            //     //odd
            //     ans = s.substr(i+1,j-1);
            // } else {
            //     ans = s.substr(i+1,j);
            // }
            // if(count&1){
            //     ans = s.substr(i+1,j-1);
            // } else {
            //     ans = s.substr(i+1,j-1);    
            // }
            if(i == -1){
                ans = s.substr(i+1,j);
            } else
            ans = s.substr(i+1,j-1-i);
        } 
        // cout<<ans<<" "<<count<<" - after"<<endl<<endl;
    }
    string longestPalindrome(string s) {
        if(s.length() == 1) return s;
        int count = 0;
        int n = s.length();
        string ans = "";
        for(int i=0;i<n;i++){
            //odd
            cout<<endl<<endl<<"odd call"<<endl;
            expandAroundIndex(s,i,i,ans);
            //even
            cout<<"even call"<<endl;
            expandAroundIndex(s,i,i+1,ans);
        }
        return ans;

        // //substring
        // // two pointer approach
        // // odd even moving
        // string largest = "";
        // //odd traversal
        // int i = 0;
        // int n = s.size();
        // int large = 1;
        // while(i<n){
        //     int l = i-1;
        //     int r = i+1;
        //     int count = 1;
        //     for(;l>=0 && r<n;l--,r++){
        //         if(s[l]!=s[r]) break;
        //         count += 2; //mean equal
        //     }
        //     if(count>large){
        //         large = count;
        //         largest = s.substr(l+1,r-1);
        //     }
        //     i++; 
        // }

        // //even traversal
        // i = 0;
        // int j = i+1;
        // while(j<n){
        //     int l = i;
        //     int r = j;
        //     int count = 0;
        //     for(;l>=0 && r<n;l--,r++){
        //         if(s[l]!=s[r]) break;
        //         count += 2; //mean equal
        //     }
        //     if(count>large){
        //         large = count;
        //         largest = s.substr(l+1,r-1);
        //     }
        //     i++;
        //     j++;
        // }
        // return largest;
    }
};
```
