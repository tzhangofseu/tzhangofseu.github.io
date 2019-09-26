---
title: The Learning Problem
published: true
---

# 本课故事主线：
+ 什么情况下可以机器学习（例子+技术）
+ 为什么机器可以学习（理论+例子）
+ 机器怎么学习（技术+实践）
+ 机器怎么样可以学的更好（实践+理论）

# 本节目录：
+ 课程介绍
+ 什么是机器学习
+ 机器学习的应用
+ 机器学习的组成
+ 机器学习和其他领域

# 什么是机器学习
学习vs机器学习
+ 学习：observations -> learning -> skill
+ 机器学习：data -> ML -> skill
+ skill: 改进性能（如预估准确度）
+ 机器学习的定义：从数据中计算出的经验改进性能。
+ 例：股票数据 -> ML -> 更多的投资回报

# 机器学习的应用
一些机器学习使用场景：
1. 人类无法人工设计程序（火星导航，未知领域，规则未知）
2. 人类无法定义出解决方案（语音/图像识别）
3. 人类无法做的快速决策（超短线交易）
4. 大规模的个人化场景（客户定向营销）

总结一下场景：
1. 存在潜在的模式
2. 无法程序化定义或者成本太高
3. 有数据

日常应用举例：
+ 衣：
   1. data: 销售数据 + 顾客调研
   2. skill：给客户时尚建议
+ 食：
   1. data：Twitter data（words + location）
   2. skill: 判断餐厅食物中毒的可能性
+ 住：
   1. data：一些房子的特性和耗能情况
   2. skill：预测房子的耗能情况
+ 行：
   1. data：交通标志的图片和含义
   2. skill：识别交通标志
+ 育：
   1. data：学生的测验记录
   2. kill：预测一个学生是否能做出一个题目，进一步预测题目的难易程度。
+ 娱：
   1. data：用户对一些电影的投票
   2. skill：预测一个用户对一个电影的评价
   3. （movie：若干标签。相应的给用户若干标签。计算内积）

# 机器学习的组成
以银行是否给客户发信用卡为例

基本符号
+ 输入：$$ {\it x} \in {\it X} $$ （客户）
+ 输出：$$ {\it y} \in {\it Y} $$ （是否发卡）
+ target function： $$ f: {\it X} \rightarrow {\it Y} $$
+ 数据：$$ {\it D} = \{({\it x}_1, {\it y}_1),({\it x}_2, {\it y}_2),...,({\it x}_N, {\it y}_N) \} $$
+ hypothesis： $$ g: {\it X} \rightarrow {\it Y} $$

$$ \{({\it x}_n, {\it y}_n)\}\ from\ f \rightarrow ML \rightarrow g $$

例如：$$ g \in H = \{h_k\} $$，发卡条件
+ 年薪 > ￥800,000
+ 负债 > ￥100,000
+ 工作时间 < 2年

hypothesis set $$ H $$:
+ 包含好/坏的hypothesis
+ 由算法$$ A $$找出最好的作为$$ g $$

Model = $$ A $$ + $$ H $$

机器学习：use data to compute hypothesis $$ g $$ that approximates target $$ f $$
