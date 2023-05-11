vuex直接修改state是否可以？为什么

#### 一. 使用vuex修改state时，有两种方式：

1.可以直接使用 this.$store.state.变量 = xxx;

2.this.$store.dispatch(actionType, payload) 

  或者： this.$store.commit(commitType, payload)

使用dispatch 和 commit的区别在于，前者是异步操作，后者是同步操作，所以 一般情况下，推荐直接使用commit，
 即 this.$store.commit(commitType, payload)，以防异步操作会带来的延迟问题。

#### 二. 异同点

1.共同点： 能够修改state里的变量，并且是响应式的（能触发视图更新）

2.不同点：

   若将vue创建 store 的时候传入 strict: true, 开启严格模式，那么任何修改state的操作，只要不经过

   mutation的函数，vue就会 throw error :  [vuex] Do not mutate vuex store state outside mutation handlers。

#### 三.使用commit提交到mutation修改state的优点：

   vuex能够记录每一次state的变化记录，保存状态快照，实现时间漫游／回滚之类的操作。
   （实际本人未用到，暂时未遇到使用该特性的需求）



 结论： 官方推荐最好设置严格模式，并且每次都要commit来修改state，而不能直接修改state，以便于调试等。