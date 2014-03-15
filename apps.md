---
layout: 
permalink: /apps/index.html
title: Apps
description:
tags: []
image:
---
<style>
.about-apps {
	padding-left: 10px;
}
.about-apps > p {
	margin-bottom: 5px;
}
.app {
}
.app img {
	display: inline;
	width: 64px;
	height: 64px;
	margin: 5px 10px 5px 5px;
	vertical-align: middle;
}
.app .name {
	font-size: 1rem;
	overflow: hidden;
}
</style>

<section class="about-apps" ng-app="installApp" ng-controller="AppsCtrl">
{% raw %}
<!--
<div class="member" ng-repeat="member in members">
<a href="{{member.fbUrl}}">
<img src="{{member.photo}}">
<div class="name">{{member.name}}</div>
</a>
</div>
-->
<table>
<tr class="app" ng-repeat="item in apps" ng-click="installApp(item)">
	<td><img src="{{item.icon}}"></td>
	<td class="name">{{item.name}}</td>
</tr>
</table>
{% endraw %}
</section>
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
<script>
var BASE_URL = 'https://marketplace.firefox.com/api/v1/apps/app/';
var app = angular.module('installApp', []);
app.controller('AppsCtrl', function($scope, $http, slugs) {
	$http.defaults.useXDomain = true;
	var apps = [];
	slugs.forEach(function(slug) {
		var url = BASE_URL + slug + '/';
		$http.get(url).success(function(obj) {
			var app = {};
			app.name = obj.name['en-US'];
			app.slug = obj.slug;
			app.manifest = obj.manifest_url;
			app.icon = obj.icons['64'];
			apps.push(app);
		})
	});
	$scope.apps = apps;
	$scope.installApp = function(item) {
		console.log(item.slug);
		if (navigator.mozApps) {
			var req = navigator.mozApps.installPackage(item.manifest);
			req.onsuccess = function() {
		        alert(this.result.origin);
    		};
      		req.onerror = function() {
        		alert(this.error.name);
      		};
		}
	};
});
app.value('slugs', ['cameran', 'line', 'rakutengateway', 'flappy-birds']);
</script>
