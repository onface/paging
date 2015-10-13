# paging.github.io
分页生成解决方案

## 已实现语言版本

[JavaScript](https://github.com/nimojs/paging)

## 多语言实现原理

分页生成在 Web 开发中非常常见，市面上也存在很多用于生成分页的分页函数。但都难以做到**完全自定义界面**。

> 这里的完全自定义界面指的是分页生成的 HTML 不限制为 `<li class="paging">` 或 `<a class="paging">` 

Paging 提供了一套基于模板引擎的分页生成方案，不限编程语言不限模板引擎类型。基于模板引擎实现的分页可以做到 **完全自定义界面**

### createData

生成一个分页在数据层面只需要 2 个数据：当前页和总页数。根据这2个参数我们能扩展出如下数据：

```js
// {Bolean} 存在分页
_hasPaging
// {Number} 总页数 10
_pageCount
// {Number} 当前页 5
_currentPage
// {Boolean} 当前页是第一页
_isFirstPage
// {Boolean} 当前页是最后一页
_isLastPage
// {Array} 当前页前几页 [2,3,4] 
_beforePages
// {Boolean} 是否存在前几页
_hasBeforePages
// {Array} 当前页后几页 [6,7,8]
_afterPages
// {Boolean} 是否存在后几页
_hasAfterPages
// {Number|false} 上一页 4
_prevPage
// {Number|false} 下一页 6
_nextPage
// {String}链接前缀替换字符
_link
```

再根据上面的数据与模板引擎结合，渲染 HTML
以 [Mustache](http://mustache.github.io/) 为例
```html
{{#_hasPaging}}
    <div class="ui-paging">
        <{{#_prevPage}}a{{/_prevPage}}{{^_prevPage}}span{{/_prevPage}} class="ui-paging-prev" href="{{_link}}{{_prevPage}}">
            <
        </{{#_prevPage}}a{{/_prevPage}}{{^_prevPage}}span{{/_prevPage}}>
        {{^_isFirstPage}}
        <a href="{{_link}}1" class="ui-paging-item">1</a>
        {{/_isFirstPage}}
        {{#_hasBeforePages}}
        <span class="ui-paging-ellipsis">...</span>
        {{/_hasBeforePages}}
        {{#_beforePages}}
        <a class="ui-paging-item" href="{{_link}}{{.}}">{{.}}</a>
        {{/_beforePages}}
        <a href="{{_link}}{{_currentPage}}" class="ui-paging-item ui-paging-current">{{_currentPage}}</a>
        {{#_afterPages}}
        <a class="ui-paging-item" href="{{_link}}{{.}}">{{.}}</a>
        {{/_afterPages}}
        {{#_hasAfterPages}}
        <span class="ui-paging-ellipsis">...</span>
        {{/_hasAfterPages}}
        {{^_isLastPage}}
        <a href="{{_link}}{{_pageCount}}" class="ui-paging-item">{{_pageCount}}</a>
        {{/_isLastPage}}
        <{{#_nextPage}}a{{/_nextPage}}{{^_nextPage}}span{{/_nextPage}} class="ui-paging-next" href="{{_link}}{{_nextPage}}">
            >
        </{{#_nextPage}}a{{/_nextPage}}{{^_nextPage}}span{{/_nextPage}}>
        <span class="ui-paging-info"><span class="ui-paging-bold">{{_currentPage}}/{{_pageCount}}</span>页</span>
        <span class="ui-paging-which"><input value="{{_currentPage}}" type="text"></span>
        <a class="ui-paging-info ui-paging-goto" href="{{_link}}{{_currentPage}}" >Go</a>
    </div>
{{/_hasPaging}}
```

createDate 实现方法可参考 [paging.js createDate](https://github.com/nimojs/paging/blob/master/paging.js#L36-L190)
