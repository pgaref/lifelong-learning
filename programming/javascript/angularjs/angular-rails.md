# AngularJS + Rails Book

# 3: Why Angular?

*Bindings.* Angular uses binding to update content on the page.

    $http({ method: 'GET', url: 'http://some_url/books'})
      .success(function(response) {
        $scope.books = response.books
      });

## Cons

- *Binding.* Some people hate binding.
- *No model layer. Since Angular binds to native JSON, you don't need a model layer.* The path of least resistance is to have domain related services that operate on your simple JSON. Instead of `user.save()`, call `User.save($scope.user)`.
- No framework.

# 4: Hello Angular

> `angular-application.js`

    //= require_self
    //= require_tree ./angular
    AngulaRails = angular.module("AngulaRails", []);

    %select{"ng-model" => "taco.filling", "class" => "form-control", "ng-options" => "f for f in fillings"} # fillings defined as $scope.fillings
      %option{"value" => ""} Pick something # default select choice

Check boxes/radio buttons: A bit intuitive.

# 6: Models Need Dots

*The golden rule of Angular binding is that `ng-model` should be bound to models with dots.* Basically unless we use dots and shit, scope will creep itself somewhere.

# 7: AngularJS Validation

# 8: HTTP with AngularJS

    $scope.populateExpenses = () ->
      url = "/api/v1/expenses/"
      $http({method: "GET", url: url })
        .success (data) ->
          $scope.expenses = data

`$http` allows for async http requests using promises. With Angular, we can stick the JSON we get back from the http request right into the `$scope`.

To handle errors, we can use the `.error` method.

      $http({method: "GET", url: url })
        .success (data) ->
          $scope.expenses = data
        .error (data, status) ->
          $scope.searching = false
          $scope.errorMessage = 'User not found'

# 9: Talking to Rails

Rails CSRF:

    AngulaRails.config ['$httpProvider', ($httpProvider) ->
      $httpProvider.defaults.headers.common['X-CSRF-Token'] = $('meta[name=csrf-token\]').attr('content')
      $httpProvider.defaults.headers.common.Accept = 'application/json'
    ]

If we have the books when we build the page, why do we need to make an AJAX call?

[TODO]: NO_AJAX_CALL_ON_CREATE.

## 9: POST /books
