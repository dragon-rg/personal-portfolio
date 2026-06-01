---
layout: post
title: Input/Output (I/O)
description: Handling user input and program output
codemirror: true
permalink: /IO
---

## Table of Contents
- [Keyboard Input and Canvas Rendering](#keyboard-input-and-canvas-rendering)
- [GameEnv Configuration](#gameenv-configuration)
- [API Integration](#api-integration)
- [Asynchronous IO](#asynchronous-io)
- [JSON Parsing](#json-parsing)

## Keyboard Input and Canvas Rendering 

All of our levels contain event listeners for keyboard input, allowing us to move our players with WASD or arrow keys. Each of oour levels also uses the Canvas API to draw sprites, backgrounds, and platforms, as each game object has a `draw()`method that is called in the main game loop to render the game state on the canvas. This allows us to create visually engaging games while also providing responsive controls for the player.

## GameEnv Configuration

The `GameControl` class sets up the game world before anything else is done, configuring the environment for our level. By centralizing this configuration in the `GameControl` class, we ensure that all levels have a consistent setup and can easily be modified if needed.

## API Integration

The leaderboard makes HTTP GET requests to recieve the score data from the backend.  
```javascript
fetch(`${javaURI}/api/events/SCORE_COUNTER`, fetchOptions)
```

The code also includes a `.catch()` block to handle any errors that may occur during the fetch operation, ensuring that any errors won't be ignored and the developer can get fedback as to what went wrong. 

```javascript
.catch(err => {
    console.error('Error fetching dynamic leaderboard:', err);
    // Check for authentication errors (401 or 403 status)
    if (err.message && (err.message.includes('401') || err.message.includes('403'))) {
        list.innerHTML = `<p class="error">Please login to access this feature.</p>`;
    } else {
        list.innerHTML = `<p class="error">Failed to load leaderboard</p>`;
    }
});
```

## Asynchronous IO

The leaderboard uses `.then()` chaining to handle responses sequentially by checking if the status is okay, then parsing the JSON data, and finally displaying the leaderboard with the retrieved data. 

```javascript
fetch(`${javaURI}/api/events/SCORE_COUNTER`, fetchOptions)
.then(res => {
    if (!res.ok) throw new Error(`HTTP ${res.status}: ${res.statusText}`);
    return res.json();
})
.then(data => {
    this.displayLeaderboard(data);
})
```

## JSON Parsing

JSON Parsing converts stored data back into JavaScript objects using `JSON.parse()`:
```javascript
const stored = JSON.parse(localStorage.getItem(storageKey) || '[]');
```

This allows the code to read the storage keys(which were previously in JSON string format) as an object literal. The code later uses JSON.stringify() to convert the JavaScript object back into a JSON string for storage.
