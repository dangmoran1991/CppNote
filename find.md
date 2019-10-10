# find的理解和使用（C++ algorithm）

无需记忆函数名，可以通过cppreference.com来寻找需要的函数：https://en.cppreference.com/w/

例如：
`find_if_not` `find_first_of` `search` `find_end` `search_n` `adjacent_find`

示例代码：
```c++
//============================第一个例子：vector========================================
vector<int> v{  4, 6, 6, 1, 3, -2, 0, 11, 2, 3, 2, 4, 4, 2, 4 };

//find the first zero in the collection
auto result = find(begin(v), end(v), 0);

//find the first 2 after that zero
result = find(result, end(v), 2);

//find first odd value
result = find_if(begin(v), end(v), [](auto elem) {return elem % 2 != 0; });

//find first even value
result = find_if_not(begin(v), end(v), [](auto elem) {return elem % 2 != 0; });

vector<int> primes{ 1,2,3,5,7,11,13 };
result = find_first_of(begin(v), end(v), begin(primes), end(primes));

//search works with subsequence
vector<int> subsequence{ 2,4 };
result = search(begin(v), end(v), begin(subsequence), end(subsequence));

//这个函数也是寻找subsequence,虽然它不叫search
result = find_end(begin(v), end(v), begin(subsequence), end(subsequence));

//寻找两个连着的4
result = search_n(begin(v), end(v), 2, 4);

//寻找两个连着的一样的元素
result = adjacent_find(begin(v), end(v));


//============================第二个例子：string========================================
string s{ "Hello I am a sentence" };

//find the first a
auto letter = find(begin(s), end(s), 'a');

string am = "am";
letter = search(begin(s), end(s), begin(am), end(am));
```