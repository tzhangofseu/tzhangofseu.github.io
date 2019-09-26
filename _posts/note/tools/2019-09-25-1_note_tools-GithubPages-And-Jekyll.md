---
title: github pages + jekyll搭建与使用
published: true
---

# Jekyll中的Latex使用
## 支持编辑时Latex实时预览
1. 编辑器Atom中安装markdown-preview-plus，把自带的markdown-preview禁用掉。
2. 然后修改markdown-preview-plus的配置：
   + Enable Math Rendering By Default勾上
   + Keybindings的Enable勾上
3. 重启Atom编辑器，快捷键ctrl+shift+m可以在编辑页面右侧同步显示效果。

`注意：该插件与网上推荐的scroll插件有冲突，所以我没有安装scroll插件`
## 支持本地Jekyll服务和Github Pages远端服务的Latex显示
在html head标签中加入一段代码即可
```html
<script type="text/javascript" async
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```
## Jekyll中支持的常用Latex语法
1. 双\$ 公式内容 双\$  如果双\$两边有字，则居左，否则居中。或者
2. 双\$

   公式内容

   双\$

`注意：编辑预览与实际网页展示会有差异，比如 ‘\in’预览时不显示`$$ \in $$

可参考：

[Latex用法](https://www.jianshu.com/p/2fe00efe06a3)

[Latex中的希腊字母表示](https://blog.csdn.net/xxzhangx/article/details/52778539)
