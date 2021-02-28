---
title: ''
---

<div align=center>
	<img src="https://cdn.jsdelivr.net/gh/singularTnT/Image-Host/Blogger/assets/leetcode_log.png" width="100%">
</div>

</br>
<!-- more -->

## Description:

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

Example 2:
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

Example 3:
```
Input: nums = [3,3], target = 6
Output: [0,1]
```

## Solution:

#### Solution 1:
Use STL:

|  Time  |  Space  |
|  :--:  |  :---:  |
|  O(n)  |  O(n)   |

```c++
class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
        std::vector<int> res; // return result.
        std::unordered_map<int, int> hash; // key is the num, value is the index.
        
        int i = 0; // record index.
        for (auto &num : nums) {
            int tar_num = target - num; // target number to find.
            // if find, return.
            if (hash.find(tar_num) != hash.end()) {
                res.push_back(i);
                res.push_back(hash[tar_num]);
                
                return res;
            }
            
            // else insert to map #hash.
            hash[num] = i;
            i++;
        }
        
        return res;
    }
};
```

#### Solution 2:
Use Boost (more elegant, unfortunately, leetcode not support Boost):

|  Time  |  Space  |
|  :--:  |  :---:  |
|  O(n)  |  O(n)   |

```c++
class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
		std::vector<int> res; // return result.
		std::unordered_map<int, int> hash; // key is the num, value is the index.

		// use boost/range/adaptors
		for (auto num : nums | boost::adaptors::indexed(0)) {
			int tar_num = target - num.value(); // target number to find.
			// if find, return.
			if (hash.find(tar_num) != hash.end()) {
				res.push_back(num.index());
				res.push_back(hash[tar_num]);

				return res;
			}

			// else insert to map #hash.
			hash[num.value()] = num.index();
		}

		return res;
	}
};
```

<!-- require APlayer -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer/dist/APlayer.min.js"></script>
<!-- require MetingJS -->
<script src="https://cdn.jsdelivr.net/npm/meting@2/dist/Meting.min.js"></script>