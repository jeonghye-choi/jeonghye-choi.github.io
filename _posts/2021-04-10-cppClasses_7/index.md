---
title: c++ Classes, this
date: 2021-04-10
tags:
  - c++
keywords:
  - c++
  - class
  - this
---

this : 객체 자신을 가리키는 pointer

특별히 선언하지 않아도 컴파일러에 의해 자동으로 정의되어 사용된다.

## Example1: 인자와 데이터멤버 구분

기존엔 "\_" 를 이용해서 인자와 데이터멤버를 구분했다. this를 통해 데이터 멤버를 가리키게 할 수 있다!

즉, 데이터멤버와 같은 이름의 인자 사용가능!

```cpp
// Rectangle.h
#ifndef Rectangle_h
#define Rectangle_h
class Rectangle{
    int leftTopX, leftTopY;
    int rightBottomX, rightBottomY;
public:
    ...
}

void setLeftTopX(const int leftTopX){
    this->leftTopX = leftTopX; // this->leftTopX는 private에 있는 데이터멤버를 가리킴.
}
void setLeftTopY(const int leftTopY){
    this->leftTopY = leftTopY;
}
void setRightBottomX(const int rightBottomX){
    this->rightBottomX = rightBottomX;
}
void setRightBottomYX(const int rightBottomY){
    this->rightBottomY = rightBottomY;
}
#endif
```

## Example2: 자신의 객체 그 자체!

```cpp
// Rectangle.h
#ifndef Rectangle_h
#define Rectangle_h
class Rectangle {
public:
    Rectangle* copy()const{
        Rectangle* r = new Rectangle;
        r->setLeftTopX(getLeftTopX());
        r->setLeftTopY(getLeftTopY());
        r->setRightBottomX(getRightBottomX());
        r->setRightBottomY(getRightBottomY());
        return r;
    }
    // 위의 copy()를 this를 사용해서 아래와 같이 정의할 수 있다.
    Rectangle* copy()const {
        return new Rectangle(*this);
        // this는 포인터다. 자신의 객체값을 그대로 전달!
        // 동일한 타입의 객체를 만들어냄 => copy constructor 호출.
    }
    bool isEqual(const Rectangle& r)const {
        return leftTopX == r.leftTopX
            && leftTopY == r.leftTopY
            && rightBottomX == r.rightBottomX
            && rightBottomY == r.rightBottomY;
    }
};
#endif
```

```cpp
// main.cpp
#include <iostream>
#include <cassert>
#include "Rectangle.h"
using namespace std;

int main(){
    Rectangle r;
    r.set(0, 0, 100, 200);

    Rectangle* pR = r.copy();
    // r이라는 Rectangle과 똑같은 Rectangle을 만들어서 그에대한 pointer리턴!
    assert(pR->isEqual());
    // assert는 디버깅을 위한 에러검출 함수! ()안의 조건을 만족해야함! 그렇지 않으면 에러를 띄워 알려준다:)

    delete pR;  //  new 연산자를 사용해서 만든 개체에 대해 삭제!
}
```

## Example3:

```cpp
// main.cpp
#include <iostream>
#include "Rectangle.h"
using namespace std;

int main(){
    Rectangle r;
    r.set(0, 0, 100, 200);

    cout << r.moveBy(10,10).print() << endl;  // 10 10 110 210
    // 이동후->print : moveBy가 Rectangle을 호출해야지 print가능

    cout << r.moveBy(10,10).moveBy(10,10).print() << endl;
    // expected: 30 30 130 230, but actually 20 20 120 220
    // moveBy가 Rectangle객체로 return 하는지, reference로 return 하는지에 따라 결과가 달라질 수 있다.
    // => moveBy후 또 moveBy: 원하는 결과를 위해서는 reference로 reture해야한다!

    r.moveBy(10,10).print();
    cout << r.moveBy(10,10).print().getArea() << endl;
}
```

따라서,

```cpp
// Rectangle.h
#ifndef Rectangle_h
#define Rectangle_h
class Rectangle {
public:
    ...
    Rectangle& moveBy(int deltaX, int deltaY);
    const Rectange& print()const{
        cout << leftTopX << leftTopY << "\t" << rightBottomX << "\t" << rightBottomY << endl;
        return *this;
    }
    int getArea()const{...}
}

#endif
```

```cpp
#include "Rectangle.h"

...
Rectangle& Rectangle::moveBy(int deltaX, int deltaY){
    // &(reference)를 하지 않는다면, return되는 this는 자신이 아닌 copy가 될 수 있다.
    setLeftTop(leftTopX+deltaX, leftTopY+deltaY);
    setRightBottom(rightBottomX+deltaX, rightBottomY+deltaY)
    return *this;
}
```
