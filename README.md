# Ex05 Image Carousel

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
## imageCarousel.jsx
```
import React, { useState, useEffect } from 'react';
import './ImageCarousel.css';

const images = [
  'https://img.etimg.com/thumb/width-1200,height-1200,imgsize-69266,resizemode-75,msid-106774994/industry/auto/cars-uvs/super-sports-car-segment-in-india-to-register-30-pc-growth-this-year-mclaren-automotive.jpg',
  'https://cdn-s3.autocarindia.com/Mercedes/cle-coupe/23c0420_001.jpg?w=640&q=75',
  'https://cdn-s3.autocarindia.com/Mercedes/cle-coupe/23c0420_001.jpg?w=640&q=75',
  'https://www.spinny.com/blog/wp-content/uploads/2024/09/videoframe_0-1160x653.webp',
];

const ImageCarousel = ({ autoPlay = true, interval = 3000 }) => {
  const [currentIndex, setCurrentIndex] = useState(0);

  // Automatic slide change
  useEffect(() => {
    if (!autoPlay) return;
    const timer = setInterval(() => {
      setCurrentIndex((prev) => (prev + 1) % images.length);
    }, interval);
    return () => clearInterval(timer);
  }, [autoPlay, interval]);

  const goToNext = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const goToPrev = () => {
    setCurrentIndex((currentIndex - 1 + images.length) % images.length);
  };

  return (
    <div className="carousel-container">
      <div className="carousel-wrapper">
        <button className="arrow left" onClick={goToPrev}>
          &#10094;
        </button>
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex}`}
          className="carousel-image"
        />
        <button className="arrow right" onClick={goToNext}>
          &#10095;
        </button>
      </div>
      <div className="carousel-dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={`dot ${currentIndex === index ? 'active' : ''}`}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
};

export default ImageCarousel;
```
## imageCarousel.css
```
body {
  margin: 0;
  padding: 0;
  font-family: 'Inter', sans-serif;
  height: 100vh;
  display: flex;
  justify-content: center; /* horizontal center */
  align-items: center;     /* vertical center */
  background: #f0f4f8;
}

.carousel-container {
  max-width: 800px;
  width: 100%;
  position: relative;
  text-align: center;
}

.carousel-wrapper {
  position: relative;
  overflow: hidden;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-image {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 2rem;
  background: rgba(0,0,0,0.3);
  color: #fff;
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  border-radius: 50%;
  user-select: none;
  z-index: 2;
}

.arrow.left {
  left: 10px;
}

.arrow.right {
  right: 10px;
}

.arrow:hover {
  background: rgba(0,0,0,0.6);
}

.carousel-dots {
  margin-top: 10px;
}

.dot {
  height: 12px;
  width: 12px;
  margin: 0 4px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dot.active {
  background-color: #717171;
}
```
## App.jsx
```
import React from 'react';
import ImageCarousel from './imageCarousel';

function App() {
  return (
    <div>
      <h1 style={{textAlign: 'center', marginTop: '1rem'}}>React Image Carousel</h1>
      <ImageCarousel autoPlay={true} interval={4000} />
    </div>
  );
}

export default App;
```
## main.jsx
```
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)

```




## OUTPUT

<img width="843" height="853" alt="Screenshot 2025-10-24 162123" src="https://github.com/user-attachments/assets/c45a2506-61e7-4746-8c88-1b4c9cae8c42" />
<img width="1920" height="1080" alt="Screenshot 2025-10-24 161729" src="https://github.com/user-attachments/assets/d43a26f9-533c-498e-94a3-838b6b747950" />
<img width="1920" height="1080" alt="Screenshot 2025-10-24 161803" src="https://github.com/user-attachments/assets/94734255-2c9d-4316-acd1-4ca056d96ea7" />



## RESULT
The program for creating Image Carousel using React is executed successfully.
