##惰性载入函数
    function method() {
        if (xxx) {
            method = function () {};
        }
        else {
            method = function () { console.log('other'); }
        }
    
        return method();
    }

##防篡改
###不可扩展
`Object.preventExtensions(obj)` 不可继续给 `Obj` 增加属性了
`Object.isExtensible(obj)` 是否可以扩展
###密封对象
`Object.seal(obj)` `obj` 不可扩展，且已有属性不可删除
`Object.isSeal(obj)`
###冻结对象
`Object.freeze(obj)` 不可扩展，不可删除属性，不可改没有 set 函数的字段
`Object.isFrozen(obj)`

####高效的 JavaScript 
HTMLCollection 存取都相当耗时，应该复制到数组里再处理
大量的字符串拼接可以用 `Array.prototype.join`

