---
layout: post
title: About
permalink: /about/
comments: true
---

## As a conversation Starter

Here are some places I have lived.

<comment>
Flags are made using Wikipedia images
</comment>

<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "4/41/Flag_of_India.svg", "description": "India - 1 year"},
        {"flag": "0/01/Flag_of_California.svg", "description": "California - 1 year"},
        {"flag": "1/1a/Flag_of_New_York.svg", "description": "New York - 1.5 year"},
        {"flag": "0/01/Flag_of_California.svg", "description": "California - Returned to the Golden State"},
    ];
    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>

### Journey through Life

Here is what I did at those places

- Born in India
- moved to the U.S. when when I was around a year old
- Residence switched from California to New York and finally back to California
- Grade Schooling in California
- Current student at Del Norte High School, co29

### Family, Hobbies, and Interests

I value my family very much, and I love to spend time with them. Some other hobbies/interests include:
<div class="grid-container" id="hobbies_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    var container = document.getElementById("hobbies_container");

    var hobbiesAndInterests = [ //images sources for the various hobbies I have
            {"image": "https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/Tennis_Racket_and_Balls.jpg/960px-Tennis_Racket_and_Balls.jpg", 
            "description": "Tennis - I play tennis regularly and love the sport.", 
            "alt": "Tennis image"},
            {"image": "https://upload.wikimedia.org/wikipedia/commons/e/ec/DnD_Symbolbild.jpg", 
            "description": "I love playing dungeons and dragons with my friends",
            "alt": "Dungeons and Dragons image"},
            {"image": "{{site.baseurl}}/images/about/Santa_Clarita_ATA_Picture.jpg",
            "description": "Martial Arts - I practice and compete in Taekwondo.",
            "alt": "Martial Arts image"}
    ];

    for (const hobby of hobbiesAndInterests) { //same as the grid above, but for hobbies instead
        var interestGridItem = document.createElement("div");
        interestGridItem.className = "grid-item";

        var img = document.createElement("img");
        img.src = hobby.image;
        img.alt = hobby.alt;

        var description = document.createElement("p");
        description.textContent = hobby.description;

        interestGridItem.appendChild(img);
        interestGridItem.appendChild(description);

        container.appendChild(interestGridItem);
    }
</script>    

<comment>
Gallery of Pics, scroll to the right for more ...
</comment>
<div class="image-gallery">
  <img src="{{site.baseurl}}/images/about/Carlsbad_Beach_Solo.jpg" alt="Image 1">
  <img src="{{site.baseurl}}/images/about/Districts_2025_Solo.jpg" alt="Image 2">
  <img src="{{site.baseurl}}/images/about/family_singapore.jpg" alt="Image 3">
  <img src="{{site.baseurl}}/images/about/Riggu_Aksho_Dhoti_function.jpg" alt="Image 4">
  <img src="{{site.baseurl}}/images/about/shake_shack_singapore.jpg" alt="Image 5">
  <img src="{{site.baseurl}}/images/about/UniversalStudios_Transformers_Sign.jpg" alt="Image 6">
  <img src="{{site.baseurl}}/images/about/XMA_Outfit_Headshot.jpg" alt="Image 7">
</div>