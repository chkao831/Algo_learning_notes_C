### Shuffle the Array
https://leetcode.com/problems/shuffle-the-array/description/
>Given the array `nums` consisting of `2n` elements in the form `[x1,x2,...,xn,y1,y2,...,yn]`.
>
>Return the array in the form `[x1,y1,x2,y2,...,xn,yn]`.
```cpp
class Solution {
public:

    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> big_vec; big_vec.reserve(2*n);
        int l=0, r=n;
        for(int i=0; i<n; i++){
            big_vec.push_back(nums[l]);
            big_vec.push_back(nums[r]);
            l++;
            r++;
        }
        return big_vec;
    }
};
```

#### Complexity:
- Time: O(n)
- Space: O(n)

#### In-place
```cpp
class Solution {
public:

    vector<int> shuffle(vector<int>& nums, int n) {
        int even_ptr=0, odd_ptr=n; //move slower than the below loop
        for(int i=0; i<nums.size(); i++){
            if(i % 2 == 0){
                nums[i] = (nums[even_ptr]%1001)*1001 + nums[i];
                even_ptr += 1;
            } else {
                nums[i] = (nums[odd_ptr]%1001)*1001 + nums[i];
                odd_ptr += 1;
            }
        }
        for(int j=0; j<nums.size(); j++){
            nums[j] /= 1001;
        }
        return nums;
    }
};
```
#### Remark:
- 5 + (7%10)*10 = 75
  - 75 % 10 = 5
  - 75 / 10 = 7
- 5: 原來位置的數，要被後來指針指的數蓋掉
- 7: 指針指的數，指針跑得比較慢，進去前要mod->multiply  
