title: markdown文档中mathjax的问题
date: 2016-01-29 00:03:10
categories: "Markdown"
tags:
  - Markdown
  - MathJax
---

在写markdown文档时经常会需要插入数学公式，我之前只会使用图片插入，上次在看到mathjax后，我开始了使用mathjax的历程，但在实际写文档的过程中遇到了一些问题。

<!--more-->

# 关于有一些公式无法正确的显示

在写机器学习的文章中遇到的一个关于范数的公式写出来编辑器上显示没有问题，但是一旦放进文档里就不行了，这个问题困扰了我很长时间。

这是代码：
```
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_{i=1}^n\mid p_i-q_i\mid ^k\right)^\frac{1}{k} $$
```

这是效果：
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_{i=1}^n\mid p_i-q_i\mid ^k\right)^\frac{1}{k} $$

这里haroopad显示的公式是正确的，但是hexo编译过后的网页显示就不对了。

把代码剪裁一下，看看什么样子的公式是可以的：
```
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_i \right) $$
```

效果：
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_i \right) $$

这个好像就可以，但是貌似sum后面的i一旦加上花括号就不行：
```
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_{i} \right) $$
```

效果：
 > 严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义
 > $$ \lim_{k\to\infty}\left( \sum_{i} \right) $$

于是我点开了两个网页的源代码，定位到这一行：
```html
<p>严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义<br>$$ \lim<em>{k\to\infty}\left( \sum</em>{i} \right) $$</p>
```

```html
<p>严格意义上讲，Minkowski Distance 不是一种距离，而是一组距离的定义<br>$$ \lim_{k\to\infty}\left( \sum_i \right) $$</p>
```

可以发现最明显的不同就算lim后面的 ``<em>``，这时我们注意到，hexo在编译的时候将lim和sum后面的下划线 \_翻译成强调的 ``<em>`` 了，仔细观察前面的公式，确实可以发现一部分变成了斜体。所以我们要在所有的下划线 \_ 前面加上 \\ 转义就可以了。

**OK，搞定**

*** p.s 我的chrome上显示的公式后面都有一个竖线，firefox没有，内啥，一般平时用chrome习惯，所以有人知道怎么弄咩？ ***

*** 上面的问题在重新配置Hexo之后就没有了，个人觉得应该是版本的问题？ ***