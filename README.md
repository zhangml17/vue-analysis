#Vue
## filter
Vue.js允许自定义过滤器，常用于一些常见的文本格式化
+ 过滤器可以用在两个地方：双括号插值和v-bind表达式
+ 当全局过滤器和局部过滤器重名时，会采用局部过滤器
+ vue2.x移除了双向过滤器
## 自定义指令
除了核心功能默认内置的指令 (v-model 和 v-show)，Vue 也允许注册自定义指令。注意，在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令
+ 注册全局自定义指令
```
Vue.directive('focus', {
    inserted(el) {
        // 聚焦元素
        el.focus()
    }
})
```
+ 注册局部自定义指令(directives选项)
```
directives:{
    focus:{
        inserted(el) {
            // 聚焦元素
            el.focus()
        }
    }
}
```
### 钩子函数
一个自定义对象可以提供的钩子函数(均为可选)
+ bind: 只调用一次，指令第一次绑定到元素时调用(在这里可以进行一次性的初始化设置)
+ inserted: 被绑定元素插入父节点时调用(仅保证父节点存在，但不一定已被插入文档中)
+ update: 所在组件的VNode更新时调用
+ componentUpdated: 指定所在组件的VNode及其子VNode全部更新后调用
+ unbind: 只调用一次，指定与元素解绑时调用
### 钩子函数参数
+ el: 指令所绑定的元素，可以用来直接操作DOM
+ binding: 一个对象，包括如下属性：
```
name: 指令名，不包括 v- 前缀
value: 指令的绑定值
oldValue: 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
expression: 字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
arg: 传给指令的参数，可选，例如 v-my-directive:foo 中，参数为 "foo"。
modifiers: 一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
```
+ vnode: Vue编译生成的虚拟节点
+ oldVnode: 上一个虚拟节点
除了el之外，其他参数都应该是只读的，切勿修改。