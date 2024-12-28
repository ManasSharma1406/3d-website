# 3d-website


# Scroll-Based Image Sequence Animation

## Overview
This project implements a smooth scroll-based image sequence animation using GSAP's ScrollTrigger and Locomotive Scroll. It creates a canvas-based animation that responds to user scrolling, displaying a sequence of images in a fluid motion.

## Features
- Smooth scrolling implementation using Locomotive Scroll
- Canvas-based image sequence animation
- Responsive design that adapts to window resizing
- Synchronized scrolling with GSAP ScrollTrigger
- Image sequence preloading for smooth playback

## Dependencies
- GSAP (GreenSock Animation Platform)
- ScrollTrigger Plugin
- Locomotive Scroll
- Modern web browser with canvas support

## Setup

### 1. Include Required Libraries
```html
<!-- Add these in your HTML file -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.x.x/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.x.x/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/locomotive-scroll@4.1.4/dist/locomotive-scroll.min.js"></script>
```

### 2. HTML Structure
```html
<div id="main">
    <div id="page">
        <canvas></canvas>
    </div>
</div>
```

### 3. Image Sequence
- Place your image sequence in a directory
- Images should be numbered sequentially (1.webp, 2.webp, etc.)
- Current setup supports 118 frames in WebP format

## Configuration

### Scroll Settings
- The animation is set to span 300% of the viewport height
- Scroll smoothness can be adjusted in the Locomotive Scroll initialization
- ScrollTrigger scrub value is set to 0.15 for smooth animation playback

### Canvas Sizing
The canvas automatically resizes to match the window dimensions:
- Width: 100% of window width
- Height: 100% of window height

## Usage

1. Initialize Locomotive Scroll:
```javascript
const locoScroll = new LocomotiveScroll({
    el: document.querySelector("#main"),
    smooth: true
});
```

2. Set up ScrollTrigger proxy:
```javascript
ScrollTrigger.scrollerProxy("#main", {
    scrollTop(value) {
        return arguments.length ? locoScroll.scrollTo(value, 0, 0) : locoScroll.scroll.instance.scroll.y;
    },
    getBoundingClientRect() {
        return { top: 0, left: 0, width: window.innerWidth, height: window.innerHeight };
    },
    pinType: document.querySelector("#main").style.transform ? "transform" : "fixed"
});
```

## Customization

### Image Sequence
To modify the image sequence:
1. Update the `files()` function with your image paths
2. Adjust the `frameCount` constant to match your number of frames
3. Update the scroll length by modifying the `end` value in ScrollTrigger settings

### Animation Timing
Adjust the animation smoothness by modifying:
- ScrollTrigger's `scrub` value (currently 0.15)
- Locomotive Scroll's `smooth` settings

## Browser Support
- Requires a modern browser with canvas support
- WebP image format support required
- JavaScript enabled

## Performance Considerations
- Images are preloaded for smooth playback
- Canvas scaling is optimized for different screen sizes
- Locomotive Scroll is optimized for mobile devices

## Troubleshooting
- If images don't load, check the file paths in the `files()` function
- If scrolling isn't smooth, adjust the `scrub` value in ScrollTrigger configuration
- For mobile performance issues, verify the `pinType` setting in ScrollTrigger proxy
