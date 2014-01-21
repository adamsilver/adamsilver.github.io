---
layout: post
title:  "ECMAScript namespacing"
date:   2014-04-01 09:00:01
categories: js
---

A namespace is a descriptive way of naming objects in a way that encapsulates its members, which enables the same member names within multiple different objects. Utilising this concept is very simple in ECMAScript but it is common to find [over-engineered](http://stackoverflow.com/questions/3410984/javascript-namespace) solutions which are often best avoided. Utilising namespacing is very simple:

## 1. Define top level namespace

The 1st level is typically the name of the application. Let's call this application 'zoo'.

	// zoo.js
	var zoo = {};

LowerCamelcase naming is used; UpperCamelCase is typically reserved for constructors only.

## 2. Define second level namespace

Our 'zoo' application needs a bunch of animals so let's define the 2nd level called 'animals': our animals within this namespace.

	// zoo.animals.js
	zoo.animals = {};

## 3. Define a component within namespace

Having provided some structure to our application let's create an animal component called 'Zebra'. This will be placed within the 'animals' namespace:

	// zoo.animals.Zebra.js
	zoo.animals.Zebra = function() {};
	zoo.animals.Zebra.prototype.eat = function() {};

That's all there is to it.