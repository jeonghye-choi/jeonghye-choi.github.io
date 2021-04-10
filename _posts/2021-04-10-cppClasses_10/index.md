---
title: c++ Classes, Information Hidiing
date: 2021-04-10
tags:
  - c++
keywords:
  - c++
  - class
  - Information Hidiing
---

## private and public members

모듈화를 위해서, 중요하지 않은 정보는 숨김.

또한 유지성과 유지성을 위해서 (public한 부분만 이해하면 되기 때문에)

### 구조

```cpp
class class_name{
private:
    data members  // private에 있는 데이터멤버는 클래스 밖에서 접근 불가능
public:
    member functions
};
```

### Example

```cpp
class Rectangle{
private:
    int leftTopX, leftTopY;
    int rightBottomX, rightBottomY;
    void setLeftTop(int x, int y){
        leftTopX = x;
        leftTopY = y;
    }
    void setRightBottom(int x, int y){
        rightBottomX = x;
        rightBottomY = y;
    }
public:
    void set(int x1, int y1, int x2, int y2){
        setLeftToop(x1, y1);
        setRightBottom(x2, y2);
    }
    void getLeftTop(int& x, int& y)const{
        x = leftTopX;
        y = leftTopY;
    }
    void getRightBottom(int& x, int& y)const{
        x = rightBottomX;
        y = rightBottomY;
    }
    int getArea()const{
        return (rightBottomX-leftTopX)*(rightBottomY-leftTopX);
    }
}
```

```cpp
int main(){
    int x1, y1, x2, y2;
    cin >> x1 >> y1 >> x2 >> y2;

    Rectangle r1;
    r1.set(x1, y1, x2, y2);
    r1.leftTopX = r1.leftTopX + 1   // ERROR: private 접근 불가

    int x3, y3, x4, y4;
    r1.getLeftTop(x3, y3);
    r1.getRightBottom(x4, y4);

    Rectangle r2;
    r2.setLeftTop(x3, y3);  // ERROR : private 접근 불가 -> set사용
    r2.setRightBottom(x4, y4);  // ERROR : private 접근 불가 -> set사용
    r2.set(x3, y3, x4, y4);    // OK

    cout << endl << r1.getArea() << "\t" << r2.getArea() << endl;
}
```

## friend function and friend class

friend는 private 임에도 불구하고 외부에 접근을 허용한다.

friendsms information hiding principle을 위배하기 때문에 최소한의 상황에서 사용권장.

### 가능한 friend forms

- 1 friend non-member function

- 2 friend class

- 3 friend member function

### 1. friend non-member function

#### 구조

```cpp
// friend 함수
void f(){ ... }
```

```cpp
class SomeClass {
[private:]
    전용멤버
[public:]
    공용멤버
    friend void f();
};

```

#### Example

```cpp
// Window.h
class Window {
private:
    ...
    string title;
    ...
public:
    string getTitle() const;
    friend void friendOfWindow(const Window&);
    void nonFriendOfwindow(const Window&);
};
```

```cpp
// WindowMain.cpp
void friendOfWindow(const Window& anWindow){
    cout << anWindow.title;
}
void nonFriendOfwindow(const Window& anWindow){
    cout << anWindow.title;  // ERROR
    cout << anWindow.getTitle();

}
```

### 2. Friend Class

#### 구조

```cpp
// friend 함수
class C {
    멤버함수_1
    멤버함수_2
    ...
    멤버함수_n
}
```

```cpp
class SomeClass {
[private:]
    전용멤버
[public:]
    공용멤버
    friend class C;
};

```

#### Example1

```cpp
class StringNode {
    string data;
    StringNode* next {nullptr};

    StringNode(const string& d="")
    : data(d) {}
    bool isEqual(const StringNode& n)const{
        return data == n.data;
    }
    friend class StringList;
}
```

#### Example2

```cpp
class StringList {
    StringNode* head {nullptr}  //default is private
public:
    StringNode* addNode(const string& data){
        StringNode* newNode = new StringNode(data);
        if ( head==nullptr ){ head = newNode; }
        else {
            head->next = newNode;
            head = newNode;
        }
        return newNode;
    }
    void removeNode(const StringNode* const node){
        StringNode* cur = head, * prev = nullptr;
        while ( cur != nullptr ) {
            if (next->isEqual(*node)){
                if (prev) {
                    prve->next = cur->next;
                } else {
                    head = cur->next;
                }
                delete cur;
                break;
            }
            cur = cur->next;
        }
    }
};
```

### 3. Friend Member Function

```cpp
class StringNode {
private:
    string data;
    StringNode* next {nullptr};
public:
    bool isEqual() const;
    StringNode* getNext() const;
    void setNext(const StringNode* const);
    friend void StringList::addNode(const StringNode& node);
};

class StringList {
    StringNode* head {nullptr};
public:
    void addNode(const StringNode& node){
        StringNode* newNode = new StringNode;
        newNode->data = node.data;
        newNode->next = nullptr;

        if (head==nullptr){
            head = newNode;
        } else {
            head->next = newNode;
            head = newNode;
        }
    }
    void removeNode(const StringNode& node){
        StringNode* cur = head, * prev = nullptr;
        while ( cur != nullptr ){
            if (next->isEqual(node)){
                if (prev){
                    prev->setNext(cur->getNext());
                } else {
                    head = cur->getNext();
                }

                delete cur;
                break;
            }
            cur = cur->getNext();
        }
    }
}
```
