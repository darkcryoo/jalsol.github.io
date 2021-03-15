---
layout: post
title:  "[Vietnamese] C++ Vector"
date:   2021-03-15 15:40:51 +0700
categories: programming cpp
---

C++ là một ngôn ngữ có rất nhiều data structures mạnh mẽ, hữu ích cho competitive programming. Tuy nhiên, có một hiện tượng là các em dường như chưa nắm rõ được bản chất, cũng như cách dùng.

Có rất nhiều blog trên mạng về các loại data structures này rồi, search là ra một rổ. Cơ mà vì muốn quảng bá blog (hihi) nên anh cũng rảnh háng ngồi viết bài chơi.
**Lưu ý: anh sẽ bỏ qua một số kiến thức phức tạp như iterator, cấu trúc data bên trong các data structures, capacity,...** Đứa nào muốn tìm hiểu thêm thì có thể alo anh hoặc giải KK VOI 2021, dlbm1302.

Bài viết đầu tiên trong series sẽ là về **vector**, một data structure cơ bản và rất thường dùng trong C++, cũng như competitive programming.

## Vector
Vector là dynamic array (mảng động). Còn vì sao nó lại gọi là **vector** mà không phải là **dynamic_array** hay **darray** hay cái gì đó thì đi hỏi bác Stroustrup :D

Cú pháp khai báo vector là:
```cpp
vector<T> name;
```
Trong đó, `T` là tên kiểu dữ liệu mà nó chứa (int, long long, pair,...), và `name` là tên của vector.<br/>
VD:
```cpp
vector<int> vi;
vector<long long> vll;
vector<pair<int, int>> vpii;
vector<vector<int>> vvi;
```

# Gán giá trị, kích cỡ
Mặc định, vector sẽ chẳng có phần tử nào cả.
```cpp
vector<int> a; // a = {}
```

Vậy, nếu ta muốn khai báo vector có `n` phần tử thì làm như nào?
```cpp
vector<int> a(n); // a = {0, 0, ..., 0}
```

Lúc này, vector sẽ có `n` phần tử. **Tất cả các phần tử mặc định đều sẽ mang giá trị 0**.<br/>
Thế còn, nếu ta muốn khai báo một vector có `n` số `5` thì làm sao?
```cpp
vector<int> a(n, 5); // a = {5, 5, ..., 5}
```

Ngoài ra, nếu muốn gán vector này bằng dấu `=`, ta có thể làm như sau:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
```

Trong quá trình sử dụng, ta muốn "reset" vector về lại giá trị nào đó (như `memset`, ta không dùng được `memset` với vector), ta có thể làm như sau với `assign`:
```cpp
vector<int> a; // khai báo trước đó
a.assign(n, 5); // a = {5, 5, ..., 5}
```

Ta còn có thể sử dụng lệnh `resize` để đổi lại kích cỡ của vector:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
a.resize(3); // a = {1, 2, 3}
```

**Lưu ý:** `resize` **và** `assign` **chỉ khác nhau ở chỗ:** `resize` **không gán lại giá trị,** `assign` **thì có.**

# Truy cập phần tử
Ta hoàn toàn có thể truy cập phần tử của vector như mảng bình thường:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
cout << a[3] << endl; // in ra 4
```

Ngoài ra, ta có thể sử dụng `at()` (cơ mà anh chẳng thấy ai dùng cả .\_.)
```cpp
vector<int> a = {1, 2, 3, 4, 5};
cout << a.at(3) << endl; // in ra 4
```

**Lưu ý: vector (cũng giống mảng) bắt đầu đánh số chỉ số từ 0.**

Ta có thể lấy phần tử đầu tiên và cuối cùng của vector bằng `front()` và `back()`:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
cout << a.front() << ' ' << a.back() << endl; // in ra "1 5"
```

# Con trỏ
Sơ qua thì chúng ta có `begin()`, `end()`, `rbegin()`, `rend()`,...<br/>
Bản thân con trỏ là một topic khó, anh sẽ bỏ qua. Anh sẽ cân nhắc update bổ sung nếu cần thiết.

# Kích cỡ
Function `empty()` sẽ cho ta biết vector có rỗng hay không:
```cpp
vector<int> a;
cout << a.empty() << endl; // in ra 1, tức là true
a.resize(69420);
cout << a.empty() << endl; // in ra 0, tức là false
```

Function `size()` sẽ cho ta biết kích cỡ của vector:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
cout << a.size() << endl; // in ra 5
```

Ngoài ra, còn một số khái niệm về capacity, anh sẽ bỏ qua.

# Chỉnh sửa
Để **thêm** vào **đằng sau** của vector, ta dùng `push_back()`:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
a.push_back(27022004); // a = {1, 2, 3, 4, 5, 27022004} ;)
```

Ngoài ra, ta còn lệnh `emplace_back()`. Có thể anh sẽ viết riêng một blog ngắn về lệnh này. Tạm thời `push_back()` là ổn rồi.

Để **bỏ** phần tử **đằng sau** của vector, ta dùng `pop_back()`:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
a.pop_back(); // a = {1, 2, 3, 4}
```

Để xóa toàn bộ vector, ta dùng `clear()`:
```cpp
vector<int> a = {1, 2, 3, 4, 5};
a.clear(); // a = {}
```

Để đổi giá trị 2 vector cho nhau, ta có thể dùng `swap()`:
```cpp
vector<int> a = {1, 2, 3};
vector<int> b = {4, 5, 6};

// 1 trong 2 cách đều cho kết quả giống nhau, nhưng cách 2 nhanh hơn cách 1
swap(a, b);
a.swap(b);
```

Các lệnh như `insert()`, `erase()`,... có liên quan tới **con trỏ**. Anh sẽ cân nhắc update bổ sung nếu cần thiết.

## Nguồn
* [cppreference.com](https://en.cppreference.com/w/cpp/container/vector)
* [cplusplus.com](https://www.cplusplus.com/reference/vector/vector/)
