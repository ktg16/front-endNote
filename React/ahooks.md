## ahooks 记录

### useSafeState(替代useState)

用法与 `React.useState` 完全一样，但是在组件卸载后异步回调内的 `setState` 不再执行，避免因组件卸载后更新状态而导致的内存泄漏。

useRequest

`useRequest` 是一个强大的异步数据管理的 Hooks，React 项目中的网络请求场景使用 `useRequest` 就够了。

https://ahooks.js.org/zh-CN/hooks/use-request/index