# count的理解和使用(C++ algorithm)
避免自己写循环，使用以下标准函数的好处是：
`count` `count_if` `all_of` `any_of` `none_of` 
is the same regardless of whether you are counting a `vector` or a `map` and regardless of what the collection holds.

包含头文件：
```c++
#include <algorithm>
```
示例代码：
```c++
vector<int> v{ 2,7,1,6,2,-2,4,0 };

//count how many entries have the target value (2)
int twos = 0;
int const target = 2;

twos = count(v.begin(), v.end(), target);
twos = count(begin(v), end(v), target);//Try to always use this!!!

//count how many entries are odd
int odds = 0;
odds = count_if(begin(v), end(v), [](auto elem) {return elem % 2 != 0; });

map<int, int> monthlengths{ { 1,31 },{ 2,28 },{ 3,31 },{ 4,30 },
{ 5,31 },{ 6,30 },{ 7,31 },{ 8,31 },{ 9,30 },{ 10,31 },{ 11,30 },{ 12,31 } };

int longmonths = count_if(begin(monthlengths), end(monthlengths), 
[](auto elem) {return elem.second == 31; });

//Are all, any, or none of the values odd? (Conclude from number of odd entries)
bool allof, noneof, anyof;
allof = (odds == v.size());
noneof = (odds == 0);
anyof = (odds > 0);

allof = all_of(begin(v), end(v), 
[](auto elem) {return elem % 2 != 0; });
noneof = none_of(begin(v), end(v), 
[](auto elem) {return elem % 2 != 0; });
anyof = any_of(begin(v), end(v), 
[](auto elem) {return elem % 2 != 0; });

```