---
title: 文本超出隐藏
date: 2018-03-29
tags:
---

# 文本超出隐藏（...）

## html结构
```
//基础css
.item{
    width: 300px;
    background-color: #eee;
    margin-bottom: 20px;
}

//html
<div class="item single">
    单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试单行文本测试
</div>
<div class="item single">
    English test English test English test English test English test English test English test English test English test 
</div>

<div class="item many">
    English test English test English test English test English test English test English test English test English test 
</div>
<div class="item many">
   多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试多行文本测试
</div>
```


##  单行文本超出隐藏

```
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

##  多行文本超出隐藏

```
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 2;
overflow: hidden;
//这里是对英文换行处理
word-warp:break-word;
word-break:break-all;
```

### 注释
> word-wrap是控制换行的。 使用break-word时，是将强制换行。中文没有任何问题，英文语句也没问题。但是对于长串的英文，就不起作用
> break-word是控制是否断词的。 normal是默认情况，英文单词不被拆开。 break-all，是断开单词。在单词到边界时，下个字母自动到下一行。主要解决了长串英文的问题。


[查看代码](https://github.com/Alley23/web_list_demo/blob/master/CSS/%E6%96%87%E6%9C%AC%E8%B6%85%E5%87%BA%E9%9A%90%E8%97%8F.html)


[查看更多文章](https://alley23.github.io/)
