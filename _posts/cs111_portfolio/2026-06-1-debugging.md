---
layout: post
title: Debugging
description: Techniques for debugging game code using browser developer tools
codemirror: true
permalink: /debugging
---

## Table of Contents
- [Console Debugging](#console-debugging)
- [Hit Box Visualization](#hit-box-visualization)
- [Source-Level Debugging](#source-level-debugging)
- [Network Debugging](#network-debugging)
- [Application Debugging](#application-debugging)
- [Element Inspection](#element-inspection)

## Console Debugging

Console debugging is the foundation of tracking game state and identifying issues. Using `console.log()` strategically throughout your code allows you to monitor variables, method calls, and game flow in real-time.

### Strategic Logging in Update Methods

In my game projects, I use `console.log()` to track collision detection and state changes:

```javascript
/**
 * Example from Guard.js - tracking collision and boundary behavior
 */
update() {
    // Update begins by drawing the object
    this.draw();

    if (this.spriteData && typeof this.spriteData.update === 'function') {
        this.spriteData.update.call(this);
    }
    // Check for collision with the player
    if (!this.playerDestroyed && this.collisionChecks()) {
        this.handleCollisionEvent();
    }

    this.position.y += this.velocity.y; // update position

    // Ensure the object stays within the canvas boundaries
    this.stayWithinCanvas();
}

stayWithinCanvas() {
    // Bottom of the canvas
    if (this.position.y + this.height > this.gameEnv.innerHeight) {
        this.position.y = this.gameEnv.innerHeight - this.height;
        this.velocity.y *= -1; // Reverse vertical velocity to create a "bounce" effect
        console.log(this.velocity.y);  // ← Debug: Track velocity changes
    }
    // ...more boundary checks...
}

handleCollisionEvent() {
    var player = this.gameEnv.gameObjects.find(obj => obj instanceof Player); 

    console.log("Collision has occurred, player has been destroyed.");  // ← Debug: Log collision events

    player.destroy();
    this.playerDestroyed = true;
}
```

**How to Use Console Logging:**
- Open **DevTools** with `F12` or right-click → Inspect
- Go to the **Console** tab
- As your game runs, logs will appear showing variable values, method calls, and state changes
- Use different log levels: `console.log()`, `console.warn()`, `console.error()`

## Hit Box Visualization

Visualizing collision boundaries helps you understand why collisions are or aren't being detected. By drawing rectangles around game objects, you can refine your collision detection logic.

### Drawing Collision Boundaries

Most game engines can toggle hitbox visualization. This allows you to see the collision rectangles around your game objects:

```javascript
/**
 * Example: Visualizing a collision boundary on the canvas
 */
function drawHitbox(gameObject, context) {
    const hitbox = gameObject.collisionData.hit;
    
    // Draw rectangle showing the collision boundary
    context.strokeStyle = 'red';  // Red for active collision
    context.lineWidth = 2;
    context.strokeRect(
        hitbox.x,
        hitbox.y,
        hitbox.width,
        hitbox.height
    );
}

// In your render loop, conditionally draw hitboxes
if (DEBUG_MODE) {
    for (const gameObj of gameEnv.gameObjects) {
        drawHitbox(gameObj, context);
    }
}
```

**To Toggle Hitbox Display:**
1. Add a debug flag in your game configuration
2. Press a key (like `D`) to toggle `DEBUG_MODE`
3. Adjust collision rectangle values until collisions work as expected

## Source-Level Debugging

Source-level debugging lets you pause code execution and inspect variables at specific points, making it easier to understand complex logic.

### Using Breakpoints in DevTools

```javascript
/**
 * Example: Setting a breakpoint to examine collision logic
 */
handleCollisionEvent() {
    var player = this.gameEnv.gameObjects.find(obj => obj instanceof Player);
    
    // ← DevTools: Click the line number to set a breakpoint here
    console.log("Collision has occurred, player has been destroyed.");
    
    player.destroy();
    this.playerDestroyed = true;
}
```

**How to Debug with Breakpoints:**
1. Open DevTools (`F12`)
2. Go to the **Sources** tab
3. Find your JavaScript file
4. Click on the line number to set a **breakpoint** (a blue marker appears)
5. Run your game and trigger the code
6. Execution pauses at the breakpoint
7. Use the **Variables panel** to inspect object values
8. Click **Step Over** (or press `F10`) to execute line-by-line
9. Click **Resume** (or press `F8`) to continue execution

## Network Debugging

Network debugging helps you track API calls and inspect responses for errors.

### Examining Fetch Requests

In my heist-exe project, `heistMusic.js` checks the fetch response for errors:

```javascript
async fetchPreviewUrl() {
    const response = await fetch(this.endpoint);
    if (!response.ok) {
      throw new Error('API request failed (' + response.status + ')');
    }
    const data = await response.json();
    // ... rest of the code
}

async startMusic() {
    try {
      const previewUrl = await this.fetchPreviewUrl();
      this.audio = new Audio(previewUrl);
      this.audio.play();
    } catch (error) {
      console.warn('Background music: failed to start', error);
    }
}
```

**How to Debug Network Requests:**
1. Open DevTools (`F12`) → **Network** tab
2. Trigger the API call
3. Click on the request to inspect:
   - **Status**: 200 (success), 404 (not found), 500 (error)
   - **Response**: The data returned from the API
   - **Headers**: Request/response metadata

## Application Debugging

Application debugging lets you inspect browser storage where game state is persisted—cookies, localStorage, and sessionStorage.

### Inspecting Stored Data

From my local-storage project:

```javascript
/**
 * Example: Storing and retrieving player data
 */
// Store coins collected
const coinsCollected = parseInt(localStorage.getItem('coinsCollected') || '0');
const newTotal = coinsCollected + this.value;
localStorage.setItem('coinsCollected', newTotal);

// Store player name in session storage
const playerName = sessionStorage.getItem('playerName');
if (!playerName) {
    playerName = prompt('Enter your name for the leaderboard:') || 'Anonymous';
    sessionStorage.setItem('playerName', playerName);
}
```

**How to Debug Application Storage:**
1. Open DevTools (`F12`)
2. Go to the **Application** tab
3. Look at the left sidebar:
   - **LocalStorage**: Persists across browser sessions
   - **SessionStorage**: Clears when you close the tab
   - **Cookies**: Authentication and user tracking data
4. Select an entry to see all stored data
5. You can edit, delete, or clear storage manually for testing
6. Use the search function to find specific keys

## Element Inspection

Element inspection helps you understand the DOM structure, check styles, and inspect game canvas properties.

### Inspecting Canvas and DOM Elements

```html
<!-- Example: Canvas element in your HTML -->
<canvas id="gameCanvas" width="800" height="600"></canvas>

<!-- DevTools allows you to inspect these elements -->
```

**How to Inspect Elements:**
1. Open DevTools (`F12`)
2. Go to the **Elements** tab
3. Click the **Select Element** button (top-left arrow icon)
4. Click on any element in your game or page
5. The DevTools will show:
   - **HTML structure**: How the element is nested
   - **Styles**: All CSS applied to the element
   - **Box Model**: Padding, margin, borders, dimensions
   - **Event Listeners**: JavaScript events attached to the element

### Inspecting Game Object State

You can also inspect JavaScript objects in the Console:

```javascript
// In your console, type:
gameEnv.gameObjects  // View all game objects
gameEnv.gameObjects[0]  // Inspect a specific object
player.position  // Check player's current position
player.velocity  // Check velocity values
```

This allows you to query your game state in real-time without adding console logs everywhere.

---

## Debugging Workflow Example

Here's how to debug a collision issue:

1. **Console Debugging**: Add `console.log()` to track collision detection
2. **Element Inspection**: Use the console to check `player.position` and `enemy.position`
3. **Hit Box Visualization**: Enable debug mode to see collision rectangles
4. **Source-Level Debugging**: Set a breakpoint in `handleCollisionEvent()`
5. **Step Through**: Use Step Over to execute line-by-line
6. **Application Debugging**: Check if game state is being saved correctly

By combining these techniques, you can quickly identify and fix bugs in your game!
