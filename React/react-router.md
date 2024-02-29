# [***React-router框架***](https://react.docschina.org/)

react- router有两种使用方式：基础写法和依赖写法（个人的分类）

## 1.基础写法及各属性的使用

```react
<Routes>
  <Route path="/" element={<App />}>
    <Route path="expenses" element={<Expenses />} />  // 嵌套路由
      <Route path="invoices" element={<Invoices />} >
      	<Route path=":invoiceId" element={<Invoice />}></Route> //再次嵌套路由（动态的子路由,使用这种方法可以获取url参数）
      </Route>
    <Route   // 类似vue中redirect 重定向  如果访问router path为' ' 就直接去<main></main>
      path="*"
      element={
        <main style={{ padding: "1rem" }}>
          <p>There's nothing here!</p>
        </main>
      }
    />
  </Route>
</Routes>
```

### 读取url参数

```react
//<Invoices />页
import { useParams } from "react-router-dom";

export default function Invoice() {
  let params = useParams();
  return <h2>Invoice: {params.invoiceId}</h2>;
}
```

### Index Routes 索引路由

```react
<Routes>
  <Route path="/" element={<App />}>
    <Route path="expenses" element={<Expenses />} />
    <Route path="invoices" element={<Invoices />}>
      <Route
        index   // 索引路由
        element={
          <main style={{ padding: "1rem" }}>
            <p>Select an invoice</p>
          </main>
        }
      />
      <Route path=":invoiceId" element={<Invoice />} />
    </Route>
    <Route
      path="*"
      element={
        <main style={{ padding: "1rem" }}>
          <p>There's nothing here!</p>
        </main>
      }
    />
  </Route>
</Routes>
```

什么是索引路由？

- 索引路由在父路由路径的父路由出口中呈现。
- 当父路由匹配但其他子路由都不匹配时，索引路由匹配。
- 索引路由是父路由的默认子路由。
- 当用户尚未单击导航列表中的一项时，会呈现索引路由。

### NavLink  （Active Link）

```react
<NavLink className={({isActive})=>({
        return {isActive?"red":"blue"}
        to={'/expenss'}                           
    })}></NavLink>
```

### Search Params (搜索参数)

https://reactrouter.com/docs/en/v6/getting-started/tutorial#search-params

通过filter搜索参数找到我们想要的router

做全局查询使用

### 自定义行为

```react
import { useLocation, NavLink } from "react-router-dom";

function QueryNavLink({ to, ...props }) {
  let location = useLocation();
  return <NavLink to={to + location.search} {...props} />;
}

```

使用 useLocation 将搜索的信息记录下来

### 编程方式导航

使用 useNavigate

```react
import {
  useParams,
  useNavigate,
  useLocation,
} from "react-router-dom";

 let navigate = useNavigate();
<button onClick={()=>{navigate('/invoices')}}></button>
```

路由器：BrowserRouter 与 HashRouter区别

### Link

```react
<Link to={'/index'}></Link> 
```

to的用法与 cd 类似

### NavLink

```react
<NavLink style={({isActive})=>(isActive ? activeStyle : undefind))}></NavLink>
```

### 路由跳转

1.使用组件进行跳转

```
// 页面跳转
<Link to="/otherPage">跳转到其他页面</Link>
```

```
//组件重定向
import { Redirect } from 'react-router-dom';
// 重定向跳转
<Redirect to="/otherPage" />
```

```
import { useHistory } from 'react-router-dom';

function MyComponent() {
  const history = useHistory();

  // 页面跳转
  history.push('/otherPage');

  // 重定向跳转
  history.replace('/otherPage');
}
//导航跳转
```

