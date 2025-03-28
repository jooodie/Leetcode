
# 1768. Merge Strings Alternately

## 📝 題目說明：
給定兩個字串 `word1` 和 `word2`，請交錯合併字母：
從 `word1` 開始，依序從兩個字串中交錯取出一個字元，
若其中一個字串較長，則將多餘的部分附加在最後。

範例：
- word1 = "abc"
- word2 = "pqr"
- 結果 = "apbqcr"

---

## 💡 我的 C 解法

```c
char * mergeAlternately(char * word1, char * word2){
    int len1 = strlen(word1);
    int len2 = strlen(word2);
    int totalLen = len1 + len2;

    char *result = (char *)malloc((totalLen + 1) * sizeof(char));

    int i = 0, j = 0, k = 0;
    while (i < len1 && j < len2) {
        result[k++] = word1[i++];
        result[k++] = word2[j++];
    }
    while (i < len1) {
        result[k++] = word1[i++];
    }
    while (j < len2) {
        result[k++] = word2[j++];
    }
    result[k] = '\0';
    return result;
}
```

---

## 🧠 解法說明：

- 使用 `strlen()` 取得兩字串長度
- 用 `malloc` 分配新字串記憶體
- 指標 `i`, `j`, `k` 控制 word1、word2、result 的位置
- 最後補上 `\0`，完成 C 字串結尾

---

## 🔍 學習心得：

這題練習了：
- malloc 的正確使用方式
- C 字串與 \0 的結尾概念
- while 迴圈邏輯與 post-increment 操作
- 解錯誤訊息、debug 能力

---

🎉 持續累積中 → Jodie's LeetCode 筆記日記 🧠
