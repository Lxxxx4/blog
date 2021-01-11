#### vue版本2.6.11

#### 入口文件

###### **complier/index**
- 初始化全局API（initGlobalAPI）
- 挂载isServer
- 挂载ssrContext
- 挂载FunctionalRenderContext

```JS
initGlobalAPI的内容：
挂载默认配置，util，nexttick，observable，初始化option

```
###### vue构造函数
```js
_init(option)
绑定uid(唯一标志vue实例)
合并默认配置项并挂载到$options
初始化生命周期initLifecycle
初始化事件机制initEvents
初始化渲染initRender
执行beforeCreate
执行created
初始化data/props （initState）
挂载vue实例（$mount）
```

###### 初始化生命周期initLifecycle

- 在当前vue实例的父vue实例的$children下 **push** 当前vue实例
- 初始一些属性

###### 初始化事件机制initEvents

###### 初始化渲染initRender
- 初始化虚拟dom(_vnode)
- 