# [[fallthrough]]属性
* cpp17[meta cpp]

## 概要

[[fallthrough]]属性は意図したフォールスルーであることをコンパイラに伝え、警告を抑制するための属性である。

## 仕様

switch-case文において意図しないフォールスルーによってバグが発生することを防止するため、コンパイラはコンパイル時にフォールスルーを検出して警告を出力する場合がある。

プログラマが意図してフォールスルーを行う場合、コンパイラの警告は無用であるが、警告を抑制する方法が無かった。[[fallthrough]]属性により意図したフォールスルーであることをコンパイラに伝え、警告を抑制することができる。

[[fallthrough]]属性はフォールスルーしたい各caseの最後の式に記述する。ただし最後のcase/defaultに記述するとコンパイルエラーとなる。

## 例
```cpp
void f(int n) {
  void g(), h(), i();
  switch (n) {
  case 1:
  case 2: //caseの間に1つも文がなければフォールスルーは警告されない
    g();
    [[fallthrough]];
  case 3: //[[fallthrough]]属性の記述によりフォールスルー警告は無効化される
    h();
  case 4: //コンパイラがフォールスルーを警告する
    i();
    [[fallthrough]]; //最後のcaseには記述できない、コンパイルエラーになる
  }
}
```

### 出力
```
(対応コンパイラがあれば、コンパイル結果を後ほど記述)
```

## 参照
- [P0068R0 Proposal of [[unused]], [[nodiscard]] and [[fallthrough]] attributes.](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0068r0.pdf)
- [P0188R1 Wording for [[fallthrough]] attribute.](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0188r1.pdf)