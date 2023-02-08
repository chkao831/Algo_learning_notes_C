# Jump Game II
https://leetcode.com/problems/jump-game-ii/description/
>Return the minimum number of jumps to reach `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.
## DFS
### First Attempt: DFS - Top Down with Cache: TLE
```cpp
class Solution {
public:
    int min_jump = INT_MAX;
    vector<int> memo;
    void dfs(int idx, int current_jump, vector<int>& nums){
        if (idx >= nums.size() - 1){
            min_jump = min(min_jump, current_jump);
            return;
        }
        if(memo[idx] != -1 && memo[idx] < current_jump){
            return;
        } else {
            memo[idx] = current_jump;
        }

        for(int i=nums[idx]; i>0; i--){
            dfs(idx+i, current_jump+1, nums);
        }
    }
    int jump(vector<int>& nums) {
        memo.resize(nums.size(), -1);
        dfs(0, 0, nums);
        return min_jump;
    }
};
```
#### Remark:
- 


### DFS - Bottom Up with Cache
```cpp
class Solution {
public:

    vector<int> memo;
    int dfs(int idx, vector<int>& nums){
        if(idx >= nums.size()-1){
            return 0;
        }
        if(memo[idx] != -1){
            return memo[idx];
        }
        int cur_min_step = nums.size();
        for(int i=nums[idx]; i>0; i--){
            cur_min_step = min(cur_min_step, dfs(idx+i, nums)+1);
        }
        return memo[idx] = cur_min_step;
    }
    int jump(vector<int>& nums) {
        memo.resize(nums.size(), -1);
        int min_jump = dfs(0, nums);
        return min_jump;
    }
};
```
#### Remark:
- 和Top Down關鍵區別在於：Top Down每次下來走到重複的路時，其實那個cache值仍然不是最後確定的，還要check是不是比現在最優還好，是的話才update。Bottom Up從下面上來，上來到了一個點，其後的cache已經是最短路徑了。兩者時間複雜度相同，但在極端case會有運算上的區別。
- 這裡的cache是一個vector

#### Complexity:
- Time: O(N^2)
- Space: O(N)

## BFS
```cpp
class Solution {
public:


    int jump(vector<int>& nums) {
        int level_end = 0, cur_farthest = 0;
        int levels = 0;

        if (nums.size()==1){
            return 0;
        }

        for(int i=0; i<nums.size()-1; i++){
            cur_farthest = max(cur_farthest, i+nums[i]);
            if (cur_farthest >= nums.size()-1){
                levels++;
                break;
            }
            // Visited all the items on the current level, make the queue size for the next level
            if (i==level_end){
                level_end = cur_farthest;
                levels++;
            }
        }
        return levels;
    }
};
```
#### Complexity:
- Time: O(N)
- Space: O(1)
