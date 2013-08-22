title: filter
date: 2013-08-22 21:52:34


#Create Filter
##First

```javascript
angular.module('myApp', []).
    filter(<filter name>, <function define>);
```

##So

```html
<!DOCTYPE html>
<html ng-app="myApp">
    <head>
        <title>test</title>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
    </head>
    <body>
        <div ng-controller="Ctrl">
            <ul>
                <li ng-repeat='userName in userNames | postfix'>
                    {{userName}}
                </li>
            </ul>
        </div>
        <script>
            angular.module('myApp', []).
            filter('postfix', function(){   // use filter method to create postfix
                return function(input) {    // the input is userNames not userName!
                    var out = [];
                    for (i in input) {
                        out[i] = input[i] + ' is good!';
                    }
                    return out;
                };
            });
            // controller    
            function Ctrl($scope){
                $scope.userNames = ['dken', 'grace', 'alex', 'dinos', 'bob', 'ruby', 'linus'];
            };
        </script>
    </body>
</html>
```

###Interact with input

```html
<!DOCTYPE html>
<html ng-app="myApp">
    <head>
        <title>test</title>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.0.7/angular.min.js"></script>
    </head>
    <body>
        <div ng-controller="Ctrl">
            <input type="text" ng-model='comment'>  <!-- add ng-model -->
            <ul>
                <li ng-repeat='userName in userNames | postfix:comment'>
                    {{userName}}
                </li>
            </ul>
        </div>
        <script>
            angular.module('myApp', []).
            filter('postfix', function(){   // use filter method to create postfix
                return function(input, comment) {    // add comment be a parameter
                    var out = [];
                    for (i in input) {
                        out[i] = input[i] + ' ' + comment;
                    }
                    return out;
                };
            });
            // controller    
            function Ctrl($scope){
                $scope.comment = '';    // initial comment
                $scope.userNames = ['dken', 'grace', 'alex', 'dinos', 'bob', 'ruby', 'linus'];
            };
        </script>
    </body>
</html>
```