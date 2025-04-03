## LeetCode 80. Remove Duplicates from Sorted Array II  
**移除排序陣列中的重複項目 II**

---

### 📝 題目描述  
Given an integer array `nums` sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears **at most twice**.  
The relative order of the elements should be kept the same.  
Return the number of elements in the modified array.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with **O(1)** extra memory.

給定一個已按照非遞減順序排序的整數陣列 `nums`，你需要**就地刪除一些重複項**，使每個元素最多只出現兩次，並**保持原來的相對順序**。  
在不使用額外陣列的情況下，以 **O(1)** 的空間複雜度完成此操作。  
返回刪除後陣列的新長度 `k`，使得 `nums[0..k-1]` 包含正確的結果。

---

### 📚 範例  

#### Example 1:
```
Input:  nums = [1,1,1,2,2,3]
Output: 5, nums = [1,1,2,2,3,_]
```

#### Example 2:
```
Input:  nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3,_]
```

---

### ❓ 我的問題  

```c
int i = 2;  // i 是下一個要放的位置
for (int j = 2; j < numsSize; j++) {
    if (nums[j] != nums[i - 2]) {
        nums[i] = nums[j];
        i++;
```

🔸 這邊是判斷第三個元素（j=2）是不是 ≠ 第一個元素（i-2），對吧？  
🔸 因為只要倒數第二個跟當前值不一樣，就代表這個數字還沒出現超過兩次，可以保留！  
🔸 第二位數值（nums[1]）其實不需要特別管，因為陣列是排序好的～

✅ 沒錯！這樣理解完全正確 👍  
`nums[i - 2]` 就是結果陣列的倒數第二位，我們透過它來判斷目前這個數字是否已經出現過兩次了。

---

### ✅ C 語言解法（O(n) 時間，O(1) 空間）

```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize <= 2) return numsSize;  // 小於等於2個元素時直接返回原長度

    int i = 2;  // i 是下一個要寫入的位置，前兩個元素保留

    for (int j = 2; j < numsSize; j++) {
        // 只要當前元素和結果中倒數第二個不同，就保留
        if (nums[j] != nums[i - 2]) {
            nums[i] = nums[j];
            i++;
        }
    }

    return i;  // 回傳新的長度，表示前 i 個元素是正確結果
}
```

---

### 🔍 解題邏輯整理  

| 觀察重點 | 說明 |
|----------|------|
| 排序陣列 | 重複的元素一定會相鄰 |
| 前兩個值 | 不管怎樣都可以保留 |
| 判斷條件 | 若 `nums[j] != nums[i - 2]`，代表還沒超過兩次，就可以放 |
| 為何用 i-2 | 倒數第二位用來確認某個值是否已經出現兩次了 |

---

### 📌 小結  

- **這題的精髓**就是利用 `nums[i - 2]` 做「次數控制」的判斷
- **排序陣列的特性**讓我們可以這樣直接判斷
- **不能用額外空間**，因此只能用雙指標就地處理
