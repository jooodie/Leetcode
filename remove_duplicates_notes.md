
# 📘 LeetCode 26 — Remove Duplicates from Sorted Array
**從排序陣列中移除重複項目（C 語言筆記版）**

---

## 📝 題目說明 | Problem Description （中英對照）

> Given an integer array `nums` **sorted in non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once.  
> Return `k` — the number of unique elements in `nums`, and make sure that the first `k` elements of `nums` contain the unique elements **in the same order**.

> 給定一個已**按照非遞減順序排序**的整數陣列 `nums`，請你**就地（in-place）移除重複的項目**，使每個唯一元素只出現一次。  
> 最後回傳唯一元素的個數 `k`，並確保 `nums` 的前 `k` 個元素是這些不重複的值（順序不變）。

---

## ✅ 解題邏輯整理（雙指標 Two Pointers）

- 使用兩個變數：
  - `i`：目前「**結果陣列最後一個唯一值的位置**」
  - `j`：從頭往後走，掃描整個陣列
- 當 `nums[j] != nums[i]` 時，就發現了新值，移到 `i+1` 的位置

---

## ❓ Jodie 提出的關鍵問題與解答 ✨

### Q1:
> “結果陣列最後一個唯一元素的位置” 是什麼意思？

✅ 解釋：這指的是「目前不重複的那些數字，**最後一個被存放的位置**」，也就是我們接下來要寫入下一個唯一數字的位置 - `i + 1`。

---

### Q2:
> 為什麼 `j` 要從 1 開始？

✅ 解釋：因為陣列的第 0 個數字一定是唯一的，**我們預設保留它**。所以比較應該從 `j = 1`（第二個元素）開始。

---

### Q3:
> 為什麼要 `return i + 1`？

✅ 解釋：`i` 是最後一個唯一值的 index，而陣列從 index 0 開始。  
所以總共的唯一元素個數就是 `i + 1`。

---

### Q4:
> 如果陣列只有一個數字怎麼辦？

✅ 解釋：完美可以處理！因為 `j = 1` 會直接跳過 for 迴圈，  
只留下 `nums[0]`，而 `i = 0`，回傳 `i + 1 = 1`，就是正確的唯一值個數。

---

## ✅ C 語言正確寫法：

```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize == 0) return 0;

    int i = 0;

    for (int j = 1; j < numsSize; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }

    return i + 1;
}
```

---

## 🧪 範例輸入與輸出：

```c
nums = [1, 1, 2, 3, 3];
// → 處理後 nums = [1, 2, 3, _, _]
// → 回傳值 = 3（唯一值個數）
```

---

## 🎯 邊界條件思考：

| 測資         | 輸出 | 說明             |
|--------------|------|------------------|
| `[]`         | `0`  | 空陣列           |
| `[42]`       | `1`  | 只有一個元素     |
| `[1,1,1]`     | `1`  | 全部都一樣       |
| `[1,2,3]`     | `3`  | 全部都不一樣     |
