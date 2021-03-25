---
title: 多次元の畳み込み
layout: document
---

## モノイド環
$R$ を環とし $X$ をモノイドとする

$R[X] = \left \\{ \displaystyle \sum_{x \in X} r_x x \mid r_x \in R \right \\}$ と定める
以後、これをモノイド環と呼ぶ

$a \in R[X]$ に対して、$x \in X$ の係数を $a_x \in R$ と書く

モノイド環の和と積を以下で定める

和：$ a + b = \displaystyle \sum_{x} (a_x + b_x) x $

積：$ a * b = \displaystyle \sum_{xy = z} (a_x b_y) z $

### 例：多項式環
$X = (Z_{\geq 0}, +, 0) $ とすると、これは多項式環になる

## 点ごとの積
モノイド環の点ごとの積を以下で定める

$ a \cdot b = \displaystyle \sum_{x} (a_x b_x) x $

以下では、点ごとの積と区別するため、単なる積を畳み込みと呼ぶこともある

モノイド環において、畳み込みを点ごとの積に移すような操作（環同型写像）を考える

### 例：フーリエ変換
$X = (Z_m, +, 0)$ に対して、

$a + b = \mathrm{idft}(\mathrm{dft}(a) + \mathrm{dft}(b)) $

$a * b = \mathrm{idft}(\mathrm{dft}(a) \cdot \mathrm{dft}(b)) $

であることがよく知られている（巡回畳み込み）

注意：競技プログラミングにおいては十分大きな $m$ を取ることで巡回を考慮しないようにしていることが多いが、後述する xor 畳み込みのように巡回性を利用する場合もある。

### 例：累積和と階差
$X_\max = (Z_{\geq 0}, \max, 0) $, $ f(a) = \displaystyle \sum_x \left (\sum_{y \leq x} a_y \right) x $ とすると

$a + b = f^{-1}(f(a) + f(b)) $

$a * b = f^{-1}(f(a) \cdot f(b)) $

また、$X_\min = (Z_{\geq 0}, \min, \infty) $, $ g(a) = \displaystyle \sum_x \left (\sum_{y \geq x} a_y \right) x $ とすると

$a + b = g^{-1}(g(a) + g(b)) $

$a * b = g^{-1}(g(a) \cdot g(b)) $

## 直積モノイドのモノイド環とその上の演算
二つのモノイド環 $K[X], K[Y]$ に対して、直積モノイドのモノイド環 $K[X \times Y]$ を考える

直積モノイドのモノイド環の和と積は定義に従い、以下のようになる

和：$ a + b = \displaystyle \sum_{(x, y)} (a_{(x, y)} + b_{(x, y)}) (x, y) $

積：$ a * b = \displaystyle \sum_{(x, y) \circ (p, q) = (s, t) } (a_{(x, y)} b_{(p, q)}) (s, t) $

## 多次元の畳み込み
$K[X], K[Y]$ と、それらの畳み込みを点ごとの積に移すような変換 $f, g$ が与えられたとき、直積モノイドのモノイド環の畳み込みを点ごとの積に移すような変換 $h$ を構成したい

驚くべきことに、これは $X$ 方向に $f$ を適用した後 $Y$ 方向に $g$ を適用すると実現できる

証明：

$X$ 方向を行、$Y$ 方向を列とするような行列を考える

$a \in K[X \times Y]$ に対して、$i$ 行目以外の要素を全て $0$ に置き換えた元を $a_i$ とする（以下では、特に断りなくその行のみ取り出した列と同一視する）

分配法則より、
$ a * b = \displaystyle \left (\sum_i a_i \right ) *  \left (\sum_k b_k \right ) = \sum_{i, k} a_i * b_k $

$ a_i * b_k $ の $i \circ k$ 行目以外の要素は $0$ になる

$a_i, b_k$ の各行に $g$ を適用したあと、各列に $f$ を適用し、点ごとの積を取ってから各列 $f^{-1}$ で戻したものを $c$ とする

$c_{(i \circ k, j)} = g(a_i)_j \ g(b_k)_j$ であるから、$g^{-1}(c) = a_i * b_k$ である ■

$3$ 次元以上の場合においても、帰納法を用いて同様に構成可能である

## 応用
### xor 畳み込み
$n$ bit の xor 畳み込みは $ X = (Z_{2^n}, \oplus, 0) $ の場合と解釈できる

$ (Z_{2^n}, \oplus, 0) \cong (Z_2, +, 0)^n $ より、サイズ $2$ の DFT を $n$ 次元に渡って適用すればよい

### or 畳み込み
$n$ bit の or 畳み込みは $ X = (Z_{2^n}, \|, 0) $ の場合と解釈できる

$ (Z_{2^n}, \|, 0) \cong (Z_2, \max, 0)^n $ より、（昇順の）累積和による変換を $n$ 次元に渡って適用すればよい

### and 畳み込み
$n$ bit の and 畳み込みは $ X = (Z_{2^n}, \&, \sim 0) $ の場合と解釈できる

$ (Z_{2^n}, \&, \sim 0) \cong (Z_2, \min, 0)^n $ より、（降順の）累積和による変換を $n$ 次元に渡って適用すればよい

### gcd 畳み込み
gcd 畳み込みは $ X = (Z_{\geq 0}, \gcd, 0) $ の場合と解釈できる

$ (Z_{\geq 0}, \gcd, 0) \cong \displaystyle \prod_{p} (Z_{\geq 0}, \min, \infty) $ より、（降順の）累積和による変換を素数ごとに適用すればよい

## 問題例
- https://codeforces.com/gym/102441/problem/E