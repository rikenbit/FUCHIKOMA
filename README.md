# FUCHIKOMA
FUCHIKOMA（ふちこま、天乃斑駒が由来）は、BAHSICとDiffusion Mapを利用した、非線形なPCAにおける主成分に寄与した遺伝子を特定する手法です。

# 特徴・メリット
1. Diffusion Mapを利用した非線形なPCA
2. 各主成分に寄与する遺伝子をBAHSICによる特徴選択で特定する
3. 複数の主成分が組み合わさった方向に寄与する遺伝子も選択できる
4. あらかじめクラス数の判定をする必要がない（教師無し）
5. ***による並列化
6. single-cell RNA-Seqに固有な***の補正
7. ***によるp-value、その後のFDR補正の対応

# 使い方
```r
# destinyを読み込む
library(destiny)

# データ読み込み
data("testdata")
data("cellcycle")

# オブジェクト化
testdata.obj <- as.ExpressionSet(testdata)

# Diffusion Mapを実行（第10主成分までを見る）
dif <- DiffusionMap(testdata.obj, n.eigs=10)

# 目視でどの主成分に分かれるのかを確認
pairs(eigenvectors(dif), col=cellcycle)

# FUCHIKOMA実行
result <- FKM(dif, DC=c(1,2))

# DEGs
head(result)

# データ保存
write.table(result)
```
