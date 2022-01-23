搜索常见指标

## Precision@K
+ 指检索得到的文档中相关文档所占的比例。
+ 公式 $ precision = \frac{|\{relevant\,documents \} \cap \{retrieved\,documents\}|}{|\{retrieved\,documents\}|}$
+ Precision@K 表示 $ |\{retrieved\,documents\}| $ = K

## Recall@K
+ 指所有相关文档被检索的比例
+ 公式 $ recall = \frac{|\{relevant\,documents \} \cap \{retrieved\,documents\}|}{|\{relevant\,documents\}|} $

## AUC/GAUC
+ AUC的物理意义为任取一对正例和负例，正例得分大于负例得分的概率
+ AUC的值与ROC（tpr-fpr）曲线下方面积相等

|  iterm | 意义  | 公式 |
|  ----  | ----  | ---- |
| tpr | True Postive Rate  | TP/(TP+FN) |
| fpr | False Postive Rate | FP/(FP+TN) |

+ GAUC先对搜索session内样本求AUC，然后对所有session求平均

## MAP（Mean Average Precision）
+ AP/AveP：同时考虑准确率和召回率，把准确率看成召回率的函数 precision = P(r)，来衡量随着召回率从0到1，准确率的变化情况。AveP 即对该函数进行积分，求 precision 的期望均值
+ $AveP =\int_{0}^{1} P(r) d r=\sum_{k=1}^{n} P(k) \Delta(k)=\frac{\sum_{k=1}^{n}(P(k) \times \operatorname{rel}(k))}{\text { number of relevant documents }}$
其中，rel(k) 表示第k个文档是否相关，若相关则为1，否则为0；P(k) 表示前k个文档的准确率，即precision@K。
+ 公式理解 $AveP =\frac{1}{R} \times \sum_{r=1}^{R} \frac{r}{\text { position }(r)}$ 其中，R 表示相关文档的总个数；position(r) 表示，结果列表从前往后看，第 r 个相关文档在列表中的位置。举例，有三个相关文档，位置分别为1、3、6，那么：
$AveP =\frac{1}{3} \times\left(\frac{1}{1}+\frac{2}{3}+\frac{3}{6}\right)$
+ MAP：对多个query的AveP求均值 $MAP=\frac{\sum_{q=1}^{Q} A v e P(q)}{Q}$

## NDCG (Normalize DCG)
+ 特点：支持对多级label（＞2）文档进行综合打分
+ 公式：DCG (Discounted cumulative gain) $\mathrm{DCG} @ k=\sum_{j=1}^{k} g\left(r_{j}\right) d(j)$  其中，gain函数一般取：$g\left(r_{j}\right)=2^{r_{j}}-1$ ，rj 为 label，discount 函数一般取：$d(j)=\frac{1}{\log _{2}(j+1)}$
+ 公式：$\mathrm{NDCG} @ k=\frac{1}{\operatorname{maxDCG} @ k} \mathrm{DCG} @ k$

## MRR (Mean reciprocal rank)
+ RR (reciprocal rank) 表示第一个相关文档排序位置的倒数。MRR即对多个query的RR求均值：$MRR=\frac{1}{|Q|} \sum_{i=1}^{|Q|} \frac{1}{\operatorname{rank}_{i}}$
+ 应用：常用于只要求一个最终结果的场景，如问答类检索


## ERR (Expected reciprocal rank)
+ 表示用户的需求被满足时停止的位置的倒数的期望
+ 公式：$E R R=\sum_{r=1}^{n} \varphi(r) P P_{r}=\sum_{r=1}^{n} \frac{1}{r} P P_{r}=\sum_{r=1}^{n} \frac{1}{r} \prod_{i=1}^{r-1}\left(1-R_{i}\right) R_{r}$ 其中，PPr 为用户在位置 r 停止的概率； φ(r) 指位置的倒数。$P P_{r}=\prod_{i=1}^{r-1}\left(1-R_{i}\right) R_{r}$ 其中，Ri是关于文档相关度 label 的函数，如可取： $R_{i}=R\left(g_{i}\right)=\frac{2^{g}-1}{2^{g_{\max }}}, g \in\left\{0,1, \ldots \cdots, g_{\max }\right\}$
+ 特点：*考虑了文档之间的相关性信息*，一个文档是否被用户点击和排在它前面的文档有很大的关系。














