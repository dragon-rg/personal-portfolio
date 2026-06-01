---
layout: post
title: Data Types
description: Data types in the JavaScript language
codemirror: true
permalink: /data-types
---

## Table of Contents
- [Numbers](#numbers)
- [Strings](#strings)
- [Booleans](#booleans)
- [Arrays](#arrays)
- [Objects](#objects)

## Numbers

Numbers represent quantities and measurements used in calculations and comparisons.

{% capture numbers_example %}
let num1 = 16
let num2 = 42

console.log(num1 + num2); // 58
{% endcapture %}
{% include runners/code.html runner_id="js-numbers" language="javascript" code=numbers_example %}

## Strings

Strings store text data and can be combined and separated.

{% capture strings_example %}
let str1 = "Apples";
let str2 = "Bananas";

//first string
console.log(str2); // "Bananas"

//concatenation
console.log(str1 + " and " + str2); // "Apples and Bananas"

//slicing
console.log(str1.slice(0, 3)); // "App"
{% endcapture %}
{% include runners/code.html runner_id="js-strings" language="javascript" code=strings_example %}

## Booleans

Booleans represent true/false values and can be used with logical operators and conditionals.

{% capture booleans_example %}
let atDestination = false;
let aboveSpeedLimit = true;

if (atDestination) {
    console.log("At destination, stop the vehicle.");
} else if (aboveSpeedLimit) {
    console.log("Above speed limit, slow down.");
} else {
    console.log("Below speed limit, can speed up.");
}

// will print the else if statement since aboveSpeedLimit is true
{% endcapture %}
{% include runners/code.html runner_id="js-booleans" language="javascript" code=booleans_example %}

## Arrays

Arrays store collections of data that can be accessed and manipulated.

{% capture arrays_example %}
let fruits = ["apple", "banana", "orange"];
let numbers = [10, 20, 30, 40];

fruits.push("grape");
console.log(fruits);
console.log(numbers[0]);
console.log(numbers.length);
{% endcapture %}
{% include runners/code.html runner_id="js-arrays" language="javascript" code=arrays_example %}

## Objects

Objects store related data as key-value pairs and organize complex information.

{% capture objects_example %}
let user = {
    name: "Alice",
    age: 25,
    email: "alice@example.com"
};

console.log("Username: " + user.name);
console.log("JSON format: " + JSON.stringify(user));
console.log("Parsed into javascript object: " + JSON.parse(JSON.stringify(user)).name);
{% endcapture %}
{% include runners/code.html runner_id="js-objects" language="javascript" code=objects_example %}
