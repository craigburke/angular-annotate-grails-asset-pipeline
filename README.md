AngularJs Annotate Asset-Pipeline
================================
[![Build Status](https://drone.io/github.com/craigburke/angular-annotate-asset-pipeline/status.png)](https://drone.io/github.com/craigburke/angular-annotate-asset-pipeline/latest)

The Grails `angular-annotate-asset-pipeline` is a plugin that provides annotations for dependecy injections to allow angular files to be minified within the asset pipeline.

For more information on how to use asset-pipeline, visit [here](http://www.github.com/bertramdev/asset-pipeline).

## Getting started
Add the plugin to your **BuildConfig.groovy**:
```groovy
plugins {
		runtime ":angular-annotate-asset-pipeline:1.0.0"
}
```

## How it works

Since the parameter names are significant for AngularJS to do dependency injection and most minifiers rename parameters,
you have to use inline annotations. See [A Note on Minification](https://docs.angularjs.org/tutorial/step_05)

This plugin uses [ng-annotate](https://github.com/olov/ng-annotate) to add those inline annotation and make your angular files safe to minify.

For example this 
```javascript
angular.module('myApp', [])
	.controller('IndexController', function($scope) {
		$scope.message = "Hello world"
	});
```

Will be automatically annotated like so:
```javascript
angular.module('myApp', [])
        .controller('IndexController', ['$scope', function($scope) {
                $scope.message = "Hello world"
        }]);
```