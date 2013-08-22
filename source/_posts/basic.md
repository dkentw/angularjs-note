title: Basic
date: 2013-08-17 08:39:22
tags:
---

#Basic

##基本架構
```html
<!doctype html>
<html ng-app="MyModule">
	<body>
    1 + 2: {{ 1+2 }}.
    <script src="angular.js"></script>
    </body>
</html>
```

一切的起點都來自於一個特殊的屬性名稱 ```ng-app```, 這個 ```ng-app```並不屬於 HTML 裡頭的預設支援的屬性, 基本上 HTML 並不認得這個名稱, 但是在載入 Angularjs 後, 這個名字將會觸發 Angularjs 初始化的行為.

**Angularjs 初始化的動作:**

1. 辦認 ```ng-app```, 如果有 module name 就存下來.
2. 建立一個 injector, 整個 HTML 文件, Angularjs 都利用這個 injector 來辨認自己的 **directive** (指令).
3. 接下來的動作就是 compile 整個 HTML DOM element, 並執行 Angularjs 的相關動作.

ref: <http://docs.angularjs.org/guide/concepts>


###{{ expression }}
這個符號可以用來讀取變數或者 Model 裡的資料.

###Directive
* 在 HTML tag 裡 ```ng-``` 開頭的屬性名稱.
* 或者, 可以自成一個 HTML tag.
* 對 Angularjs 而言, **directive** 就是 **function**, 可以利用它來對 HTML 做各種操作.
* 既然是 function, 所以也可以傳入參數, 例如: `ng-app="MyModule"` 中的 *MyModule* 就是參數.

API ref: <http://docs.angularjs.org/api>

**Directive 分類**

* Hook 原有的 HTML, `<a>, <form>, <input>`.
* For template, style 操作
* For event binding
* For MVC framework


### Filter
filter 有兩種表示方式:

1. In html template
2. In Javascript

**In html template**

```
{{ expression | <filter name>:<parameters>}}
```
要注意一件事, filter 的第一個參數就是 expression 本身, 所以如果沒有在`:`後面加上參數的話, 預設就是 expression.

**In Javascript**

```
$filter('<filter name>')(<parameters>)
```

### Scope
View <--> $scope <--> Controller

* $scope 是一個物件.
* Controller 藉由 $scope 這個物件做為參數來操作 View.
* scope 有分為 root scope, child scope. ![Root scope](http://docs.angularjs.org/img/tutorial/tutorial_00.png)
* ng-controller 會建立一個新的 child scope.

ref: <http://docs.angularjs.org/guide/scope>


### Controller
1. 當 ng-controller 第一次出現在 HTML 裡時, Angularjs 就會對它進行初始化.
2. 初始化之後, 會產生自己的 variable scope, 如果傳入 $scope 同時也可以建立一個新的 data model ( create new child scope )

```html
<!DOCTYPE html>
<html ng-app>
    <head>
        <title>test</title>
    </head>
    <body>
        <div ng-controller="Ctrl">
            <input type="text" ng-model="username">
        </div>
        <div ng-controller="Spy"></div>
        <script>
            function Ctrl($scope){
            	/* Initial */
                console.log('initial');
                console.log($scope.username);
                /* Create scope */
                $scope.username = 'dken';
                console.log($scope.username);
            };
            function Spy($scope){
                console.log('initial spy');
            };
        </script>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
    </body>
</html>
```
### Services
* Services 是根據 DI(Dependency Injector)來實做的.
* 所有的 Angularjs 內建的 services 名稱都以 $ 做為開頭.


![](http://docs.angularjs.org/img/tutorial/xhr_service_final.png)

### DI
* DI 無所不在

<http://docs.angularjs.org/guide/di>

### MVC
M~V~C~
![](http://docs.angularjs.org/img/guide/about_view_final.png)

### DATA Binding
Ref: <http://docs.angularjs.org/guide/dev_guide.templates.databinding>
