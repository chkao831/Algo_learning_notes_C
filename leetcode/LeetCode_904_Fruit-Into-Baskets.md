### Fruit Into Baskets
https://leetcode.com/problems/fruit-into-baskets/
>Given the integer array `fruits`, return the maximum number of fruits you can pick.

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fs) {
        unordered_map<int, int> memo;
        int l=0, r=0, n=fs.size(), ans=0;

        while(r<n){
            if(memo.find(fs[r])!=memo.end()){
                memo[fs[r]]+=1;
            }else{
                while(memo.size()>1){
                    memo[fs[l]]-=1;
                    if(memo[fs[l]]==0)
                        memo.erase(fs[l]);
                    l++;
                }
                memo[fs[r]]+=1;
            }
            r++;
            ans=max(ans, r-l);
        }
        return ans;
    }
};
```

#### Remark:
- `unordered_map` access takes time complexity of O(logN)
- if key exists in map, then `(map.find(key) != memo.end())` 
- if key does not exist in map, then `(map.find(key) == memo.end())` 
- do delete entry from map, do `map.erase(key)`
- `max(ele1, ele2)` only takes two elements, not more.
#### Submission:
```
```
#### Complexity:
- Time: O(N)
- Space: O(2) = O(1)
