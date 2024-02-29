# css面试题

文本溢出用什么隐藏

1. overflow:hidden.  文本元素 溢出

2. 单行文本溢出

   ```
   white-space: nowrap;  
   overflow: hidden;  
   text-overflow: ellipsis;
   ```

3. 行文本溢出

```
.multi-line-text {  
    display: -webkit-box;  
    -webkit-line-clamp: 3;  
    -webkit-box-orient: vertical;    
    overflow: hidden;  
}
```





