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
		<ol class="post-list">
 			{% for post in site.categories.basicoperators %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Strings and Chractors</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.strings_characters %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Collection Types</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.collection_types %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>

---------------------------------

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">Control Flow</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.control_flow %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Functions</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.functions %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Closures</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.closures %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Enumerations</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.enumerations %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>