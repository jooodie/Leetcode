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

### 🔧 C Implementation

```c
int majorityElement(int* nums, int numsSize) {
    int count = 0;
    int candidate = 0;

    for (int i = 0; i < numsSize; i++) {
        if (count == 0) {
            candidate = nums[i];
        }
        if (nums[i] == candidate) {
            count++;
        } else {
            count--;
        }
    }

    return candidate;
}
```

---

## 📚 Notes

- This solution leverages the fact that the majority element appears more than all other elements combined.
- Even with interference from other elements, the majority one will remain after all cancellations.

---

## ✅ Complexity

- **Time:** O(n) — One pass through the array.
- **Space:** O(1) — Uses only two variables.
