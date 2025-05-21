# C++11

auto

```cpp
#include <iostream>

int main()
{
  // ブロックスコープでの変数宣言
  static auto s = "C++";                                        // s は const char* 型

  // `for` 文の初期化文、および、条件部での変数宣言
  for (auto p = s; auto elem = *p; ++p) {                       // p は const char* 型、elem は char 型
    std::cout << elem << ", ";
  }
  std::cout << '\n';
}
```

範囲for文

`begin()`, `end()`で表される領域を走査する。
要素を追加、削除する場合には使えない。

```cpp
std::vector<int> v;

for (const auto& e : v) {
  std::cout << e << std::endl;
}
```

リスト初期化

```cpp
// 1, 2, 3の3要素を持つ配列オブジェクトを定義する
int ar[] = {1, 2, 3};
std::vector<int> v1 = {1, 2, 3};
std::vector<int> v2 {1, 2, 3};

// 再代入
v2 = {4, 5, 6};
```

一様初期化

```cpp
#include <string>

struct X {
  X(int, double, std::string) {}
};

X createX()
{
  return {1, 3.14, "hello"}; // OK
}
```

```cpp
vector<int> vec1 = {1, 2, 3};
int val = 4;
const vector<int> 
combined_vec = {vec1.begin(), vec.end(), val};

vector<int> vec2 = {4, 5};
const vector<int> combined_vec2 = {vec.begin(), vec.end(), vec2.begin(), vec2.end()};
```

ラムダ式
```cpp
auto plus = [](int a, int b) { return a + b; };
int result = plus(2, 3); // result == 5
```

### 関数のdefault/delete宣言

クラス定義時に暗黙に定義される以下の特殊関数を制御する
- デフォルトコンストラクタ
- コピーコンストラクタ
- ムーブコンストラクタ
- コピー代入演算子
- ムーブ代入演算子
- デストラクタ

キーワードの意味
- default：暗黙定義されるデフォルト挙動を採用する
- delete：暗黙定義を明示的に禁止する

```cpp
class X{
public:
	// コピーを禁止する
	X(const X&) = delete; 
	X& operator=(const X&) = delete;
	// ムーブを許可する
	X(X&&) = default;
	X& operator=(X&&) = default;
}
```

unique_ptr
```cpp
std::unique_ptr<hoge> p0(new hoge());
std::unique_ptr<hoge> p1(std::move(p0));
```

make_unique
```cpp
std::unique_ptr<int[]> p2 = sdtd::make_unqiue<int[]>(3);
```

emplace_back
`push_back`の早いやつ
```cpp
std::vector<std::unique_ptr<Item>> items{};
items.emplace_back(std::make_unique<CPPBook>("Effective C++", "Scott Mayers", 19.99))
```

std::function
関数を別の関数の引数として渡すときの型
```cpp
#include <functional>
#include <iostream>

int add(int x, int y) {
    return x + y;
}

int execute(int x, int y, std::function<int(int,int)> func){
    return func(x, y);
}

int main(){
    int x = 2, y = 3;
    std::cout << execute(x, y, add) << std::endl;
    return 0;
}
```