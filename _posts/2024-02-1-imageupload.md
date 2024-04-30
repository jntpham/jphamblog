---
toc: true
comments: false
layout: post
title: Image Display
type: tangibles
courses: { csp: {week: 18} }
---

### THIS CODE MADE IN COLLABORATION WITH CHATGPT 3.5


<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Viewer and Uploader</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            text-align: center;
        }
        #images-list {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
        }
        #upload-form {
            margin-top: 20px;
            text-align: center;
        }
        #upload-form input[type="file"] {
            margin-bottom: 10px;
        }
    </style>
</head>

<body>
    <h1>Image Viewer and Uploader</h1>
    <div id="images-list">
        <!-- Images will be populated here -->
    </div>
    <div id="upload-form">
        <h2>Upload an Image</h2>
        <input type="file" id="image-file" accept="image/*"><br>
        <input type="text" id="image-name" placeholder="Image name"><br>
        <button onclick="uploadImage()">Upload Image</button>
    </div>
    <script>
        // Function to upload/display image
function uploadImage() {
    const fileInput = document.getElementById('image-file');
    const imagesList = document.getElementById('images-list');
    const imageNameInput = document.getElementById('image-name');
    // Get the file and its name
    const file = fileInput.files[0];
    const imageName = imageNameInput.value || 'Unnamed Image';
    if (file) {
        const reader = new FileReader();
        // Use addEventListener to add the load event handler
        reader.addEventListener('load', function(e) {
            const imgSrc = e.target.result;
            // Create a new element for the image and the name
            const imageItem = document.createElement('div');
            imageItem.className = 'image-item';
            // Create an img element and set its src to the base64 image data
            const img = document.createElement('img');
            img.src = imgSrc;
            img.alt = imageName;
            // Create a paragraph element for customizable user input title
            const nameParagraph = document.createElement('p');
            nameParagraph.textContent = imageName;
            // Append the img element to the imageItem div
            imageItem.appendChild(img);
            imageItem.appendChild(nameParagraph);
            // Append the imageItem div to the images-list div
            imagesList.appendChild(imageItem);
        });
        // Read the file as a data URL
        reader.readAsDataURL(file);
    } else {
        alert('Please select an image file to upload.');
    }
}
    </script>
</body>
</html>
