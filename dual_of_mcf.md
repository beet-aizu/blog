---
title: 最小費用流の双対
layout: document
---

### 主問題

 $l,u,g,w$ が与えられたり与えられなかったりしたとき（$l, g$ は与えられなくても  $0$ にしてしまえる）、以下の形の問題を最小費用流に帰着できる：

$ \displaystyle \max_{0 \le a,b,p} \sum_e l_e a_e - \sum_e u_e b_e - \sum_v g_v p_v $

s.t.

- $ a_e - b_e + p_v - p_u \le w_{uv} $
- $ (\sum_v g_v) = 0 $

イメージ的には

- $a_e $ は「条件を満たしたまま最大化するための変数」例：AOJ 2230 How to Create a Good Game
- $b_e$ は「条件を満たすために必要な最低限の量どうにかする変数」例：KUPC 2019 H - 123パズル
- $p_v $ は「二変数の差の制約を表すための変数」

いずれも非負である必要があることに注意

また、式からもわかるように $ l, u, g $ は目的関数における $ a, b, p $ の係数である

### 双対問題

双対問題として対応する最小費用流のLPは以下のように定式化される：

$ \displaystyle \min_{0 \le f} \sum_e w_e f_e $

s.t.

- $f_e \ge l_e $
- $  -f_e \ge -u_e $
- $\displaystyle \sum_{e \in \mathrm{in}(v)} f_e - \sum_{e \in \mathrm{out}(v)} f_e = -g_v $

制約の上二つの式をまとめて書くと、$ l_e \le f_e \le u_e $ となる

つまり、$l$ が最小流量制約を、$ u $ が最大流量制約を表す

また、$ g_v $ はその頂点からどれだけフローが湧き出るかを表す

頂点 $ v$ は、$ g_v > 0 $ のときソースに、$ g_v < 0 $ のときシンクになる

したがって、超頂点 $S, T $ を導入し、以下のようにグラフを構築することで主問題の最適解を得られる

- 全ての $w_{e=uv}$ について、 $ u \rightarrow v$に最小流量 $l_e $ 、最大流量 $ u_e$ , コスト $w_e$ の辺を張る
- $ g_v > 0$ なる $v$ について $ S \rightarrow v $ に流量 $ g_v$ , コスト$0$ の辺を張る
- $ g_v < 0$ のとき $v  \rightarrow T$  に流量 $-g_v$ , コスト$0$  の辺を張る

### 実装例

$V$ : 頂点数、$E$ : 辺数、$F$ : 全体の流量、 $U$ : 辺一本あたりの流量の上界、$C$ : 辺一本あたりのコストの上界 として

- [Primal Dual](https://beet-aizu.github.io/library/mincostflow/primaldual.cpp): $O(FE \log V)$
- [Capacity Scaling](https://beet-aizu.github.io/library/bflow/capacityscaling.cpp): $O(E^2 \log V \log U) $
- Cost Scaling: $O(V^3 \log (VC))$

### その他
そもそもどんな問題が解けるのかや、二変数の差に関するテクニックは [双対性](https://www.slideshare.net/wata_orz/ss-91375739) が詳しい

また、この記事は主に [競プロとLP双対まわりの話で最近知ったこと](http://tokoharuland.hateblo.jp/entry/2016/12/06/223614) を参考にした
