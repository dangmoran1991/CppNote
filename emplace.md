# C++11 Emplace的理解和使用

C++11 introduced `emplace_front` `emplace` `emplace_back` - that **construct** rather than **copy** elements.

Before this, to put an element we use:
`push_front`: in front of the container
`insert`: in front of a given position
`push_back`: at the back of the container

## emplace与push的区别
+ When we call a `push` or `insert` member, we pass **objects** of the element type and those objects are **copied** into the container.
+ When we call an `emplace` member, we pass **arguments** to a **constructor** for the element type. (The emplace members use those arguments to construct an element directly in space managed by the container.) 

```C++
struct SalesData
{
    SalesData() = default;
    SalesData(const std::string &s) :bookNo(s) {}
    SalesData(const std::string &s, unsigned n, double p) :
        bookNo(s), unitsSold(n), revenue(p*n) {}

    std::string bookNo;
    unsigned unitsSold;
    doulbe revenue;
}

//Assuming c holds SalesData elements:
c.emplace_back("12345", 25, 15.99);//Correct: uses three-argument constructor
c.push_back("12345", 25, 15.99);//Wrong: there is no version of push_back that takes 3 arguments
c.push_back(SalesData("12345", 25, 15.99));//Correct: we create a temporary object to pass to push_back
```

## 总结
### 为什么说emplace_back比push_back更高效？
+ emplace_back直接在container的相应位置创建一个对象，只调用一次相应的构造函数。
+ push_back首先生成一个临时的对象，再将该对象拷贝到container相应的位置，调用一次构造函数+一次拷贝构造函数。

### 如果需要插入的是一个指针：
区别不大。push_back更好？？？
