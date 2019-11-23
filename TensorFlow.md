# 用語
## 機械学習
- インスタンス: とりあえず用意した箱みたいな
- データセット: インスタンスの集まり
- ハイパーパラメータ : 
    - 数値的に決定できないパラメータ
    - ex) 最適化手法に何を使うかなど
- 活性化関数: 
    - 出力を正規化するためにかける関数
    - ex) ある値以上で確率80%として出力する。など
- モデル: ネットワークそのもの
- トレーニングセット ⇔ テストセット
    - トレーニングセット: モデルのトレーニングに使用
    - バリデーションセット: できたモデルのチューニングに使用する
    - テストセット: 出来たモデルのテストだけに使う
- プレースホルダー: 空の配列とか
- 損失関数: CNNの場合は`(y_actual - y_pred)^2`とか
- バッチトレーニング ⇔ 確率的トレーニング
    - 使ってる最適化手法による違い
    - バッチ: 普通の勾配法。ゆっくり下がってく。
        - バッチサイズ: 観測データの数？
    - 確率的: SGDってやつ。めっちゃ振れる。
- L1損失 ⇔ L2損失
    - |y_actual - y_pred| ⇔ |y_actual - y_pred|^2
    - L2は目的値の近くでとがった急なカーブを描いていることが特徴
 
## 遺伝的アルゴリズム
- crossover: 交叉
    - 親を組み合わせて子を作る
    - 一点交叉、二点交叉などがある(バイナリコーディングと実数値コーディングで違う)
- mutation: 突然変異
    - 変なのも親に入れてみる的な
- features: 特徴量の数
    - 設計パラメータの数とも言える
- generations: 世代数
    - すなわちイテレーション数
- selection: 淘汰(の割合)


## 一般的
- スライス
    - Python用語。配列の一部を切り取る
    - ex) `s = "Python" `とすれば、s[2:5] → "ytho"

## 英語
- Normal distribution
    - 正規分布
    - = Gaussian distribution: ガウス分布
- 

# 関数
## TensorFlow
- tf.Variable(tensor)
    - 変数を定義する
    - 変数とプレースホルダーは違うらしい...
- tf.global_variables_initializer()
    - 変数を初期化
- tf.square(x)
    - x^2
- tf.subtract(x, y)
    - x-y
- tf.matmul(a, b)
    - a*b
- tf.reduce_mean(tensor, axis)
    - tensorの要素から平均を求め、axisの次元に圧縮する
    - すべての評価関数に関して同じ重み付けにするためと思われる
- tf.reduce_min(tensor, axis)
    - tensorの要素から最小値を求め、axisの次元に圧縮する
- tf.nn.top_k(input, k)
    - inputの中からトップkまでの値を取り出す
    - つまりソートからのスライス
    - return 取り出した値, 取り出した値のinputの中でのインデックス
- tf.arg_min(input, dimension)
    - inputの中の最小値(のインデックス)を求めて返す
    - ベクトルから選ぶならdimensionは0
- tf.gather(param, indices)
    - param配列の中から、インデックス(複数)に対応したものを取り出す
- tf.slice(input, begin, size)
    - テンソルは配列0~i番目までの配列の集合だとすると、
    - begin=[k, x, y]とすると、k番目の配列の(x,y)座標を始点とする、という意味になる。
    - size=[a, b, c]とすると、beginから配列方向にa, x方向にb, y方向にc広がった部分をスライスする、という意味になる。
    - 分かりずらいけど[例](https://www.tensorflow.org/api_docs/python/tf/slice)を見たら分かるはず。
- tf.concat(values, axis)
    - values=[x, y]をaxisの部分で連結する。
    - axis=0ならxとyの境目が無くなる
    - axis=1ならxの中、yの中で境目が無くなる
    - そんな感じ
- tf.random_normal(shape)
    - 正規分布からランダムに選ばれたでshapeのテンソルを埋める
- tf.train.GradientDescentOptimizer(learning_rate)
    - 勾配降下法
    - 引数は学習率
- tf.cast()

- tf.equal()



## Numpy
- np.arrange(start, stop, step, dtype)
    - startからstopまで等差stepの数列を作成する。
    - stepを省略したら等差1
    - startを省略したらstopの数だけ
    - dtypeは自動選択されるが、int, float32のように指定することも可
- np.linspace(start, stop, num)
    - startからstopまでnum個の数列を作成する。
- np.random.randn(size)
    - 平均0, 分散1の正規分布(標準正規分布)に従う乱数行列作成
    - sizeに行列のサイズを指定。ex) np.random.randn(3, 3)
- np.random.normal(loc, scale, size)
    - 平均loc, 分散scaleの正規分布に従う乱数発生
- np.random.choice(a, size, replace=False)
    - 配列からsizeぶんランダムに選んで、そのインデックスを返す
    - replace=Trueなら重複あり
- np.transpose(axis)
    - 転置する

## Other
- round(f, n)
    - fを小数第n位で四捨五入する
    - デフォルトはn=0
    - ex) f=12.345 n=1なら 12.3
    - nは負の値も設定可能