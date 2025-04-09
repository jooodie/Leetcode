# LeetCode 169. Majority Element

## 📝 Description
Given an array `nums` of size `n`, return the majority element.  
The majority element is the element that appears more than `⌊n / 2⌋` times.  
You may assume that the majority element always exists in the array.

---

## 📌 Examples

### Example 1
```
Input: nums = [3,2,3]  
Output: 3
```

### Example 2
```
Input: nums = [2,2,1,1,1,2,2]  
Output: 2
```

---

## ✅ Solution 1: Boyer-Moore Voting Algorithm (O(n) Time, O(1) Space)

### 💡 Idea

Use a voting strategy to cancel out non-majority elements:

1. Set `candidate` as the current majority candidate, and `count` as the vote count.
2. Traverse the array:
   - If `count == 0`, set `candidate` to the current number.
   - If current number equals `candidate`, increase `count`.
   - Otherwise, decrease `count`.
3. Since a majority element always exists, the final `candidate` is the answer.
   
用固定大小陣列模擬計數器（因為題目說 -10^9 <= nums[i] <= 10^9）
這範圍太大，不適合開 count[nums[i]] 陣列。
所以我們改用 經典的 Boyer-Moore 投票法，C語言寫法更簡潔，也不需要開 hash map！

### 🔧 C Implementation

```c
int majorityElement(int* nums, int numsSize) {
    int count = 0;
    int candidate = 0;

    for (int i = 0; i < numsSize; i++) {
        if (count == 0) { //新候選人
            candidate = nums[i];
        }
        if (nums[i] == candidate) {
            count++; //候選人票數加一
        } else {
            count--; //非當前候選人得票，票數抵銷aka扣一
        }
    }

    return candidate; //最後給出最終候選人
}
```

---

## 📚 Notes

- This solution leverages the fact that the majority element appears more than all other elements combined.
- Even with interference from other elements, the majority one will remain after all cancellations.

## 🧠 解釋一下邏輯：
向選舉一樣，每次遇到跟 candidate 一樣的數，就 count++
遇到不同的，就 count--
如果 count == 0，我們就換一個 candidate
因為題目保證「多數元素一定存在」，所以最後留下的 candidate 一定是答案

---

## ✅ Complexity

- **Time:** O(n) — One pass through the array.
- **Space:** O(1) — Uses only two variables.
