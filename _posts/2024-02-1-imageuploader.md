---
toc: true
comments: false
layout: post
title: Image Display
type: tangibles
courses: { csp: {week: 17} }
---




<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Viewer and Uploader</title>
    <style>
        /* Add some styles for the page */
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
        .image-item {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
            width: 150px;
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
        function uploadImage() {
        const fileInput = document.getElementById('image-file');
            const imagesList = document.getElementById('images-list');
            const imageNameInput = document.getElementById('image-name');
            // Get the file and its name
            const file = fileInput.files[0];
            const imageName = imageNameInput.value || 'Unnamed Image';    
        }
            

        const apiBaseUrl = '/api/images';
        // Function to fetch and display images from the API
        async function fetchImages() {
            try {
                const response = await fetch(apiBaseUrl);
                const data = await response.json();
                const imagesList = document.getElementById('images-list');
                imagesList.innerHTML = ''; // Clear existing images
                // Loop through the data and display each image
                data.forEach(imageData => {
                    if (imageData.error) {
                        // Display error message if any
                        const errorMessage = document.createElement('div');
                        errorMessage.innerText = imageData.error;
                        imagesList.appendChild(errorMessage);
                    } else {
                        // Create a div for each image
                        const imageItem = document.createElement('div');
                        imageItem.className = 'image-item';
                        // Create an img element and set its src to the base64 image data
                        const img = document.createElement('img');
                        img.src = `data:image/jpeg;base64,${imageData.imageData}`;
                        img.alt = imageData.imagePath;
                        // Append the img element to the div
                        imageItem.appendChild(img);
                        // Append the div to the images list
                        imagesList.appendChild(imageItem);
                    }
                });
            } catch (error) {
                console.error('Error fetching images:', error);
            }
        }
        // Function to upload an image to the API
        async function uploadImage() {
            const imageFile = document.getElementById('image-file').files[0];
            const imageName = document.getElementById('image-name').value;
            if (imageFile && imageName) {
                try {
                    // Read the file as base64
                    const reader = new FileReader();
                    reader.onload = async function(e) {
                        const base64String = e.target.result.split(',')[1]; // Get the base64 string
                        // Create a JSON object to send in the POST request
                        const jsonData = {
                            base64_string: base64String,
                            name: imageName
                        };
                        // Send a POST request to the API
                        const response = await fetch(`${127.0.0.1:4100/api/images}/upload`, {
                            method: 'POST',
                            headers: {
                                'Content-Type': 'application/json'
                            },
                            body: JSON.stringify(jsonData)
                        });
                        const result = await response.json();
                        alert(result.message || result.error);
                        // Refresh the images list after uploading
                        if (response.ok) {
                            fetchImages(); // Call fetchImages() to refresh the list of images
                        }
                    };
                    reader.readAsDataURL(imageFile);
                } catch (error) {
                    console.error('Error uploading image:', error);
                }
            } else {
                alert('Please select an image file and enter a name.');
            }
        }
        // Fetch and display images on page load
        fetchImages();
    </script>
</body>
</html>

