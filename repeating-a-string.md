# 重复字符串

## 问题

你想重复一个字符串。

## 解决方案

创建一个包含 n+1 个空元素的数组，然后用要重复的字符串作为连接字符将数组元素拼接到一起：

```
# 创建包含10个foo的字符串
Array(11).join 'foo'

# => "foofoofoofoofoofoofoofoofoofoo"
```

## 为字符串重复方法

你也可以在字符串的原型中为其创建方法。它十分简单：

```
# 为所有的字符串添加重复方法，这会重复返回 n 次字符串
String::repeat = (n) -> Array(n+1).join(this)
```

## 讨论

JavaScript 缺少字符串重复函数，CoffeeScript 也没有提供。虽然在这里也可以使用列表推导（ comprehensions ），但对于简单的字符串重复来说，还是像这样先构建一个包含 n+1 个空元素的数组，然后再把它拼接起来更方便。
