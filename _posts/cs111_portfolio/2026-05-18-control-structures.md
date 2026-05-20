---
layout: post
title: Control Structures
description: Mastery of conditionals, loops, and program flow control
codemirror: true
permalink: /control-structures
---

## Iteration

Our game engine uses loops for many tasks, one of which being checking for collisions in `Enemy.js`.

```
/**
* Check if the Enemy collides with the Player.
* @returns {boolean} True if the Enemy collides with the Player, False otherwise.
*/
collisionChecks() {
    for (const gameObj of this.gameEnv.gameObjects) {
        if (gameObj instanceof Player) {
            this.isCollision(gameObj);
            if (this.collisionData.hit) {
                return true;
            }
        }
    }
        return false;
}
```

## Conditionals and Nested Conditions

Our game engine also uses conditionals for many of it's core purposes. An example of this is the `handleCollisionReaction()` method in the root `GameObject` class. This method uses conditionals to determine how the game object reacts to collisions with dialogue. 

```javascript
/**
 * Handles the reaction to the collision, updated to use dialogue (from end team hack)
 * @param {*} other 
 */
handleCollisionReaction(other) {
// First check if reaction is a function that can be called
    if (other && other.reaction && typeof other.reaction === "function") {
        other.reaction();
        return;
    }
    
    // If the object has a dialogueSystem, use it instead of console.log
    if (other && other.id) {
        // Try to find the object instance to use its dialogueSystem
        const targetObject = this.gameEnv.gameObjects.find(obj => 
            obj.spriteData && obj.spriteData.id === other.id
        );
        
        if (targetObject && targetObject.dialogueSystem) {
            targetObject.showReactionDialogue();
        } else if (targetObject && targetObject.showItemMessage) {
            targetObject.showItemMessage();
        } else if (other.greeting) {
            // Fallback to greeting if available
            console.log(other.greeting);
        }
    }
}
```

