---
title: c++ Classes, New features on classes since c++11
date: 2021-04-10
tags:
  - c++
keywords:
  - c++
  - class
  - new feature since c++11
---

## {} 괄호를 이용한 초기화 가능

```cpp
class Array {
    int myData[5];
public:
    Array()
    :myData{1,2,3,4,5} {};   //{} 괄호를 이용해 myData 초기화
};

class MyClass {
public:
    int x;
    double y;
};

class MyClass2 {
    int x;
    double y;
public:
    MyClass2(int first, double second)
    :x{first}, y{second}{};
}

int main(){
    Array arr;

    // public attributes를 사용한 초기화
    MyClass myClass1{2021, 4.10};
    MyClass myClass2 = {2021, 4.10};

    // constructor를 사용한 초기화 <-- 생성자 추천!!
    MyClass2 myClass3{2021, 4.10};
    MyClass2 myClass4 = {2021, 4.10};
}

```

## 클래스 멤버 초기화 가능

```cpp
class C{
    int x;
public:
    C()
    :x(7){}
};
```

```cpp
class C{
    int x=7;  // class member (직접) 초기화
public:
    C();
};
```

### 사용가능한 표현

- =(equal sign)

- 괄호(){}

  ```cpp
  class C {
      double d=0;
      string s("abc");
      char * p {nullptr};
      int y[5] {1,2,3,4};
  public:
      C();
  };
  ```

  ```cpp
  class C {
      double d;
      string s;
      char * p;
      int y[5];
  public:
      C()
      : d(0.0), s("abc"), p(nullptr), y{1,2,3,4}{}
  };
  ```
