在TypeScript中，"?. "被称为可选链（Optional Chaining）。这个操作符允许你在尝试访问对象的属性时，如果对象为null或undefined，则返回undefined，而不是抛出错误。

具体来说，使用可选链时，你可以在属性名后面加上 "?. "。例如，如果 `obj` 为null或undefined，`obj?.prop`的值就会是undefined，而不会抛出异常。这个特性在处理可能为空或undefined的对象属性时非常有用，避免了在访问对象时出现空指针异常。

