---
title: swift
layout: default
---

#swiftの学習

- - -

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">The Basics</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.basics %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Basics Operators</span></h4>
		<ul class="post-list">
 			{% for post in site.categories.basicoperators %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			

		<h4></h4>
		<ul class="post-list">
 			{% for post in site.categories.scale %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			

		<h4></h4>
		<ul class="post-list">
 			{% for post in site.categories.layout %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			
	</div>

	<div class="col-sm-3">
		<h4></h4>
		<ul class="post-list">
 			{% for post in site.categories.shapes %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			
		<h4></h4>
		<ul class="post-list">
 			{% for post in site.categories.geo %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			
	</div>

	<div class="col-sm-3">
		<h4></h4>
		<ul class="post-list">
 			{% for post in site.categories.transition %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ul>			
	</div>

</div>