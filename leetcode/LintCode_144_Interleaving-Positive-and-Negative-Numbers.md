### Interleaving Positive and Negative Numbers
https://www.lintcode.com/problem/144/
>Given an array with positive and negative integers. Re-range it to interleaving with positive and negative integers.
```cpp
class Solution {
public:
    /**
     * @param a: An integer array.
     * @return: nothing
     */
    int partition(vector<int> &a) {
        int left=0, right=a.size()-1;
        while (left <= right){
            while ((left <= right) && (a[left] < 0)){
                left++;
            }
            while ((left <= right) && (a[right] >= 0)){
                right--;
            }
            if (left <= right){
                swap(a[left], a[right]);
                left++; right--;
            }
        }
        return left;
    }

    void swapper(int start, int end, vector<int> &a){
        while (start < end){
            swap(a[start], a[end]);
            start+=2; end-=2;
        }
    }

    void rerange(vector<int> &a) {
        int neg_count = partition(a);
        int pos_count = a.size() - neg_count;
        int l=0, r=a.size()-1;
        if (neg_count < pos_count){
            l++;
        } else if (pos_count > neg_count){
            r--;
        } else {
            l++; r--;
        }
        swapper(l, r, a);
    }
};
```
#### Remark:
- `std::swap(a, b)`

#### Complexity:
- Time: O(n) partition; O(n) interleave -> O(n)
- Space: O(1)
