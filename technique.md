---
title: 典型テクニックまとめ
layout: document
---

一度でも出題されたら典型！（素振り）

### 数え上げ

* Bell Number: 区別できる $ n $ 個のボールを区別できない $ k $ 個以下の箱に分割する
    * 特に $ B(n, n) $ は $ n $ 個のボールを任意個のグループに分割する方法の数である。
    * 怪しい　[https://mathtrain.jp/zensya:title]　でしか見たことがない
    * wikipediaと定義が違う　[https://ja.wikipedia.org/wiki/%E3%83%99%E3%83%AB%E6%95%B0:title]
* Stirling Number (1st kind): $ n $  個のボールを $ k $ 個の非空のsubsetに分割する通り数
    * $x(x-1)(x-2)(x-3) \ldots (x-n)$ の$k$次の係数とも取れる
* Montmort Number: 撹乱順列の個数 包除原理で求められる
* ソートして大きいものから考える
* 区間の端だけ求めると $ \sum (r_i -l_i) $  で求められる
* 候補の区間が複数ある場合は最長のものだけ考える
* ちょうど $ K $ 個 = ($ K $ 個以下) - ( $ K - 1 $ 個以下 )
* 全ての $ x \in G $ に対し $ f(x) \in H $ を数えるとき、$ y \in H $ に対し $ f^{-1}(y) = x $ なるものを数えることもできる
* 多項式の係数のGCDは積に対して準同型をなす（ $ c(P) c(Q) = c(P Q) $
* $ \sum{ \binom{i}{j} } $の形は高速に求められることがある（黒白が $X, Y $ 枚あって、その中から $L$ 枚選んで並べる）とか  [https://atcoder.jp/contests/arc061/tasks/arc061_d:title]
* 判定問題を考える（ある条件を満たすものは何通り？→与えられたものは条件を満たすか？）
* 状態を準同型でまとめる（和、差など）
* $ \sum_{a \ge 0, b \ge 0, a + b = c} H(x, a) H(y, b) = H(x + y, c) $ [https://codeforces.com/contest/848/problem/D:title]
* 操作回数の期待値 = 各操作を行う回数の期待値の和 [https://atcoder.jp/contests/ttpc2019/tasks/ttpc2019_j:title] [https://atcoder.jp/contests/agc049/tasks/agc049_a:title] [https://atcoder.jp/contests/arc114/tasks/arc114_e:title]
* 連結性は除原理 [https://atcoder.jp/contests/arc105/tasks/arc105_f:title] [https://atcoder.jp/contests/abc213/tasks/abc213_g:title]
  * dp を二つ持ち、  $ \mathrm{d p 1} $ を連結性無視したもの、 $ \mathrm{d p 2} $ を連結性を考慮したものとして小さい集合から順番に（適当な $v$ を固定して） $ \mathrm{d p 2}[S] = \sum_{v \in T \subsetneq S} \mathrm{d p 2}[T] \mathrm{d p 1}[S \setminus T] $ で計算する
  * FPS の $\log$ でもできる（要出典）


### グラフ
* 次数1の頂点を取り除く
* 次数が1の頂点を見る
* 平面上の包含関係は木構造になる
* 根付き木の同型判定は子をソートしながら()で囲うと $ O(N^{2} \log N) $ でできる
    * hashでやれば $ O(N \log{N} ) $
    * [https://atcoder.jp/contests/nikkei2019-2-final/tasks/nikkei2019_2_final_d:title]
* グラフをオイラー路に分割するときの最小の数は  $ \sum_{v} \max{(i_v - o_v, 0)} $
* Oreの定理：任意の隣接しない二頂点の字数の和が頂点数以上ならハミルトン閉路が存在する
* Konigの定理：二部グラフの辺彩色は最大次数と一致する
* 辞書順最大の独立安定集合はgrundy数になる


### 木
* 根を固定した時、部分木のサイズが自分より大きくなる辺は根以外でちょうど一本存在する
* 部分木はオイラーツアーで一つの区間になる
* パスはHL分解で $ O(\log N) $ 個の区間になる
* 高さの和の部分和問題は上界と下界で挟める
* 高さが低いなら葉がたくさんある 参考: [https://codeforces.com/contest/1104/problem/E]
    * より形式的には、高さが $h $ なら少なくとも$ \frac{n-1}{h} $個はある
* 各頂点の次数はプリュファーコードでの出現回数 + 1 になっている [https://yukicoder.me/problems/no/1302:title]


### 構築
* へび
* 二べき
* 縦横でダメなら斜め [Grand Prix of Nanjing - A](https://official.contest.yandex.ru/opencupXXI/contest/24046/problems/)
* 非対称なものを作りたいときは乱択する
* 二つ作って重ねる [AGC025D](https://atcoder.jp/contests/agc025/tasks/agc025_d), [AGC027D](https://atcoder.jp/contests/agc027/tasks/agc027_d)


### 幾何
* 格子点のみを頂点とする図形の面積は $ 0.5 $ 刻み（ピックの定理）
* 放物線をつなげて一番高いところに行きたい場合は終点の傾きを一致させる


### ゲーム
* 小さい制約の問題をgrundyで解いてエスパーする
* DPできる制約ならする
* 不変量を考える
* 交互に隣接する頂点を選んで動かせなくなった方が負けのゲームで後手勝ち⇔完全マッチングが存在
    * [https://oi.in.ua/wp-content/uploads/2019/10/seerc-2019-editorial.pdf]

### 文字列
* ある文字列をずらして一致してる部分を最大化⇒FFT
* 辞書順最小を求める場合はprefixではなくsuffixでDPする
* distinctな文字列の数え上げは直近の文字にだけ遷移するようにすればできる [AGC027E](https://atcoder.jp/contests/agc027/tasks/agc027_e), [ARC110E](https://atcoder.jp/contests/arc110/tasks/arc110_e)
* 辞書順最小のconcatは $x+y<y+x$でソート [ECR9-C](https://codeforces.com/contest/632/problem/C)
* 文字列のソートは長さの総和を $ S $ とすると $ O(S \log S) $ でできる（STLでも）
* 文字列をいくつかの連続部分列に分けると独立に考えられる場合がある


### 最適化
* 最適解を持ってきて性質を見る
* 他の情報から復元できるパラメータを探す
* 自由度が一つ落とせる場合は半分全列挙ができる
* 極大と最大が一致するかを考える
* 順番を決める問題は適当な基準でソートして貪欲かDP
* 操作によっていくつかの区間に分かれ、それぞれが独立なものは区間DP
* $ f(X) $ の最小化は $ X $ を決め打ったときの性質に注目する
* 最大値、最小値に注目する


### オーダー改善
* ペア、トリオだけ考える
* 最初の一つを決めると残りも決まる
* 冪乗が出てきた場合、k=1を場合分けで取り除くとsqrtに落ちる
* 調和級数でlogになる  $\displaystyle \sum_{i=1}^{N} \frac{1}{i}= O(N \log N) $
* 個数制限付きナップザックは2冪に分解すると高々log個の01ナップザックになる
* 使わなかったものを最後にまとめて貪欲
* 配るDPをもらうDPに書き換えてセグ木で高速化
* 多次元DPでは一番小さいパラメータを動かす
* 部分集合の列挙は $ O(3^{n}) $ でできる（ for(int i=b;i>0;i=(i-1)&b);
* 同じ状態をまとめる
* 各要素が高々一つのときはbitDP
* 階差を考える
* 累積和をとる
* $ a \gt b $ なら $ (a \bmod b) \lt a/2 $
    * MODを取って結果が変化するのはlog回（毎回半分以下になるので）
* 累積和を $ k $つずらすのは $ O(k) $ でできる
* Master Theorem
    * $T(N) = a T(N/b) + f(N)$ の形の漸化式を満たす計算量の解析
    * [https://tomorinao.blogspot.com/2018/10/devide-and-conquer-and-master-theorem.html:title]
    * $a = b = 2$ [https://codeforces.com/contest/949/problem/E:title]
* 適当なポテンシャルを考えると償却できる
    * LCT が有名
    * [https://atcoder.jp/contests/agc044/tasks/agc044_b:title]
* 高度合成数
  [https://web.archive.org/web/20210731133024/https://www.firiex.com/dokuwiki/%E7%AB%B6%E3%83%97%E3%83%AD/%E9%AB%98%E5%BA%A6%E5%90%88%E6%88%90%E6%95%B0:title]
  * $10^{12}$ 程度なら $d^{2}$ が間に合う
* 以上／未満で二値に分類
    * [D - Median Pyramid Hard](https://atcoder.jp/contests/agc006/tasks/agc006_d)
    * [G - Range Sort Query](https://atcoder.jp/contests/abc237/tasks/abc237_g)


### 定数倍改善
* setのlower_boundは遅いので変更がないならvectorを使う
* キャッシュの載り方を意識する
* 構造体を渡す時は参照渡しにする
* unordered_map, unordered_set
    * <b>reserveすると100倍くらい変わる</b>
* pb_ds_cc_hash_table


### 手抜き実装
* 番兵を入れると境界値判定が不要になる
* 手抜きしてもいいか実装前によく確認する
* 等価に思える処理が等価かどうかよく確かめる


### デバッグ
* <span style="font-size: 200%">オーバーフローに気をつける</span>
* 負数のMODを取ると負数になる
* string::find で見つからなかった時に帰ってくるのはstring::npos （-1とは限らない）
* printf ではちょうど1/2は切り捨てられる（+EPSすれば回避可能)
* std::lower_boundをsetに使うと $ O(N) $


### 勘違い
* DAGでないグラフで最小値を求める場合はメモ化再帰ではなくDijkstra
* a -> c の最短路の長さと (a -> b の最短路の長さ)+(b -> c の最短路の長さ) は必ずしも一致しない
* フローでの頂点の流量は（自分で制限しないと）無限
* 次数が3以上のグラフでDFSで全探索は普通にやるとできない
    * 最後の子を探索するとき左の子の探索は最終状態しか残っていない
* 嘘解法を考えすぎない
* 乱択はよっぽどのことがないと通らない
    * 投げる前に確率を見積もる


### 未分類
* 単調性がないかどうか考える（あれば二分探索できる）
* 最小値の最大化、平均最大化は二分探索
* K番目の値を求める時はX以下の数を数える二分探索
* 入力を乱数で生成すると最悪ケースがなくなる
* 操作を繰り返す系は不変量に注目する
* マンハッタン距離の総和の最小化はn/2番目の値
* <span style="font-size: 200%">マンハッタン距離は回す！！</span>
    * $(x, y) \rightarrow (x+y, x-y) $とすればよい
* 中央値を求める時はペアを作る
* 逆から見る
* クエリを先読みする
* $\gcd(x, x+1) = \gcd(x, 1) =  1$
* BITはmapで動的に構築すると空間 $ O(Q \log Q) $、時間 $ O(Q \log^{2} Q) $
* 左右で分けてくっつける
* 各人が選択をするとき、同じ選択をする人をまとめて考える [AGC022D](https://atcoder.jp/contests/agc022/tasks/agc022_d)
* 半分ずつになるDPのとき、幅は高々 $\log$ 個見ればいい
* 操作が可逆な時 A->Bにできる ⇔ B->Aにできる ⇔ A->C->Bにできる ⇔ A->C, B->Cにできる
* 行反転と列反転で01を全て同じ色にできる ⇔ 任意の小正方形(2x2)内のxorが0 [ARC081D](https://atcoder.jp/contests/arc081/tasks/arc081_d)
* 関数は合成に関してモノイドをなす（セグ木に載る）
* yが一定なら $ \max(\mathrm{floor}(\frac{x}{y})) = \mathrm{floor}(\frac{\max(x)}{y}) $
* maxとfloorとaddは合成できる（遅延セグ木に載る） [JAG](https://atcoder.jp/contests/jag2018summer-day2/tasks/jag2018summer_day2_i)
* 要素を[k, k+len) に並べるような場合はすべてのx座標からiを引いておく
* ある値xを作れるか⇔∑lb ≤ x ≤ ∑ub
* ある条件を満たすものが一つでもあるかという質問は、個数を求めると逆元を作れる [dowango](https://atcoder.jp/contests/dwacon5th-prelims/tasks/dwacon5th_prelims_d)
* p進数での桁和と元の数はmod (p-1)で一致する
* 操作で順序が入れ替わらないことがある
* 可換な操作を全体に対して行うような操作は分割統治で順序関係を制限できる
* 和と差はmod2で不変
[https://twitter.com/DEGwer3456/status/1241375867067961344?s=20:embed]
* xor に対して準同型なhash ってなーんだ？ zobrist hash
* 区間カウントクエリはMo [https://codeforces.com/contest/840/problem/D:title]
