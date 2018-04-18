```javascript
/*
 * 归纳 react 和 vue的异同点
 * 背景: 友云设采用react全家桶，微信采用vue基础部分，对于react和vue都有一个大致的掌握，这里总结一下，做个区分
 * time: 2018.4.12
 */
```

## 数据流

默认情况下，react采用单向数据流，修改state只能通过 `setState()` 方法操作

默认情况下，vue采用双向数据绑定，可以直接修改state `this.data = newData`

> 注意: 在2者封装组件时，因为传递的props都是只读的，不允许直接修改，但是react可以直接在 `jsx` 中使用 pops，但是vue在使用的时候要注意，不能将 props 通过 `v-modal` 方式绑定到组件上，因为这样会直接修改 props， 从而系统报错

## 组件

### 构建方式

react: 无状态组件可以直接导出一个函数，有状态组件则要通过 `extends React.Component` 方式实现

vue: 导出一个对象，对象格式固定，通常包含 name、components、data、methods等

### 组件格式

**react** 

(有状态组件)

类似java, 采用es6 关键字 `class`, 使用jsx(默认jsx, 当然也可以使用其他的)

```javascript
class Filter extends React.Component {
	constructor(props) {
        super(props)
    }
    componentDidMount() {}
	render(){
		return ()
	}
}

Filter.propTypes = {}
Filter.defaultProps = {}

export default Filter
```

**vue**

独特格式，指定输出对象格式

```javascript
<template></template>

<script>
export default {
  name: 'TaskList',
  components: {},
  mixins: [],
  data () {
    return {}
  },
  methods: {},
  watch: {},
  mounted: function () {}
}
</script>

<style></style>

```

### 生命周期

**react**

装配

1. constructor()
2. componentWillMount()
3. componentDidMount()

更新

4. componentWillReceiveProps()
5. shouldComponentUpdate()
6. componentWillUpdate()
7. getSnapshotBeforeUpdate()
8. componentDidUpdate()

卸载

9. componentWillUnmount()

错误处理

10. componentDidCatch()

**vue**

1. beforeCreate()
2. created()
3. beforeMount()
4. mounted()
5. beforeUpdate()
6. updated()
7. beforeDestroy()
8. destroyed()

## 虚拟dom

## 事件

2者都是绑定在虚拟dom上的，当虚拟dom组件被销毁，那么事件也取消

## 特性

### react

### vue 

1. mixin
2. 指令：v-if、v-modal等
3. computed
4. watch
5. slot内容分发

## 其他小点

1. vue-class react-className
2. 