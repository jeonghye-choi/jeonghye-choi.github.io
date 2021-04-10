---
title: c++ Classes, Nested Classes
date: 2021-04-10
tags:
  - c++
keywords:
  - c++
  - class
  - nested classes
---

클래스 내부에 클래스 정의

## Example

가능은 하지만, 이럴 필요가 없으면 Point를 nested class로 하지 않는 것이 좋다!

```cpp
class Rectangle {
public:
    class Point {
    public:
        int x, y;
        void print()const{ cout << x << "\t" << y; }
        bool isEqual(const Point& p)const{ return x==p.x && y==p.y; }
    };

    Point leftTop, rightBottom;
    void setLeftTop(int x, int y){
        leftTop.x = x;
        leftTop.y = y;
    }
    void setRightBototm(int x, int y){
        RightBototm.x = x;
        RightBototm.y = y;
    }
    bool isEqual(const Rectangle& r)const{
        return leftTop.isEqual(r.leftTop) && rightBottom.isEqual(r.rightBottom);
    }
    const Rectangle& print()const{
        leftTop.print();
        cout << "\t" << rightBottom.print();
        return *this;
    }
}
```

```cpp
//main.cpp
#include <iostream>
#include <string>
#include "Rectangle.h"
using namespace std;

int main(){
    Rectangle r1;
    r1.set(0,0,100,200);

    Rectangle r2;
    r2.set(10,10,110,210);

    r1.print(); cout << endl;
    r2.print(); cout << endl;

    string msg = r1.isEqual(r2) ? "SAME" : "DIFFERENT";
    cout << msg << endl;

    Rectangle::Point pt; // Rectangle 내부의 Point!
    //가능은 하지만, 이럴 필요가 없으면 Point를 nested class로 하지 않는 것이 좋다!
}
```
