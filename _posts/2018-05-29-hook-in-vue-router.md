---
layout:     post
title:      "vue-router 的钩子函数"
subtitle:   ""
date:       2018-05-29 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - vue
---

### 完整的导航解析流程

1.  导航被触发。
1.  在失活的组件里调用离开守卫。
1.  调用全局的 beforeEach 守卫。
1.  在重用的组件里调用 beforeRouteUpdate 守卫 (2.2+)。
1.  在路由配置里调用 beforeEnter。
1.  解析异步路由组件。
1.  在被激活的组件里调用 beforeRouteEnter。
1.  调用全局的 beforeResolve 守卫 (2.5+)。
1.  导航被确认。
1.  调用全局的 afterEach 钩子。
1.  触发 DOM 更新。
1.  用创建好的实例调用 beforeRouteEnter 守卫中传给 next 的回调函数。


#### 全局钩子

1.  beforeEach
1.  afterEach
1.  beforeResolve (2.5+)。

#### 路由独享钩子

1.  beforeEnter
1.  beforeLeave

#### 组件内钩子

1.  beforeRouteEnter
1.  beforeRouteUpdate (2.2+)
1.  beforeRouteLeave