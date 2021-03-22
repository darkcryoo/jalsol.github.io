---
layout: post
title:  "[Vietnamese] C++ Vector"
date:   2021-03-15 15:40:51 +0700
categories: programming cpp
---

C++ là một ngôn ngữ có rất nhiều data structures mạnh mẽ, hữu ích cho competitive programming.

Có rất nhiều blog trên mạng về các loại data structures này rồi, search là ra một rổ. Cơ mà vì muốn quảng bá blog (hihi) nên tôi cũng rảnh háng ngồi viết bài chơi.
**Lưu ý: tôi sẽ bỏ qua một số kiến thức phức tạp như iterator, cấu trúc data bên trong các data structures, capacity,...**

Bài viết đầu tiên trong series sẽ là về **vector**, một data structure cơ bản và rất thường dùng trong C++, cũng như competitive programming.

# Vector
Vector là dynamic array (mảng động). Kích cỡ của vector có thể tùy biến thay đổi, thay vì cố định như mảng thường.
Còn vì sao nó lại gọi là **vector** mà không phải là **dynamic\_array** hay **darray** hay cái gì đó thì đi hỏi bác Stroustrup :D

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

## Gán giá trị, kích cỡ
**Mặc định, vector sẽ chẳng có phần tử nào cả.**
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

Hoặc, sử dụng `initializer_list`, ta cũng có thể gán giá trị cho vector như sau:
```cpp
vector<int> a {1, 2, 3, 4, 5}; // không cần dấu =
```

Trong quá trình sử dụng, ta muốn "reset" vector về lại giá trị nào đó (như `memset`, ta không dùng được `memset` với vector), ta có thể làm như sau với `assign`:
```cpp
vector<int> a; // khai báo trước đó
a.assign(n, 5); // a = {5, 5, ..., 5}
```

Ta còn có thể sử dụng lệnh `resize` để đổi lại kích cỡ của vector:
```cpp
vector<int> a {1, 2, 3, 4, 5};
a.resize(3); // a = {1, 2, 3}
```

**Lưu ý:** `resize` **và** `assign` **chỉ khác nhau ở chỗ:** `resize` **không gán lại giá trị,** `assign` **thì có.**

## Truy cập phần tử
Ta hoàn toàn có thể truy cập phần tử của vector như mảng bình thường:
```cpp
vector<int> a {1, 2, 3, 4, 5};
cout << a[3] << endl; // in ra 4
```

Ngoài ra, ta có thể sử dụng `at()` (cơ mà anh chẳng thấy ai dùng cả .\_.)
```cpp
vector<int> a {1, 2, 3, 4, 5};
cout << a.at(3) << endl; // in ra 4
```

**Lưu ý: vector (cũng giống mảng) bắt đầu đánh số chỉ số từ 0.**

Ta có thể lấy phần tử đầu tiên và cuối cùng của vector bằng `front()` và `back()`:
```cpp
vector<int> a {1, 2, 3, 4, 5};
cout << a.front() << ' ' << a.back() << endl; // in ra "1 5"
```

## Con trỏ
Sơ qua thì chúng ta có `begin()`, `end()`, `rbegin()`, `rend()`,...<br/>
Bản thân con trỏ là một topic khó, ta sẽ bỏ qua. Sẽ cân nhắc update bổ sung nếu cần thiết.

## Kích cỡ
Function `empty()` sẽ cho ta biết vector có rỗng hay không:
```cpp
vector<int> a;
cout << a.empty() << endl; // in ra 1, tức là true
a.resize(69420);
cout << a.empty() << endl; // in ra 0, tức là false
```

Function `size()` sẽ cho ta biết kích cỡ của vector:
```cpp
vector<int> a {1, 2, 3, 4, 5};
cout << a.size() << endl; // in ra 5
```

Ngoài ra, còn một số khái niệm về capacity, ta sẽ bỏ qua.

## Chỉnh sửa
Để **thêm** vào **đằng sau** của vector, ta dùng `push_back()`:
```cpp
vector<int> a {1, 2, 3, 4, 5};
a.push_back(20032021); // a = {1, 2, 3, 4, 5, 20032021}
```

Ngoài ra, ta còn lệnh `emplace_back()`. Điểm lợi của `emplace_back()` được đề cập ở [đây](/programming/cpp/cp/2021/03/16/my-favorite-cp-tricks.html) (tiếng Anh).

Để **bỏ** phần tử **đằng sau** của vector, ta dùng `pop_back()`:
```cpp
vector<int> a {1, 2, 3, 4, 5};
a.pop_back(); // a = {1, 2, 3, 4}
```

Để xóa toàn bộ vector, ta dùng `clear()`:
```cpp
vector<int> a {1, 2, 3, 4, 5};
a.clear(); // a = {}
```

Để đổi giá trị 2 vector cho nhau, ta có thể dùng `swap()`:
```cpp
vector<int> a {1, 2, 3};
vector<int> b {4, 5, 6};

// 1 trong 2 cách đều cho kết quả giống nhau, nhưng cách 2 nhanh hơn cách 1
swap(a, b); // hoặc a.swap(b);
// a = {4, 5, 6}
// b = {1, 2, 3}
```

Các lệnh như `insert()`, `erase()`,... có liên quan tới **con trỏ**. Sẽ cân nhắc update bổ sung nếu cần thiết.

## Các lệnh hữu ích khác
(Cảm ơn idol ***[dlbm1302](https://www.facebook.com/dlbm.1302)*** đã góp ý)

Sắp xếp toàn bộ vector bằng `sort()`:
```cpp
vector<int> a {5, 4, 3, 2, 1};
sort(a.begin(), a.end()); // a = {1, 2, 3, 4, 5} : sort tăng dần
sort(a.rbegin(), a.rend()); // a = {5, 4, 3, 2, 1} : sort giảm dần
```

Đảo ngược toàn bộ vector bằng `reverse()`:
```cpp
vector<int> a {2, 7, 0, 2, 2, 0, 0, 4};
reverse(a.begin(), a.end()); // a = {4, 0, 0, 2, 2, 0, 7, 2}
```

Gán giá trị cho mảng bằng `fill() và fill_n()` (`fill() và fill_n()` là các lệnh tương tự `memset()`, nhưng mạnh mẽ hơn):
```cpp
int n = 6;
vector<int> a(n);
fill(a.begin(), a.end(), -1); // a = {-1, -1, -1, -1, -1, -1}
fill_n(a.begin(), 3, 20); // a = {20, 20, 20, -1, -1, -1}
```

Rải các phần tử bằng `iota()`:
```cpp
vector<int> a(5);
iota(a.begin(), a.end(), 7); // a = {7, 8, 9, 10, 11}
```

Tìm giá trị lớn nhất, nhỏ nhất ở trong vector:
```cpp
vector<int> a {2, 7, 0, 2, 2, 0, 0, 4};
cout << *max_element(a.begin(), a.end()) << endl; // in ra 7
cout << *min_element(a.begin(), a.end()) << endl; // in ra 0
```

Xóa các phần tử trùng lặp trong vector (có thể ứng dụng để nén sau này):
```cpp
vector<int> a {2, 7, 0, 2, 2, 0, 0, 4};
sort(a.begin(), a.end()); // bắt buộc
a.erase(unique(a.begin(), a.end()), a.end()); // a = {0, 2, 4, 7}
```

## Nguồn
* [cppreference.com](https://en.cppreference.com/w/cpp/container/vector)
* [cplusplus.com](https://www.cplusplus.com/reference/vector/vector)
