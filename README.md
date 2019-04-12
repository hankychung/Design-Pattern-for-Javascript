# 单例模式 - Singleton Pattern
## 定义
保证一个类仅有一个实例，并提供访问此实例的全局访问点。
## 实现
```
class Singleton {
    constructor(tip) {
        this.tip = tip
    }
    getTip() {
        console.log(this.tip)
    }
    static getIns = (() => {
        let instance = null
        return () => {
            if (!instance) instance = new Singleton('单例设计模式：此类仅有一个实例对象')
            return instance
        }
    })()    
}

let a = Singleton.getIns()
let b = Singleton.getIns()

console.dir(a) // Singleton的实例对象
console.log(a === b) // true
```
## 应用
> 某厂面试题：实现Storage，使得该对象为单例，并对localStorage进行封装设置值setItem(key,value)和getItem(key)

es5的实现方法
```
function Storage(tip) {
    this.tip = tip
}

Storage.prototype.setItem = function(key, val) {
    window.localStorage.setItem(key, val)
}
Storage.prototype.getItem = function(key) {
    return window.localStorage.getItem(key)
}

Storage.getIns = (function() {
    let instance = null
    return function() {
        if (!instance) instance = new Storage('单例设计模式实现localstorage')
        return instance
    }
})()

let storage1 = Storage.getIns(),
storage2 = Storage.getIns()

storage1.setItem('hello', 'world')
console.log(storage2.getItem('hello')) // world
console.log(storage1 === storage2) // true
```



