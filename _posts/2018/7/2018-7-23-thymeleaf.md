---
layout:     post
title:      thymeleaf 常用标签的使用方法
subtitle:   thymeleaf
date:       2018-7-23
author:     Peng
header-img: img/post-bg-2015.jpg
keywords_post:  "模板,thymeleaf,springboot,spring"
catalog: true
tags:
    - springboot
---

#### 一.基本使用方式

后端代码：
```
    @RequestMapping("test")
    public String test(ModelMap map) {
        
        User u = new User();
        u.setName("superadmin");
        u.setAge(10);
        u.setPassword("123465");
        u.setBirthday(new Date());
        u.setDesc("<font color='green'><b>hello imooc</b></font>");
        
        map.addAttribute("user", u);
        
        User u1 = new User();
        u1.setAge(19);
        u1.setName("imooc");
        u1.setPassword("123456");
        u1.setBirthday(new Date());
        
        User u2 = new User();
        u2.setAge(17);
        u2.setName("LeeCX");
        u2.setPassword("123456");
        u2.setBirthday(new Date());
        
        List<User> userList = new ArrayList<>();
        userList.add(u);
        userList.add(u1);
        userList.add(u2);
        
        map.addAttribute("userList", userList);
        
        return "thymeleaf/test";
    }
```

前端代码：
```
用户姓名:<input th:id="${user.name}" th:name="${user.name}" th:value="${user.name}"/>
//转换生日格式
用户生日：<input th:value="${#dates.format(user.birthday,'yyyy-MM-dd')}"/>
```

#### 二.对象引用方式
```
<div th:object="${user}">
    用户姓名：<input th:id="*{name}" th:name="*name" th:value="*{name}"/>
    用户生日：<input th:value="*${#dates.format(birthday,'yyyy-MM-dd hh:mm:ss')}"/>
</div>
```
#### 三.渲染form表单
```
//field等于说自动解析这串代码的id，name等等属性
<form th:action="@{/th/postform}" th:object="${user}" method="post" th:method="post">
    <input type="text" th:field="*{name}"/>
    <input type="text" th:field="*{age}"/>
    <input type="submit"/>
</form>
```


```
    @PostMapping("postform")
    public String postform(User u) {
        
        System.out.println("姓名：" + u.getName());
        System.out.println("年龄：" + u.getAge());
        
        return "redirect:/th/test";
    }
```


#### 四.text与utext
后端代码：
```
@RequestMapping("test")
public String test(ModelMap map){
    User u = new User();
    u.setName("LeeCX");
    u.setAge(18);
    u.setPassword("123456");
    u.setBirthday(new Date());
    u.setDesc("<font color='green'><b>hello</b></font>");
    map.addAttribute("user",u);
    return "thymeleaf/test"
}
```
前端代码：
```
<span th:text="${user.desc}">abc</span>
<span th:utext="${user.desc}">abc</span>
```
#### 五.URL
```
<a th:href="@{http://www.imooc.com}">网站地址</a>
```
#### 六.引用静态资源文件js/css
application.properties
```
spring.mvc.static-path-pattern=/static/**
```
text.js
```
alert("test js");
```
test.html
```
<script th:src="@{/static/js/test.js}"></script>
```
#### 七.th:unless与th：if 

```
<br/>
<div th:if="${user.age} == 18">十八岁的天空</div>
<div th:if="${user.age} gt 18">你老了</div>
<div th:if="${user.age} lt 18">你很年轻</div>
<div th:if="${user.age} ge 18">大于等于</div>
<div th:if="${user.age} le 18">小于等于</div>
<br/>
```
#### 八.选择框
```
<br/>
<select>
     <option >选择框</option>
     <option th:selected="${user.name eq 'lee'}">lee</option>
     <option th:selected="${user.name eq 'imooc'}">imooc</option>
     <option th:selected="${user.name eq 'LeeCX'}">LeeCX</option>
</select>
<br/>
```

#### 八.循环：th：each

```
<table>
    <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>年龄备注</th>
        <th>生日</th>
    </tr>
    <tr th:each="person:${userList}">
        <td th:text="${person.name}"></td>
        <td th:text="${person.age}"></td>
        <td th:text="${person.age gt 18} ? 你老了 : 你很年轻">18岁</td>
        <td th:text="${#dates.format(user.birthday, 'yyyy-MM-dd hh:mm:ss')}"></td>
    </tr>
</table>
<br/>
```
#### 十.th：switch与th：case
1.messages.properies
```
<!--所在路径：src/main/resources/i18n/messages.properties-->
roles.manager=manager
roles.superadmin=superadmin
```

```
application.properties
```
2.所在路径：src/main/resources/application.properties
```

spring.messages.basename=i18n/messages
spring.messages.cache-seconds=3600
spring.messages.encoding=UTF-8

```

3.页面
```
<!--roles是在资源文件里配置的资源文件
设置user.name的属性，根据i18n里面的配置，来判断输出什么内容
-->
<br/>
<div th:switch="${user.name}">
  <p th:case="'lee'">lee</p>
  <p th:case="#{roles.manager}">普通管理员</p>
  <p th:case="#{roles.superadmin}">超级管理员</p>
  <p th:case="*">其他用户</p>
</div>
<br/>
```
