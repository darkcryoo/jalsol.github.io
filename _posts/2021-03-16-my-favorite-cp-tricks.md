---
layout: post
title:  "[Updating] My favorite competitive programming tricks"
date:   2021-03-16 13:16:30 +0700
categories: programming cpp cp
---

I would like to talk a bit about my favorite competitive programming tricks (and, maybe, the story behind them).<br/>
I'm using C++17 (64-bit), but these should work with C++11 and above.

## Alternative operator representations

I'm quoting this from [cppreference.com](https://en.cppreference.com/w/cpp/language/operator_alternative):

```
C++ (and C) source code may be written in any non-ASCII 7-bit character set that includes
the ISO 646:1983 invariant character set. However, several C++ operators and punctuators
require characters that are outside of the ISO 646 codeset: {, }, [, ], #, \, ^, |, ~.
To be able to use character encodings where some or all of these symbols do not exist
(such as the German DIN 66003),C++ defines the following alternatives composed of ISO 646 compatible characters.
```

Basically, the reason C++ has keywords like `and`, `or`, `compl`, etc is because some keyboards didn't have the characters `&`, `|`, `~` etc.<br/>
I like using these more. Despite requiring more keystrokes, these keywords can be typed using actual letters, without holding the Shift keys.
They are also closer to the homerow, and it makes the codes look more like actual phrases and sentences (eg. `not empty(c)` vs `(!empty(c)))`.
Most developers don't actually like it though, which is why I don't use it for actual development work. This is exclusively for competitive programming.

## constexpr

`constexpr` is guaranteed to be assigned at compile time, while `const` doesn't necessarily have to. Also, some functions like `static_assert()` only
accept `constexpr` values.

## auto

Compare this:
```cpp
vector<int>::iterator it = a.begin();
```
to this:
```cpp
auto it = a.begin();
```

Isn't this great and magical? `auto` can guess the declared type of a variable, so you don't have to. However, it has side effects, so use them wisely.

## Structured bindings

This feature is officially available on C++17, but you can use this on C++11 and 14. Sure, you'll get a warning, but it will still work.<br/>

Instead of:
```cpp
tuple<int, int, int, int> a;
int x = get<0>(a);
int y = get<1>(a);
int z = get<2>(a);
int t = get<3>(a);
```
you can do this:
```cpp
tuple<int, int, int, int> a;
auto [x, y, z, t] = a;
```

You can also use the `const` keyword, or get the elements as references with `&`.
```cpp
tuple<int, int, int, int> a;
const auto &[x, y, z, t] = a;
```

## Range-based for-loops

There is the normal incremental for-loop, there is the iterator-based for-loops. But, the most intuitive of them all is range-based for-loops.
```cpp
vector<int> a {1, 2, 3, 4, 5};
for (int x : a) {
    cout << x << ' '; // prints "1 2 3 4 5 "
}
```
This is very convenient. One don't have to deal with indices and iterators, just straight up plug a (few) variable(s) and it works. You can combine this
with the `auto` keyword and structured bindings.
```cpp
vector<tuple<int, int, int>> a;
for (const auto &[x, y, z] : a) {
    // do something
}
```

## emplace()/emplace\_back()

This is a rather widely known *tricks* (it's not really a trick, but it seems that there are some people who are still not aware of it).<br/>
Many people still use `push()` and `push_back()` to add an element to a container. However, there is a major difference between `push()/push_back()`
and `emplace()/emplace_back()`.

`push()/push_back()` requires an object as the parameter, ie. if it's a container of `pair`, you need to pass a `pair`;
if it's a container of `tuple`, you need to pass a `tuple`, etc. If you already have an object ready to be passed, then that's fine. If not, you
will have to create one. After that, the container will create a new object within itself, and copy the passed object to the newly created object.
So, you need to create 2 objects, instead of 1. If the object takes time and memory to construct, that's a waste of efficiency.

`emplace()/emplace_back()`, however, requires **members** of an object as the parameters, not the whole object. If it's a container of `pair<int, int>`,
you only need to pass 2 `int`'s, instead of a `pair`. You don't have to construct a new `pair`. The `int`'s will be referenced. 'The container will still
create a new object within itself, but it will take the passed parameters as the constructor parameters. In the end, you only need to create 1 object only,
which is the one inside the container. This is a lot faster, compared to `push()/push_back()`.

However, for simpler types like `int` or `long long`, it's actually faster to create another copy, than to reference them. That's why I simply choose
`push()/push_back()` for these types.

## fill()/fill\_n()

Many people use `memset()`. It is indeed fast, but it can't fill an array with an arbitrary value, nor fill a certain range of the array.
The better alternatives are `fill()/fill_n()`. They can be a bit slow, but they can fix the aforementioned problems. Also, if necessary, it will call
`memset` in the background to save some speed.

**[To be continued]**
