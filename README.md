# Paging solution

> 分页生成解决方案

## 编程语言版本实现



> 分页生成解决方案 Paging solution

## 编程语言版本实现

- [JavaScript](https://github.com/onface/paging-js)
- ~~[PHP](https://github.com/onface/paging-php)(未实现)~~
- ~~[JAVA](https://github.com/onface/paging-java)(未实现)~~
- ~~[Go](https://github.com/onface/paging-go)(未实现)~~
- ~~[C](https://github.com/onface/paging-c)(未实现)~~
- ~~[C++](https://github.com/onface/paging-cpp)(未实现)~~

## 前端框架实现版本

- [paging.react](https://github.com/onface/paging.react)
- ~~[vue-paging](https://github.com/onface/paging.vue)(未实现)~~
- ~~[ng-paging](https://github.com/onface/paging.ng)(未实现)~~

## 多语言实现原理

分页生成在 Web 开发中非常常见，市面上也存在很多用于生成分页的分页函数。但都难以做到**完全自定义界面**。

> 这里的完全自定义界面指的是分页生成的 HTML 不限制为 `<li class="paging-item">` 或 `<a class="paging-item">` 

Paging 提供了一套基于模板渲染的分页生成方案，不限编程语言不限模板引擎类型。基于模板引擎实现的分页可以做到 **完全自定义界面**

### createData

正常一个分页需要如下基础数据：


1. `page` `9` 当前页码 **(必须)** 
2. `pageCount` `20` 总页数 **(必须存在 `pageCount` 或者存在 `pageSize` 和 `dataTotal`)** 
3. `pageSize` `10` 每页显示数据数 **(没有 pageCount 时候必须存在此数据)** 
4. `dataTotal` `200` 总数据量 **(没有 pageCount 时候必须存在此数据)** 
5. `prevBatch` `3` 显示`page`前多少页 
6. `nextBatch` `3` 显示`page`后多少页 
7. `prevSomePage` `5` 显示 `page` 前指定页 
7. `nextSomePage` `5` 显示 `page` 后指定页


```js
// {Bolean} 存在分页
hasPaging

// {Number} 20 总页数 
pageCount

// {Number} 200 总数据量 
dataTotal

// {Number} 9 当前页 
page

// {Boolean} false 当前页是第一页 
isFirstPage

// {Boolean} false 当前页是最后一页
isLastPage

// {Array,Boolean} [6,7,8] [] 当前页前几页不存在前几页则为 [] (根据 传入的 prevPages 扩展)
prevBatch

// {Array,Boolean} [10,11,12] [] 当前页后几页  不存在后几页则为 [] (根据 传入的 prevPages 扩展)
nextBatch

// {Number} 8 上一页 
prevPage

// {Number} 10 下一页 
nextPage

// {Boolean} true 除了 prevBatch 和 第一页还存在其他页
prevHasMorePage 

// {Boolean} true除了 nextBatch 和 最后一页还存在其他页
nextHasMorePage

// {Number|Boolean} 4 当前页前 5 页 (根据 传入的 prevSomePage 决定是前几页)
prevSomePage

// {Number|Boolean} 14 当前页后 5 页 (根据 传入的 nextSomePage 决定是前几页)
nextSomePage
// {Number} 每页显示多少条数据
pageSize
```

再根据上面的数据与模板引擎结合，渲染 HTML。最终配合样式 [onface/design/paging](https://github.com/onface/design/tree/master/components/paging) 实现完全自定义界面

createData 实现方法可参考 [paging.js createData](https://github.com/onface/paging-js/blob/master/lib/createData.js)
