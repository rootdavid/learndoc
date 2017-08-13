## JQuery技术内幕读书笔记
### 为什么使用自执行匿名函数，以及好处？
* 防止其他框架或代码污染JQuery，造成代码冲突
* 自执行匿名函数写法
```
    // 写法 1（常见写法，也是 jQuery 所采用的）
    ( function() {
    // ...
    } )();
    // 写法 2
    ( function() {
    // ...
    }() );
    // 写法 3
    !function() {
    // ...
    }();

```
* 什么要为自调用匿名函数设置参数 undefined ？
    * 因为<strong>undefined</strong>关键字在有的浏览器是可更改的，为了防止在jQuery核心代码里面有冲突
* jQuery 自初始化工厂函数
```
(function(window, undefined){
    var jQuery = (function(selector, context) {
        return new jQuery.fn.init(seleter, context, rootjQuery)
    })();

    return jQuery;

    //核心代码...

    window.jQuery = window.$ = jQuery;
})(window)

```