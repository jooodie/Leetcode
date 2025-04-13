## LeetCode 189. Rotate Array

### Problem Description (English)

> Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

#### Constraints:
- `1 <= nums.length <= 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`
- `0 <= k <= 10^5`

---

### Example

```c
Input:  nums = [1, 2, 3, 4, 5, 6, 7], k = 3
Output: [5, 6, 7, 1, 2, 3, 4]
```

---

#### Follow up:
- Try to come up with as many solutions as you can. There are at least **three different ways** to solve this problem.
- Could you do it **in-place** with **O(1) extra space**?

---

### Idea: Reverse Method (三段反轉法)

To rotate the array to the right by `k` steps:

1. Reverse the entire array  
2. Reverse the first `k` elements  
3. Reverse the remaining `n - k` elements

This effectively puts every element in its correct rotated position.

- **Time complexity:** O(n)  
- **Space complexity:** O(1) (in-place)

---

### C Code with Clear Comments

```c
// Reverse a portion of the array
void reverse(int* nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}

void rotate(int* nums, int numsSize, int k){
    k = k % numsSize;  // 避免 k 大於陣列長度

    reverse(nums, 0, numsSize - 1);     // 把整個陣列反轉
    reverse(nums, 0, k - 1);            // 把前 k 個反轉（讓它們回到正確順序）
    reverse(nums, k, numsSize - 1);     // 把後面 n-k 個反轉
}
```

---

### Example

```c
Input:  nums = [1, 2, 3, 4, 5, 6, 7], k = 3
Output: [5, 6, 7, 1, 2, 3, 4]
```

---

🧩 小提醒：
一定要記得 k = k % numsSize;
不然如果 k > numsSize，會出錯！

---

#### Follow up:
- Try to come up with as many solutions as you can. There are at least **three different ways** to solve this problem.
- Could you do it **in-place** with **O(1) extra space**?

---
