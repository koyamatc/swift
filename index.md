---
title: swift
layout: default
---

#Swift Language Guide

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

---------------------------------

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">Classes and Structures</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.class_structure %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Properties</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.properties %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Methods</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.methods %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Subscripts</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.subscripts %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>

---------------------------------

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">Inheritance</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.inheritance %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Initialization</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.initialization %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Deinitialization</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.deinitialization %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Automatic Reference Counting</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.arc %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>

---------------------------------

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">Optional Chaining</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.optional_chaining %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Type Casting</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.type_casting %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Nested Types</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.nested_types %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Extensions</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.extensions %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>

---------------------------------

<div class="row">
	<div class="col-sm-3">
		<h4><span class="label label-info">Protocols</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.protocols %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Generics</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.generics %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info">Advanced Operators</span></h4>
		<ol class="post-list">
 			{% for post in site.categories.advanced_operators %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

	<div class="col-sm-3">
		<h4><span class="label label-info"></span></h4>
		<ol class="post-list">
 			{% for post in site.categories.x %}
   				<li><a href="{{ post.url }}">{{ post.postTitle }}</a></li>
 			{% endfor %}
		</ol>			
	</div>

</div>
