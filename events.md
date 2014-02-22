---
layout: events
permalink: /events/index.html
title: イベント
description:
tags: []
image:
  feature: head.jpg
---
<style>
.event {
	border: 1px gray solid;
	margin-bottom: 12px;
	padding: 8px;
	height: 140px;
	overflow: scroll;
}
.event-title {
	font-weight: bold;
	display: block;
	font-size: 1.6rem;
	margin-bottom: 8px;
}
.event-date {
	font-weight: bold;
	margin-bottom: 8px;
}
.event-date > div {
	display: inline;
	margin: 3px;
}
</style>

<div ng-app="eventApp" ng-controller="EventListCtrl">
{% raw %}
<div class="event" ng-repeat='evt in events track by $index'>
	<a class="event-title" href="{{evt.url}}" target="_blank">{{evt.title}}</a>
	<div class="event-date">
		日時:<div>{{evt.dateFrom}}</div>-<div>{{evt.dateTo}}</div>
	</div>
	<div class="event-desc">{{evt.description}}</div>
</div>
{% endraw %}
</div>

<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
<script>
var app = angular.module('eventApp', []);
app.controller('EventListCtrl', function($scope, $http){
	var eventURL = 'http://reading.fxos.org:3001/events';
	$http({method: 'GET', url: eventURL, responseType: 'json'}).
	success(function(data, status, headers, config) {
		data.forEach(function(event) {
			var from = new Date(event.dateFrom);
			var to = new Date(event.dateTo);
			if (from.getYear === to.getYear &&
				from.getMonth === to.getMonth &&
				from.getDate === to.getDate) {
				event.dateTo = twoDigit(to.getHours()) + ':' + twoDigit(to.getMinutes());
			}
		});
		$scope.events = data;
	});
});
function twoDigit(num) {
	return (num < 10) ? '0' + num : num.toString();
}
</script>
