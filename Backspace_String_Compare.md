
# 📄 題目名稱：Backspace String Compare  
**（字串比對：模擬退格符號 `#`）**

---

## 題目描述
Given to strings S and T, containing only latin letters in the lower registry and ‘#’ symbols. You need to implement a function that will treat '#'s as a backspace (the precending to it symbol will be erased) and compare two strings and return true if those are equal and false if not..
給定兩個字串 `S` 和 `T`，它們只包含小寫英文字母與 `#` 符號。請實作函式 `issame`，將 `#` 視為退格鍵（即刪除其前一個字元），並回傳兩個字串經過退格處理後是否相等。

---

## 函式簽名

```cpp
bool issame(const std::string& S, const std::string& T);
```

---

## 範例

### Example 1

```
Input:  S = "ab#c", T = "ad#c"
Output: true

S 會變成 "ac"（b 被 # 刪掉）  
T 也會變成 "ac"（d 被 # 刪掉）
```

### Example 2

```
Input:  S = "a##c", T = "#a#c"
Output: true

S 處理後為 "c"  
T 處理後也為 "c"
```

### Example 3

```
Input:  S = "a#c", T = "b"
Output: false

S → "c"  
T → "b"  
不相等
```

### Example 4

```
Input:  S = "##abcd####ab", T = "abcd##ab#c##"
Output: true

兩邊經過處理後都會變成 "ab"
```

---

## 解題思路

- 定義一個 `process` 函式來模擬退格操作
- 建立一個 `result` 字串作為模擬鍵盤輸入的結果
  - 如果遇到一般字母就用 `push_back()` 加進去
  - 如果遇到 `#`，就用 `pop_back()` 刪掉最後一個字元
- 對 `S` 和 `T` 分別進行處理，最後比對處理結果是否一致

---

## 程式碼解法

```cpp
#include <string>

std::string process(const std::string& str) {
    std::string result;
    for (char ch : str) {
        if (ch == '#') {
            if (!result.empty()) {
                result.pop_back();
            }
        } else {
            result.push_back(ch);
        }
    }
    return result;
}

bool issame(const std::string& S, const std::string& T) {
    return process(S) == process(T);
}
```

---

## 🧩 拆解說明：
- bool →	函式會回傳布林值（true 或 false）
- issame →	函式名稱，意思是「是否相同」

- std::string → 這是 C++ 標準字串型別，代表一個字串
  例如 "hello" 就是 std::string
- **&** 是什麼？ → 引用（reference）
  意思是：不是把整個字串複製進來，而是用「原本變數」的參考（指向）來處理，這樣做可以提升效率（不用複製一整串字元）
- "const std::string& S" 我接收一個「只讀的字串參考」，名字叫做 S

- const std::string& S →	傳入參數：字串 S，用參考傳遞，而且不會被修改
- const std::string& T →	傳入參數：字串 T，同樣是常數參考



---

## 時間與空間複雜度

- 時間複雜度：O(n + m)，其中 `n` 與 `m` 是 `S` 和 `T` 的長度
- 空間複雜度：O(n + m)，額外空間用於儲存處理後的字串結果

- 有 2 個字串	👉 分別長度為 n 和 m
- 每個字串都跑一次	👉 時間複雜度 O(n + m)
- 為每個字串產生處理結果	👉 空間複雜度 O(n + m)

---

## 🤔 我的提問與思考紀錄

- `for (char ch : str)`→  C++範圍式 for 迴圈，會逐字讀取 `str` 中的每一個字元，並將其存入變數 `ch`
- `pop_back()`→   C++語法，它會把最後一個字元移除
- `push_back(ch)` →  C++語法， 把 `ch` 放到最後
- 處理字串時為什麼要先檢查 `empty()`？→ 避免在空字串上 `pop_back()` 導致錯誤
- 可以怎麼判斷處理完後的兩字串是否相等？→ 呼叫issame function, `process(S) == process(T)`
