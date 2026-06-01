---
layout: post
title: Documentation
description: Writing clear documentation and comments to explain code
codemirror: true
permalink: /doc
---

## Table of Contents
- [Code Comments/JSDocs](#code-commentsjsdocs)
- [Mini Lesson](#mini-lesson)

## Code Comments/JSDocs

In my `Guard.js` and `HorizontalGuard.js` asset files, I made sure to include comments and JSDocs to explain the purpose of the methods I overrode in the respective classes. This make it easy for other developers and my future self to understand the purpose of the code later on, saving us more time. Example:
```javascript
/**
 * stayWithinCanvas method ensures that the object stays within the boundaries of the canvas.
 * With this override, we can also reverse the velocity whenever the guard hits the edges of the canvas.
 */
stayWithinCanvas() {
    // Bottom of the canvas
    if (this.position.y + this.height > this.gameEnv.innerHeight) {
        this.position.y = this.gameEnv.innerHeight - this.height;
        this.velocity.y *= -1; // Reverse vertical velocity to create a "bounce" effect
        console.log(this.velocity.y);
    }
    // Top of the canvas
    if (this.position.y < 0) {
        this.position.y = 1;
        this.velocity.y *= -1; // Reverse vertical velocity to create a "bounce" effects
        console.log(this.velocity.y);
    }
    // Right of the canvas
    if (this.position.x + this.width > this.gameEnv.innerWidth) {
        this.position.x = this.gameEnv.innerWidth - this.width;
        this.velocity.x = 0;
    }
    // Left of the canvas
    if (this.position.x < 0) {
        this.position.x = 0;
        this.velocity.x = 0;
    }
}
```

## Mini Lesson
I collaborated with my groups to create multiple mini lessons in a comic/visual style to explain Data Abstraction, Collision Mechanics, and Local Storage to my peers.

| [data abstraction]({{site.baseurl}}/js/data-abstraction) | [collision mechanics]({{site.baseurl}}/collision-mechanics) | [local storage]({{site.baseurl}}/local-storage) | 
