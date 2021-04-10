---
title: c++ Classes, 객체 데이터 멤버
date: 2021-04-09
tags:
  - c++
keywords:
  - c++
  - class
  - 객체 데이터 멤버
  - const member function
---

## const member function

```cpp
// Rectangle.h
#ifndef Rectangle_h
#define Rectangle_h

class Rectangle {
    int leftTopX, leftTopY;
    int rightBottomX, rightBottomY;
    void setLeftTop(int x, int y){  // 데이터 멤버 수정함 -> const사용불가!
        leftTopX = x;
        leftTopY = y;
    }
    void setRightBottom(int x, int y){
        rightBottomX = x;
        rightBottomY = y;
    }
public:
    static int allCount;  // 명시만

    Rectangle() { allCount++; }
    ~Rectangle() { allCount--; }

    static int getAllCount() { return allCount; }   // not const
    static bool noRectangle() { return allCount == 0; }

    void set(int x1, int y1, int x2, int y2){
        setLeftTop(x1, y1);
        setRightBottom(x2, y2);
    }
    void getLeftTop(int& x, int& y)const{  //const: 자신의 데이터멤버의 값을 변경하지 않고 읽기만 한다고 명시.
        x = leftTopX;
        y = leftTopY;
    }
    void getRightBottom(int& x, int& y)const{
        x = rightBottomX;
        y = rightBottomY;
    }
    int getWidth()const{ return rightBottomX - leftTopX; }
    int getHeight()const{ return rightBottomY - leftTopY; }

    int getArea()const;  // 명시만
    void moveBy(int deltaX, int deltaY);  // 명시만
};

#endif
```

```cpp
// Rectangle.cpp
#include <iostream>
#include "Rectangle.h"

int Rectangle::allCount = 0;
int Rectangle::getArea()const { return getWidth()*getHeight(); }
void Rectangle::moveBy(int deltaX, int deltaY){
    setLeftTop(leftTopX + deltaX, leftTopY+deltaY);
    setRightBottom(rightBottomX + deltaX, rightBottomY + deltaY);
}

```

```cpp
// RectangleMain.cpp
#include <iostream>
#include "Rectangle.h"
using namespace std;

void readRectangle(Rectangle& r){
    int x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;
    r.set(x1, y1, x2, y2);
}

void printRectangle(const Rectangle& r){
    int x1, y1, x2, y2;
    r.getLeftTop(x1, y1);
    r.getRightBottom(x2, y2);
    cout << x1 << "\t" << y1 << "\t" << x2 << "\t" << y2 << endl;
    // r.setLeftTop(0,0); 은 Error 발생 <= const 때문에
}

int main(){
    Rectangle r;
    readRectangle(r);
    printRectangle(r);
}

```
