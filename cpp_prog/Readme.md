# Modern C++ (C++11/14) — Quick Reference

Modern C++ (C++11 and C++14) introduced many features that simplify coding, improve safety, enhance performance, and enable more expressive code. This document summarizes key language improvements with brief explanations and examples.

---

## 1️⃣ Language Improvements

### General Features

#### `constexpr`

* Allows functions and variables to be evaluated at compile time.

```cpp
constexpr int square(int x) { return x * x; }
```

#### `auto` Type Deduction

* The compiler automatically deduces the variable type.

```cpp
auto x = 42; // int
auto name = "Hafiz"; // const char*
```

#### `decltype`

* Deduce the type of an expression.

```cpp
int a = 5;
decltype(a) b = 10; // b is int
```

#### Range-based `for` Loop

* Simplifies iteration over containers.

```cpp
for (auto& num : numbers) {
    std::cout << num << std::endl;
}
```

#### `static_assert`

* Compile-time assertion for constant expressions.

```cpp
static_assert(sizeof(int) == 4, "int size is not 4 bytes");
```

#### `nullptr`

* A type-safe null pointer literal.

```cpp
int* ptr = nullptr;
```

#### Scoped / Strongly-Typed Enums (`enum class`)

* Avoids name clashes; safer than old enums.

```cpp
enum class Color { Red, Green, Blue };
Color c = Color::Red;
```

#### Uniform Initialization (`{}`)

* Consistent initialization syntax for variables, structs, classes.

```cpp
int arr[3] {1, 2, 3};
std::vector<int> v {1, 2, 3, 4};
```

#### `using` Keyword for Type Aliasing

* Cleaner alternative to `typedef`.

```cpp
using IntVec = std::vector<int>;
```

#### User-Defined Literals

* Define custom literal suffixes.

```cpp
constexpr long double operator"" _cm(long double val) { return val / 100; }
auto length = 50.0_cm;
```

#### Binary Literals (`0b`)

* Binary representation of numbers.

```cpp
int mask = 0b10101010;
```

#### Digit Separators (`'`)

* Improve readability of large numbers.

```cpp
int big = 1'000'000;
```

#### Raw String Literals (`R"(...)"`)

* Avoid escaping in strings.

```cpp
std::string path = R"(C:\Program Files\MyApp)";
```

---

## 2️⃣ Class & Object Improvements

#### Defaulted and Deleted Special Member Functions

* Request compiler-generated default or forbid certain operations.

```cpp
class MyClass {
public:
    MyClass() = default;
    MyClass(const MyClass&) = delete;  // No copy constructor
};
```

#### Delegating Constructors

* One constructor calls another within the same class.

```cpp
class MyClass {
public:
    MyClass(int x) { /*...*/ }
    MyClass() : MyClass(0) { }
};
```

#### In-Class Member Initializers

* Initialize member variables directly in class definition.

```cpp
class MyClass {
    int count = 0;
};
```

#### Uniform Initialization

* See earlier uniform `{}` initialization example.

#### `std::initializer_list`

* Allows initializer-list constructors.

```cpp
class MyClass {
public:
    MyClass(std::initializer_list<int> vals) { /*...*/ }
};
MyClass obj {1, 2, 3, 4};
```

#### Explicit Conversion Operators

* Prevent implicit conversions.

```cpp
class MyClass {
public:
    explicit operator bool() const { return true; }
};
```

#### Read-Only Objects (`const` Member Functions)

* Prevent modification of object state.

```cpp
class MyClass {
    int value;
public:
    int get() const { return value; }
};
```

#### Explicit Type Conversion

* Require explicit casting when converting.

```cpp
explicit MyClass(int val) { /*...*/ }
```

#### Type Traits (`<type_traits>`)

* Metaprogramming utilities for type introspection.

```cpp
static_assert(std::is_integral<int>::value, "int is not integral");
```

---

## 3️⃣ Inheritance Improvements

#### `final` and `override` Keywords

* Ensure correct overriding; prevent further overriding.

```cpp
class Base {
public:
    virtual void foo() final;
    virtual void bar() {}
};

class Derived : public Base {
public:
    void bar() override { /* correct override */ }
};
```

#### Inheriting Base Class Constructors

* Simplify constructor inheritance.

```cpp
class Base {
public:
    Base(int) { }
};

class Derived : public Base {
    using Base::Base;
};
```

---

## 4️⃣ Move Semantics

#### Move Constructor & Move Assignment Operator

* Efficient resource transfer, avoid unnecessary copies.

```cpp
class MyClass {
public:
    MyClass(MyClass&& other) noexcept { /* move resources */ }
    MyClass& operator=(MyClass&& other) noexcept { /* move assign */ return *this; }
};
```

#### `std::move()`

* Cast object to rvalue reference to enable move semantics.

```cpp
MyClass obj1;
MyClass obj2 = std::move(obj1);  // obj1 moved
```

---

# Summary Table

| Feature                     | Purpose                       |
| --------------------------- | ----------------------------- |
| `auto` / `decltype`         | Type deduction                |
| `constexpr`                 | Compile-time evaluation       |
| `nullptr`                   | Safer null pointers           |
| `enum class`                | Scoped enums                  |
| `using`                     | Type alias                    |
| Uniform Initialization `{}` | Unified initialization syntax |
| `static_assert`             | Compile-time assertions       |
| Move Semantics              | Efficient resource handling   |
| `override` / `final`        | Safer inheritance             |
| `std::initializer_list`     | List initialization support   |

---
