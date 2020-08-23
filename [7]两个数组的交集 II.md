# ([8.23]两个数组的交集 II)[https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/submissions/]
给定两个数组，编写一个函数来计算它们的交集。

```
示例 1：

输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```
```
示例 2:

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

## 哈希表法
```
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        if(nums1.size()>nums2.size()){
            return intersect(nums2,nums1);
        }
        unordered_map<int,int> m;
        for(auto n: nums1){
            ++m[n];
        }
        int k = 0;
        for(auto  n: nums2)
        {
            auto it= m.find(n);
            if( it != end(m) && --it->second >=0 )
            {
                nums1[k++]=n;
            }
        }
        return vector(begin(nums1),begin(nums1)+k);

    }
};
```

## 双指针判断
```
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(),nums1.end());
        sort(nums2.begin(),nums2.end());
        int length1= nums1.size();
        int length2  = nums2.size();
        vector<int> intersection;
        int index1 = 0, index2 = 0;
        while(index1<length1 && index2 < length2)
        {
            if ( nums1[index1]< nums2[index2])
            {
                index1++;
            }
            else if (nums1[index1]> nums2[index2])
            {
                index2++;
            }
            else{
                intersection.push_back(nums1[index1]);
                index1++;
                index2++;
            }
        }
        return intersection;

        

    }
};
```
