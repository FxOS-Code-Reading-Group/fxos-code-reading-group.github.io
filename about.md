---
layout: post
permalink: /about/index.html
title: About
description:
tags: []
image:
  feature: head.jpg
---
<style>
.about-members {
	padding-left: 30px;
}
.about-members > p {
	margin-bottom: 5px;
}
.member img {
	display: inline;
	width: 50px;
	height: 50px;
	margin: 5px 10px 5px 5px;
	vertical-align: middle;
}
.member .name {
	display: inline;
	font-size: 1.2rem;
}
</style>

[FxOS コードリーディング](https://www.facebook.com/groups/fxos.code.reading/)では [Firefox OS コミュニティ](http://fxos.org/)の支援により、[reading.fxos.org](reading.fxos.org) サブドメインでサーバを運営しています。

サーバは GMO インターネット様のコミュニティ支援で ConoHa VPS をご提供頂いています。

- <http://www.conoha.jp/community>

#### 運営メンバー

<section class="about-members" ng-app="aboutApp" ng-controller="MemberCtrl">
<p>現在、このサーバは以下のメンバーで運営しています。</p>

{% raw %}
<div class="member" ng-repeat="member in members">
<a href="{{member.fbUrl}}">
<img src="{{member.photo}}">
<div class="name">{{member.name}}</div>
</a>
</section>
{% endraw %}
</div>
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.12/angular.min.js"></script>
<script>
var app = angular.module('aboutApp', []);
app.controller('MemberCtrl', function($scope, members) {
	$scope.members = members;
});
app.value('members', [
	{
		"name": "Yabushita Masami", 
		"fbUrl": "https://www.facebook.com/aoitan",
		"photo": "https://fbcdn-profile-a.akamaihd.net/hprofile-ak-prn2/t5/211907_100002226748952_1181208063_q.jpg"
	}, 
	{
		"name": "Muneaki Nishimura", 
		"fbUrl": "https://www.facebook.com/muneaki.nishimura",
		"photo": "https://fbcdn-profile-a.akamaihd.net/hprofile-ak-prn2/t5/211864_100000789139984_1113866819_q.jpg"
	},
	{
		"name": "Mizuho Sakamaki", 
		"fbUrl": "https://www.facebook.com/miz.sak.9",
		"photo": "https://fbcdn-profile-a.akamaihd.net/hprofile-ak-prn2/t5/1076156_100003028510608_2021514009_q.jpg"
	}, 
	{
		"name": "Hayato Hiratori", 
		"fbUrl": "https://www.facebook.com/hayato.hiratori",
		"photo": "https://fbcdn-profile-a.akamaihd.net/hprofile-ak-ash2/t5/1118755_100004317186751_709080406_q.jpg"
	}
]);
</script>
