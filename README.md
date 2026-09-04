# Ex05 Image Carousel
## Date: 01/09/2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
## App.jsx
```
import { useEffect, useState } from "react";
import "./App.css";

function App() {
  const images = [
    "/images/image1.png",
    "/images/image2.png",
    "/images/image3.png",
    "/images/image4.png",
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const previousImage = () => {
    setCurrentIndex(
      (currentIndex - 1 + images.length) % images.length
    );
  };

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentIndex((currentIndex + 1) % images.length);
    }, 3000);

    return () => clearInterval(interval);
  }, [currentIndex]);

  return (
    <div className="container">
      <h1>Image Carousel</h1>

      <div className="carousel">
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex + 1}`}
        />

        <button className="previous" onClick={previousImage}>
          ❮
        </button>

        <button className="next" onClick={nextImage}>
          ❯
        </button>
      </div>

      <p>
        Image {currentIndex + 1} of {images.length}
      </p>
    </div>
  );
}

export default App;
```
## App.css
```
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f2f2f2;
}

.container {
  text-align: center;
  padding-top: 40px;
}

h1 {
  margin-bottom: 25px;
}

.carousel {
  position: relative;
  width: 700px;
  height: 400px;
  margin: auto;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.carousel img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border: none;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  font-size: 30px;
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 5px;
}

.previous {
  left: 15px;
}

.next {
  right: 15px;
}

button:hover {
  background-color: rgba(0, 0, 0, 0.8);
}

p {
  font-size: 18px;
  font-weight: bold;
}
```
## index.css
```
* {
  box-sizing: border-box;
}
```

## OUTPUT
![alt text](image.png)

![alt text](image-1.png)

![alt text](image-2.png)

![alt text](image-3.png)
## RESULT
The program for creating Image Carousel using React is executed successfully.
