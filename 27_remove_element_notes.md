# LeetCode 27: Remove Element — C 解題筆記

## 📘 題目描述（中文翻譯）

給你一個整數陣列 `nums` 和一個整數 `val`，請你「**就地移除所有等於 `val` 的元素**」，且不能使用新陣列（**in-place 操作**），然後回傳此時陣列中 **不等於 `val` 的元素個數** `k`。

- 要求把不等於 `val` 的值放到 `nums` 前 `k` 個位置
- 剩下的值可以不算，不影響答案
- 不可使用新陣列

---

## 🤔 你問我答 QA 筆記

### ☑️ 為什麼 `int k = 0;` 要一開始就設為 0？

因為 `k` 是用來表示「我已經放了幾個不等於 `val` 的值」，也是「我下一次要放值的位置」。

因此，一開始什麼都還沒放，得要從 0 開始算起，把第一個不等於 `val` 的值放在 `nums[0]`，所以 `k = 0` 是正確的設定。

---

### ☑️ 那麼「`k` 是 0 號位置不是真正值」是什麼意思？

好問！`k` 本身不是個值，它是一個 **操作的「位置指標」**：

- `k` 用來呈現：我已經放了幾個不等於 `val` 的值
- 或者說：`k` 是我 **下一次要放值的位置**

所以「`k = 0`」不是指值是 0，而是「我第一個要放的位置就是 index 0」

---

## ✨ 解題思路簡簡版

- 用 `i` 從頭到尾抓察陣列
- 每次看 `nums[i]`，如果 **不等於 `val`**，就放到 `nums[k]` 的位置，`k++`
- 最後就有 `k` 個值是有用的，前 `k` 個位置就是答案

---

## ✅ C 語言解法

```c
int removeElement(int* nums, int numsSize, int val) {
    int k = 0; // 下一個要放值的位置

    for (int i = 0; i < numsSize; i++) {
        if (nums[i] != val) {
            nums[k] = nums[i];
            k++;
        }
    }

    return k; // 回傳剩下的元素數
}
```

---

## 🧪 測試範例

```c
#include <stdio.h>

int removeElement(int* nums, int numsSize, int val);

int main() {
    int nums[] = {3, 2, 2, 3};
    int val = 3;
    int size = sizeof(nums) / sizeof(nums[0]);

    int k = removeElement(nums, size, val);

    printf("剩下的元素個數: %d\n", k);
    printf("nums 前 %d 個元素是: ", k);
    for (int i = 0; i < k; i++) {
        printf("%d ", nums[i]);
    }

    return 0;
}
```

✅ 執行結果：
```
剩下的元素個數: 2
nums 前 2 個元素是: 2 2
```

---

## 🔗 小技巧：計算陣列長度

### 使用 `sizeof` 計算陣列長度：

```c
int size = sizeof(nums) / sizeof(nums[0]);
```
這句的意思是：
> 用「陣列的總大小」除以「一個元素大小」得到陣列長度（有幾個元素）

📌 注意：這只能用在本地定義的陣列，不能用在函式參數 `int* nums` 裡！

---

加油茱蒂💪～你每次問的問題都很有想法，清楚釐清基礎真的會讓你未來寫更進階題目時更穩！繼續保持這個節奏，慢慢累積你自己的 LeetCode 筆記王國吧 🏰✨
