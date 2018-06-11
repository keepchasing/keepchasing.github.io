---
layout:     post
title:      "js模板引擎之artTemplate"
subtitle:   " \"artTemplate简单应用\""
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





