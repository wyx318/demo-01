# 如何在不刷新页面的情况下改变URL
## 主要有两种方式
#####第一种
* 改 window.location.hash  优点是：没有任何的BUG 
小栗子 ：
```
<button id="x">x</button>
<button id="y">y</button>
<div id="动态区域"></div>
<script>
  x.onclick = function () {
    // 动态区域.innerText = 'xxxxxxxxxxx'
    window.location.hash = 'x'
  }
  y.onclick = function () {
    window.location.hash = 'y'
  }
  // x.onclick = function () {
  //   // alert('1')
  //   window.location.hash = "wangyx"
  // }
  //点击当前按钮 动态展示当前hash及内容
  window.onhashchange = function () {
    var hash = window.location.hash
    展示内容(hash)
  }
//当hash为空的时候 默认展示 x的内容 当前连接 hash被复制也会展示当前内容 
  var hash = window.location.hash
  if (hash === '') {
    window.location.hash = 'x'
  } else {
    展示内容(hash)
  }

  function 展示内容(hash) {
    if (hash === '#x') {
      动态区域.innerText = 'xxxxxxxxxxx'
    } else if (hash === '#y') {
      动态区域.innerText = 'yyyyyyyyyyyy'
    }
  }
```
#####第二种
用 [window.history.pushState()](https://developer.mozilla.org/zh-CN/docs/Web/API/History_API#%E6%B7%BB%E5%8A%A0%E5%92%8C%E4%BF%AE%E6%94%B9%E5%8E%86%E5%8F%B2%E8%AE%B0%E5%BD%95%E4%B8%AD%E7%9A%84%E6%9D%A1%E7%9B%AE "null")
优点： 更优雅 。缺点：刷新就会 404  解决方式 ：让后端支持模糊匹配的路由 
小栗子 ：
```
<button id="x">x</button>
<button id="y">y</button>
<div id="动态区域"></div>
<script>
  x.onclick = function () {
    window.history.pushState('', 'x页面', '/URL-demo-2.html/x')
  }
  y.onclick = function () {
    window.history.pushState('', 'y页面', '/URL-demo-2.html/y')
  }
</script>
```
