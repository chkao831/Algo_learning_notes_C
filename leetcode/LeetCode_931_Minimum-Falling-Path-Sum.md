### Minimum Falling Path Sum
https://leetcode.com/problems/minimum-falling-path-sum/
>Given an `n` x `n` array of integers `matrix`, return the minimum sum of any falling path through `matrix`.
```cpp
class Solution {
public:
    int ans=INT_MAX;
    map<pair<int,int>, int> memo;
    int dfs(int x, int y, int n, vector<vector<int>>& matrix){

        if (!(0<=y && y<n)){
            return INT_MAX;
        }
        if (x == n-1){
            return matrix[x][y];
        }
        if(memo.find({x,y})!=memo.end()){
            return memo[{x,y}];
        }
        int left = dfs(x+1, y-1, n, matrix);
        int middle = dfs(x+1, y, n, matrix);
        int right = dfs(x+1, y+1, n, matrix);

        return memo[{x,y}] = matrix[x][y] + min(left, min(middle, right));
    }
    int minFallingPathSum(vector<vector<int>>& matrix) {
        int n=matrix.size();
        for(int i=0; i<n; i++){
            ans= min(ans, dfs(0,i,n,matrix));
        }
        return ans;
        
    }
};
```
#### Remark:
- 
#### Submission:
```
```
#### Complexity:
- Time: O(N*3^N) - 對於每個起點，啟三叉樹
- Space: O(N) - depth of the recursive stack
