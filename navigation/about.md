---
layout: post
title: About
permalink: /about/
comments: true
gallery_images:
  - missionary.jpg
  - john_tamara.jpg
  - tamara_fam.jpg
  - surf.jpg
  - john_lora.jpg
  - lora_fam.jpg
  - lora_fam2.jpg
  - pj_party.jpg
  - trent_family.png
  - claire.jpg
  - grandkids.jpg
  - farm.jpg
---

<!-- markdownlint-disable MD033 -->

## As a conversation Starter

Here are some places I have lived.

<comment>
Flags are made using Wikipedia images i found online
</comment>

<!-- The OCS grid grammar styles the container; JavaScript uses its id to add locations. -->
<div class="ocs__grid ocs__grid--card" id="grid_container">
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

    // 3a. The OCS card grid adjusts its columns to the available space.

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a grid cell for each location
        var gridItem = document.createElement("div");
        gridItem.className = "ocs__grid-cell";
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.className = "ocs__image-frame ocs__image-frame--thumbnail";
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
            {"image": "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/VEX_Robotics_Competition_Robot_and_Controller.jpg/960px-VEX_Robotics_Competition_Robot_and_Controller.jpg", 
            "description": "Robotics - I am interested in robotics and computer science, competing in FRC, taking CS classes, and making personal projects.",
            "alt": "robotics image"},
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
Gallery of Pics
</comment>
{% comment %}
Assign the one-per-line front matter list for the gallery iteration.
{% endcomment %}
{% assign gallery_images = page.gallery_images %}
<div class="ocs__grid ocs__grid--gallery">
  {% comment %}
  Render one OCS thumbnail for each filename in the list.{% endcomment %}
  {% for image in gallery_images %}
  <div class="ocs__grid-cell">
    <div class="ocs__image-frame ocs__image-frame--cover ocs__image-frame--thumbnail">
      <img src="{{site.baseurl}}/images/about/{{image}}" alt="Image {{forloop.index}}">
    </div>
  </div>
  {% endfor %}
</div>