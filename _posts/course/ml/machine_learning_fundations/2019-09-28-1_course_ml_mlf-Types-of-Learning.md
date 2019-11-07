---
title: Types of Learning
published: true
---

# 本节目录
+ 从输出空间$$ y $$的角度
+ 数据Label $$y_n$$
+ 协议 $$ f \Rightarrow (x_n, y_n) $$
+ 输入空间$$ X $$


# 从输出空间$$ y $$的角度
+ 分类
   + 二分类 $$ y = {+1, -1}$$
   + 多分类（硬币分类）$$ y = {1c, 5c, 10c, 25c...} $$
+ 回归
   + 回归 $$ y = \mathbb{R} $$
   + 有范围的回归 $$ y = [lower, upper] \subset \mathbb{R} $$ 如：股票价格，温度等
+ 结构学习 $$ y = $$ structures。语句词性 $$ y = {PVN, PVP, NVN, PV,...}$$，蛋白质结构，speech parse tree等

# 数据Label $$y_n$$
+ 监督学习。分类
+ 非监督学习。
   + 聚类：文章分主题；顾客分群
   + 密度估计（非监督bounded regression）：交通报告 生成危险区域
   + 异常检测（非监督的二元分类）：互利网日志生成的入侵报警
+ 半监督学习（主要用于减少高成本的标记）
   + 少量标记的面部图片 进行脸部识别
   + 部分药效标识 进行药效预测
+ 强化学习
   + 输出用奖励和惩罚的方式给
   + 用户对广告的点击
   + 牌类决策 赢得数量
   + 通过部分或者隐式的信息来学习，通常是序列式的。

顾客的特征：$$ x = ({\it x}_1,{\it x}_2,...,{\it x}_d,) $$

目标：$$ y = \{+1(good), -1(bad)\} $$

线性$$ h \in H $$的公式化描述：

$$ h(x) = sign((\sum_{i=1}^{n} w_{i}x_{i}) - threshold)$$

公式可以进化为

$$ h(x) = sign(\sum_{i=0}^{n} w_{i}x_{i})$$

向量化：

$$ h(x) = sign({\it W}^{\it T}{\it X})$$

在 $$ R_2 $$ 上的PLA求法示意

$$ h(x) = sign(w_0 + w_1 x_1 + w_2 x_2)$$

# PLA算法

+ 要求：从$$ H $$中选出$$ g = f $$
+ 退一步目标：在D上$$ g \approx f $$，理想情况 $$ g(x) = f(x) = y_n $$
+ 难点：$$ H $$集合无限大
+ 方法：从某个$$ g_0 $$出发，在D上逐渐修正。（后面$$ W_0 $$代表$$ g_0 $$）

算法描述
+ For t = 0,1,2,...
   1. 找到让$$ W_t $$犯错误的样本($$ X_{n(t)}, y_{n(t)} $$)，即：$$ sign(W_t^T X_{n(t)}) \neq y_{n(t)} $$


   2. 对错误之处尝试纠正
      + 若$$ y_{n(t)} = +1 $$，则$$ W_t^T,X_{n(t)} $$夹角>90，需缩小：$$ W_{(t+1)} \leftarrow W_t + X_{n(t)} $$
      + 若$$ y_{n(t)} = -1 $$，则$$ W_t^T,X_{n(t)} $$夹角<90，需扩大：$$ W_{(t+1)} \leftarrow W_t - X_{n(t)} $$
      + 综上，纠正公式为$$ W_{(t+1)} \leftarrow W_t + y_{n(t)} X_{n(t)} $$
+ 直到没错误
+ return 最后一次的$$ W $$

# PLA一定能找到答案吗
+ 假设：数据线性可分 $$ \Leftrightarrow $$ 存在$$ W_f $$使得所有$$ y_n = sign(W_f^T X_n) $$
+ 需要证明$$ W_t $$和$$ W_f $$越来越接近，两个角度
   + 内积越来越大
   + $$ W_t $$模长增长有限
+ 证明内积越来越大：
   $$ y_{n(t)} W_f^T X_{n(t)} \ge \min \limits_n y_n W_f^T X_n > 0$$
   + 用任一样本$$ (X_{n(t)}, y_{n(t)})$$进行更新：

$$
\begin{align*}
W_f^T W_{t+1} &= W_f^T (W_t + y_{n(t)} X_{n(t)}) \\
&\ge W_f^T W_t + \min \limits_n y_n W_f^T X_n \\
&> W_f^T W_t
\end{align*}
$$

+ 证明模长增长速度有限
   + $$ W_t $$只在出错时修正 $$ \Leftrightarrow sign(W_t^T X_{n(t)}) \ne y_{n(t)} \Leftrightarrow y_{n(t)} W_t^T X_{n(t)} \le 0 $$
$$
\begin{align*}
 \Arrowvert W_{t+1} \Arrowvert ^2 &= \Arrowvert W_t + y_{n(t)} X_{n(t)} \Arrowvert ^2 \\
 &= \Arrowvert W_t \Arrowvert ^2 + 2 y_{n(t)} W_t^T X_{n(t)} + \Arrowvert y_{n(t)} X_{n(t)} \Arrowvert ^2 \\
 &\le \Arrowvert W_t \Arrowvert ^2 + \Arrowvert y_{n(t)} X_{n(t)} \Arrowvert ^2 \\
 &\le \Arrowvert W_t \Arrowvert ^2 + \max \limits_n \Arrowvert X_n \Arrowvert ^2
 \end{align*}
 $$

 + 待证明：
    + $$ W_0 = 0 $$，T次纠正后

$$ \frac{W_f^T}{\Arrowvert W_f \Arrowvert} \frac{W_T}{\Arrowvert W_T \Arrowvert} \ge \sqrt{T} . constant $$

   + 所以趋势在增长，然而最大不超过1，所以一定会停下来


# 线性不可分数据如何求解
$$ f $$ 生成D的过程中会有噪音

+ 找犯错误最少的$$ W $$ (NP hard问题)

$$ W_g \leftarrow \arg\min \limits_W \sum_{n=1}^{N} \lgroup \lgroup y_{n} \ne sign(W^T X_n) \rgroup \rgroup $$
+ 改进：口袋算法（Pocket Algorithm）
   + 手持$$ \hat{W} $$
   + For t = 0,1,2,...
      1. 找到让$$ W_t $$犯错误的样本($$ X_{n(t)}, y_{n(t)} $$)
      2. 对错误之处尝试纠正
      $$ W_{(t+1)} \leftarrow W_t + y_{n(t)} X_{n(t)} $$
      3. 如果$$ W_{(t+1)} $$犯错比$$ \hat{W} $$少，则赋值给$$ \hat{W} $$ （效率低）
   + 直到足够多的轮数
   + return $$ \hat{W} $$ as $$ g $$
