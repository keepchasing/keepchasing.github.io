---
layout:     post
title:      "js模板引擎之artTemplate"
subtitle:   "artTemplate简单应用"
date:       2017-11-24 12:00:00
author:     "the Little Prince"
header-img: "img/post-bg.jpg"
catalog: true
navbarClass: ""
tags:
    - js
---

### html文件中

```
  <script src="./template.min.js" type="text/javascript" ></script>
    <div  id="listWrap">
    <script type="text/html" id="j-list-template">
      {{if listArr.length}}
        <ul>
          {{each listArr as person}}
            <li>{{person.name}}今年{{changeAge(person.age)}}了
          {{/each}}
        </ul>
      {{/if}}
    </script>
    </div>

```

### js文件中

```
  // template.helper自定义过滤器
  template.helper('changeAge', function(age){
    return ++age;
  });
  let oParent = document.querySelector('#listWrap')
  let listArr = [
    {name:'Joe',age:'9'},
    {name:'Nate',age:'2'},
    {name:'Chuck',age:'7'}
  ]
 $('.j-m-question').html(template('j-list-template"',{'questionArr':questionArr})); //向id为j-list-template的模板传入数据

```

### 模板是一个独立的文件（list-template.html）

```
<script>
let listArr = [
  {name:'Joe',age:'9'},
  {name:'Nate',age:'2'},
  {name:'Chuck',age:'7'}
]
// 利用ajax的get方法获取模板页
var html=$.get('list-template.html',function (data) {
  // 利用template.compile()获取渲染内容
  var render = template.compile(data);
  // 将数据listArr渲染进去
  var str = render(listArr);
  // 将内容添加到页面
  document.getElementById('content').innerHTML = str;
})
</script>

```





