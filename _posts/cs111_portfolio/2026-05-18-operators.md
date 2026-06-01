---
layout: post
title: Operators
description: Computing through operators
codemirror: true
permalink: /operators
---

## Table of Contents
- [Mathematical Operators](#mathematical-operators)
- [String Operations](#string-operations)
- [Boolean Expressions](#boolean-expressions)

## Mathematical Operators

We use mathematical operators to update our gravity, velocity, and collision mechanic calculations in our assets(`Guard.js`).

```javascript
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
## String Operations

String operations combine and manipulate text using concatenation. One use for this is for our sprite paths

```javascript
src: path + "/images/gamebuilder/sprites/astro.png",
```

## Boolean Expressions

Boolean operators like `&&`, `||`, and `!` combine conditions for complex logic. We used them in the `update()` method of our `Guard.js` assets.

```javascript
if (this.spriteData && typeof this.spriteData.update === 'function') {
            this.spriteData.update.call(this);
}
// Check for collision with the player
if (!this.playerDestroyed && this.collisionChecks()) {
            this.handleCollisionEvent();
}
```

