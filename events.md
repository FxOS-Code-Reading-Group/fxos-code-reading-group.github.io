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
	font-size: .8rem;
}
.event-title {
	font-weight: bold;
	display: block;
	font-size: 1.4rem;
	margin-bottom: 8px;
}
.event-date, .event-location {
	font-weight: bold;
	margin-bottom: 8px;
}
.event-date > div {
	display: inline;
	margin: 3px;
}
</style>

<div ng-app="evtApp" ng-controller="EventListCtrl">
{% raw %}
<div class="event" ng-repeat='evt in events track by $index'>
	<a class="event-title" href="{{evt.url}}" target="_blank">{{evt.title}}</a>
	<div class="event-date">
		日時:<div>{{evt.from|date:'yyyy/MM/dd HH:mm'}}</div>-
		<div ng-if="evt.isOneDay">{{evt.to|date:'HH:mm'}}</div>
		<div ng-if="!evt.isOneDay">{{evt.to|date:'yyyy/MM/dd HH:mm'}}</div>
	</div>
	<div class="event-location">場所: {{evt.location}}</div>
	<div class="event-desc">{{evt.description}}</div>
</div>
{% endraw %}
</div>

<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
<script>
var app = angular.module('evtApp', []);
app.controller('EventListCtrl', function($scope, $http) {
	var eventURL = 'http://reading.fxos.org:3001/events/gcal';
	$http({method: 'GET', url: eventURL, responseType: 'json'}).
	success(function(data, status) {
		var events = [];
		if (status == 200) {
			data.items.forEach(function(item) {
				var from = new Date(item.start.dateTime);
				var to = new Date(item.end.dateTime);
				var desc = parseDesc(item.description);
				events.push({
					title: item.summary,
					from: from,
					to: to,
					location: item.location,
					isOneDay: isSameDate(from, to),
					url: desc.url,
					description: desc.description,
				});
			});
		}
		$scope.events = events;
	});
});
function isSameDate(from, to) {
	return (from.getYear() === to.getYear() &&
			from.getMonth() === to.getMonth() &&
			from.getDate() === to.getDate());
}
function parseDesc(desc) {
	var lines = desc.split('\n');
	var ret = {};
	if (lines.length >=1 && lines[0].match(/^(http|https):\/\//)) {
		ret.url = lines[0];
		ret.description = lines.slice(1).join(' ');
	} else {
		ret.url = null;
		ret.description = lines.join(' ');
	}
	return ret;
}
</script>
