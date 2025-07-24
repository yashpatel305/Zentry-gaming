# API Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Core Components](#core-components)
3. [Utility Components](#utility-components)
4. [Animation Features](#animation-features)
5. [Usage Examples](#usage-examples)
6. [API Reference](#api-reference)

## Project Overview

**Zentry Gaming** is a modern React application built with Vite, featuring immersive gaming content with advanced animations powered by GSAP (GreenSock Animation Platform). The application showcases a gaming platform with multiple sections including hero, about, features, story, and contact pages.

### Tech Stack
- **Frontend Framework**: React 19.1.0
- **Build Tool**: Vite 7.0.4
- **Animation Library**: GSAP 3.13.0 with ScrollTrigger
- **Styling**: Tailwind CSS 3.4.3
- **Icons**: React Icons 5.5.0
- **Deployment**: GitHub Pages

### Key Features
- Responsive design with mobile-first approach
- Advanced GSAP animations and scroll-triggered effects
- Interactive video elements with smooth transitions
- Audio controls with visual indicators
- 3D tilt effects and hover interactions
- Smooth navigation with floating navbar

---

## Core Components

### 1. App Component

**File**: `src/App.jsx`

The main application component that orchestrates the layout and renders all sections.

```jsx
import App from './App.jsx'

// Usage
<App />
```

**Structure**:
- Renders navigation, hero, about, features, story, contact, and footer sections
- Uses a responsive layout with overflow handling
- Provides the main container for all content

---

### 2. Hero Component

**File**: `src/components/Hero.jsx`

An immersive hero section with interactive video elements and smooth transitions.

#### Props
This component doesn't accept props - it's a self-contained section.

#### Features
- **Video Cycling**: Displays 4 different hero videos with smooth transitions
- **Interactive Mini Video**: Click to trigger video transitions with GSAP animations
- **Loading State**: Shows a custom loading animation while videos load
- **Scroll Animations**: Implements scroll-triggered clip-path animations

#### State Management
```jsx
const [currentIndex, setCurrentIndex] = useState(1);
const [hasClicked, setHasClicked] = useState(false);
const [isLoading, setIsLoading] = useState(true);
const [loadedVideos, setLoadedVideos] = useState(0);
```

#### Key Methods
- `handleVideoLoad()`: Tracks video loading progress
- `handleMiniVdClick()`: Triggers video transition animations
- `getVideosrc(index)`: Returns video source path

#### Usage Example
```jsx
import Hero from './components/Hero'

function App() {
  return (
    <div>
      <Hero />
    </div>
  )
}
```

#### Required Assets
- Video files: `videos/hero-1.mp4` through `videos/hero-4.mp4`
- Loading animation CSS (three-body loader)

---

### 3. Navbar Component

**File**: `src/components/Navbar.jsx`

A responsive navigation bar with scroll-based visibility and audio controls.

#### Features
- **Auto-hide/Show**: Navbar visibility based on scroll direction
- **Floating Effect**: Transforms to floating style when scrolling
- **Audio Control**: Toggle background music with visual indicator
- **Responsive Menu**: Adaptive layout for mobile and desktop

#### State Management
```jsx
const [isAudioPlaying, setIsAudioPlaying] = useState(false)
const [isIndicatorActive, setIsIndicatorActive] = useState(false)
const [lastScrollY, setLastScrollY] = useState(0)
const [isNavVisible, setIsNavVisible] = useState(true)
```

#### Navigation Items
```jsx
const navItems = ['Nexus','Vault','Prologue','About', 'Contact'];
```

#### Key Methods
- `toggleAudioIndicator()`: Controls audio playback state
- Auto-scroll detection with `useWindowScroll()` hook

#### Usage Example
```jsx
import Navbar from './components/Navbar'

function App() {
  return (
    <div>
      <Navbar />
      {/* Other content */}
    </div>
  )
}
```

#### Required Assets
- Logo: `img/logo.png`
- Audio file: `audio/loop.mp3`

---

### 4. About Component

**File**: `src/components/About.jsx`

A section showcasing the platform's mission with scroll-triggered animations.

#### Features
- **Scroll-Triggered Animation**: Expanding clip-path effect on scroll
- **Pinned Animation**: Content pins during scroll animation
- **Responsive Layout**: Adapts to different screen sizes

#### Key Animation
```jsx
const clipAnimation = gsap.timeline({
  scrollTrigger: {
    trigger: '#clip',
    start: 'center center',
    end: '+=800 center',
    scrub: 0.5,
    pin: true,
    pinSpacing: true,
  }
});
```

#### Usage Example
```jsx
import About from './components/About'

function App() {
  return (
    <div>
      <About />
    </div>
  )
}
```

#### Required Assets
- Background image: `img/about.webp`

---

### 5. Features Component

**File**: `src/components/Features.jsx`

Interactive features showcase with 3D tilt effects and video backgrounds.

#### Subcomponents

##### BentoTilt
A wrapper component that adds 3D tilt effects on mouse interaction.

**Props**:
- `children` (ReactNode): Content to wrap
- `className` (string, optional): Additional CSS classes

**Usage**:
```jsx
<BentoTilt className="custom-class">
  <div>Your content here</div>
</BentoTilt>
```

##### BentoCard
A card component for displaying feature content with video backgrounds.

**Props**:
- `src` (string): Video source URL
- `title` (ReactNode): Card title (supports JSX)
- `description` (string, optional): Card description

**Usage**:
```jsx
<BentoCard
  src="videos/feature-1.mp4"
  title={<>radia<b>n</b>t</>}
  description="A cross-platform metagame app..."
/>
```

#### Features Showcase
The component displays 5 main features:
1. **Radiant**: Cross-platform metagame app
2. **Zigma**: Anime and gaming-inspired NFT collection
3. **Nexus**: Gamified social hub
4. **Azul**: Cross-world AI Agent
5. **More Coming Soon**: Placeholder for future features

#### Usage Example
```jsx
import Features from './components/Features'

function App() {
  return (
    <div>
      <Features />
    </div>
  )
}
```

#### Required Assets
- Video files: `videos/feature-1.mp4` through `videos/feature-5.mp4`

---

### 6. Story Component

**File**: `src/components/Story.jsx`

An interactive story section with 3D image manipulation effects.

#### Features
- **3D Mouse Interaction**: Image rotates based on mouse movement
- **Smooth Animations**: GSAP-powered rotation effects
- **Responsive Design**: Adapts to different screen sizes

#### Key Methods
```jsx
const handleMouseMove = (e) => {
  // Calculates rotation based on mouse position
  const rotateX = ((y - centerY) / centerY) * 10;
  const rotateY = ((x - centerX) / centerX) * -10;
  
  gsap.to(element, {
    duration: 0.3,
    rotateX,
    rotateY,
    transformPerspective: 500,
    ease: 'power1.inOut'
  })
}

const handleMouseLeave = () => {
  // Resets rotation to default
  gsap.to(element, {
    duration: 0.3,
    rotateX: 0,
    rotateY: 0,
    ease: 'power1.inOut'
  })
}
```

#### Usage Example
```jsx
import Story from './components/Story'

function App() {
  return (
    <div>
      <Story />
    </div>
  )
}
```

#### Required Assets
- Story image: `img/entrance.webp`

---

### 7. Contact Component

**File**: `src/components/Contact.jsx`

Contact section with decorative image elements and call-to-action.

#### Subcomponents

##### ImageClipBox
A utility component for displaying images with custom clip paths.

**Props**:
- `src` (string): Image source URL
- `clipClass` (string): CSS class for clip-path styling

**Usage**:
```jsx
<ImageClipBox
  clipClass="contact-clip-path-1"
  src="img/contact-1.webp"
/>
```

#### Usage Example
```jsx
import Contact from './components/Contact'

function App() {
  return (
    <div>
      <Contact />
    </div>
  )
}
```

#### Required Assets
- Contact images: `img/contact-1.webp`, `img/contact-2.webp`
- Swordman images: `img/swordman-partial.webp`, `img/swordman.webp`

---

### 8. Footer Component

**File**: `src/components/Footer.jsx`

Simple footer component with copyright information.

#### Usage Example
```jsx
import Footer from './components/Footer'

function App() {
  return (
    <div>
      {/* Other content */}
      <Footer />
    </div>
  )
}
```

---

## Utility Components

### 1. Button Component

**File**: `src/components/Button.jsx`

A reusable button component with icon support and custom styling.

#### Props
- `title` (string): Button text
- `id` (string, optional): HTML id attribute
- `rightIcon` (ReactElement, optional): Icon to display on the right
- `leftIcon` (ReactElement, optional): Icon to display on the left
- `containerClass` (string, optional): Additional CSS classes

#### Usage Examples
```jsx
import Button from './components/Button'
import { TiLocationArrow } from 'react-icons/ti'

// Basic button
<Button title="Click me" />

// Button with left icon
<Button 
  title="Watch Trailer" 
  leftIcon={<TiLocationArrow />}
  containerClass="bg-yellow-300 flex-center gap-1"
/>

// Button with right icon
<Button 
  title="Products" 
  rightIcon={<TiLocationArrow />}
  containerClass="bg-blue-50 md:flex hidden items-center justify-center gap-1"
/>

// Button with custom styling and ID
<Button 
  id="contact-button"
  title="Contact Us" 
  containerClass="mt-10 cursor-pointer"
/>
```

#### Styling Features
- Responsive design with hover effects
- Support for custom background colors via `containerClass`
- Consistent typography with uppercase text styling
- Overflow handling for smooth animations

---

### 2. AnimatedTitle Component

**File**: `src/components/AnimatedTitle.jsx`

A component for creating scroll-triggered animated titles with word-by-word reveal effects.

#### Props
- `title` (string): Title text (supports HTML tags and `<br />` for line breaks)
- `containerClass` (string, optional): Additional CSS classes for the container

#### Features
- **Scroll-Triggered Animation**: Words animate in on scroll
- **Staggered Animation**: Each word animates with a slight delay
- **3D Transform Effects**: Words start rotated and transform to normal position
- **HTML Support**: Supports bold tags and line breaks

#### Usage Examples
```jsx
import AnimatedTitle from './components/AnimatedTitle'

// Basic animated title
<AnimatedTitle 
  title="Welcome to <b>Z</b>entry"
  containerClass="text-center"
/>

// Multi-line title with line breaks
<AnimatedTitle
  title="Disc<b>o</b>ver the world's <br /> largest shared <b>a</b>dventure"
  containerClass="mt-5 !text-black text-center tracking-wide"
/>

// Title for dark backgrounds
<AnimatedTitle
  title="the st<b>o</b>ry of <br /> a hidden real<b>m</b>"
  containerClass="mt-5 pointer-events-none mix-blend-difference relative z-10 tracking-wide"
/>
```

#### Animation Details
- **Trigger**: Starts when element is 100px from bottom of viewport
- **Stagger**: 0.03s delay between each word
- **Transform**: 3D rotation with translate effects
- **Easing**: `power2.inOut` for smooth animation

---

### 3. RoundedCorners Component

**File**: `src/components/RoundedCorners.jsx`

A utility component that provides SVG filter definitions for advanced visual effects.

#### Features
- **Gaussian Blur Filter**: Creates blur effects for enhanced visuals
- **Color Matrix**: Adjusts color properties for filter effects
- **Composite Operations**: Combines multiple filter effects

#### Usage Example
```jsx
import RoundedCorners from './components/RoundedCorners'

function Story() {
  return (
    <div className="story-container">
      {/* Your content */}
      <RoundedCorners />
    </div>
  )
}
```

#### Filter Definition
```jsx
<filter id="flt_tag">
  <feGaussianBlur in="SourceGraphic" stdDeviation="8" result="blur" />
  <feColorMatrix
    in="blur"
    mode="matrix"
    values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9"
    result="flt_tag"
  />
  <feComposite in="SourceGraphic" in2="flt_tag" operator="atop" />
</filter>
```

---

## Animation Features

### GSAP Integration

The application makes extensive use of GSAP for high-performance animations:

#### Key GSAP Features Used
1. **ScrollTrigger**: Scroll-based animations
2. **Timeline**: Complex animation sequences
3. **Transform**: 3D rotations and scaling
4. **Clip-path**: Advanced masking effects

#### Common Animation Patterns

##### Scroll-Triggered Fade In
```jsx
gsap.to('.animated-word', {
  opacity: 1,
  transform: 'translate3d(0,0,0) rotateY(0deg) rotateX(0deg)',
  ease: 'power2.inOut',
  stagger: 0.03,
})
```

##### 3D Mouse Interaction
```jsx
gsap.to(element, {
  duration: 0.3,
  rotateX: calculatedRotateX,
  rotateY: calculatedRotateY,
  transformPerspective: 500,
  ease: 'power1.inOut'
})
```

##### Clip-path Animation
```jsx
gsap.from('#video-frame', {
  clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
  borderRadius: '0 0 0 0',
  ease: 'power1.inOut',
  scrollTrigger: {
    trigger: '#video-frame',
    start: 'center center',
    end: 'bottom center',
    scrub: true,
  }
})
```

### Custom CSS Animations

#### Loading Animation
```css
.three-body {
  /* Custom loading spinner with three dots */
}
```

#### Audio Indicator
```css
.indicator-line {
  /* Animated bars for audio visualization */
}
```

---

## Usage Examples

### Basic Setup

1. **Install Dependencies**
```bash
npm install
```

2. **Start Development Server**
```bash
npm run dev
```

3. **Build for Production**
```bash
npm run build
```

### Component Integration

```jsx
import React from 'react'
import Hero from './components/Hero'
import About from './components/About'
import Navbar from './components/Navbar'
import Features from './components/Features'
import Story from './components/Story'
import Contact from './components/Contact'
import Footer from './components/Footer'

const App = () => {
  return (
    <main className="relative min-h-screen w-screen overflow-x-hidden">
      <Navbar />
      <Hero />
      <About />
      <Features />
      <Story />
      <Contact />
      <Footer />
    </main>
  )
}

export default App
```

### Custom Animation Implementation

```jsx
import { useGSAP } from '@gsap/react'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/all'

gsap.registerPlugin(ScrollTrigger)

const CustomAnimatedComponent = () => {
  useGSAP(() => {
    gsap.from('.animate-element', {
      y: 50,
      opacity: 0,
      duration: 1,
      stagger: 0.1,
      scrollTrigger: {
        trigger: '.animate-element',
        start: 'top 80%',
        end: 'bottom 20%',
        toggleActions: 'play none none reverse'
      }
    })
  })

  return (
    <div className="container">
      <div className="animate-element">Item 1</div>
      <div className="animate-element">Item 2</div>
      <div className="animate-element">Item 3</div>
    </div>
  )
}
```

---

## API Reference

### Core Hooks and Utilities

#### useGSAP Hook
```jsx
import { useGSAP } from '@gsap/react'

useGSAP(() => {
  // Animation code here
}, { dependencies: [dependency], revertOnUpdate: true })
```

#### useWindowScroll Hook
```jsx
import { useWindowScroll } from 'react-use'

const { y: currentScrollY } = useWindowScroll()
```

### Common Props Interface

#### ButtonProps
```typescript
interface ButtonProps {
  title: string
  id?: string
  rightIcon?: ReactElement
  leftIcon?: ReactElement
  containerClass?: string
}
```

#### AnimatedTitleProps
```typescript
interface AnimatedTitleProps {
  title: string
  containerClass?: string
}
```

#### BentoTiltProps
```typescript
interface BentoTiltProps {
  children: ReactNode
  className?: string
}
```

#### BentoCardProps
```typescript
interface BentoCardProps {
  src: string
  title: ReactNode
  description?: string
}
```

### Required Assets Structure

```
public/
├── img/
│   ├── logo.png
│   ├── about.webp
│   ├── entrance.webp
│   ├── contact-1.webp
│   ├── contact-2.webp
│   ├── swordman-partial.webp
│   └── swordman.webp
├── videos/
│   ├── hero-1.mp4
│   ├── hero-2.mp4
│   ├── hero-3.mp4
│   ├── hero-4.mp4
│   ├── feature-1.mp4
│   ├── feature-2.mp4
│   ├── feature-3.mp4
│   ├── feature-4.mp4
│   └── feature-5.mp4
├── audio/
│   └── loop.mp3
└── fonts/
    ├── circularweb-book.woff2
    ├── general.woff2
    ├── robert-medium.woff2
    ├── robert-regular.woff2
    └── zentry-regular.woff2
```

### Performance Considerations

1. **Video Optimization**: Ensure video files are optimized for web delivery
2. **Image Formats**: Use WebP format for better compression
3. **Font Loading**: Implement proper font loading strategies
4. **Animation Performance**: Use GSAP's performance optimization features
5. **Responsive Assets**: Provide different asset sizes for various screen sizes

### Browser Compatibility

- **Modern Browsers**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Mobile Support**: iOS Safari 14+, Chrome Mobile 90+
- **Required Features**: ES6 modules, CSS Grid, Flexbox, Custom Properties

---

## Best Practices

### Component Development
1. Use functional components with hooks
2. Implement proper prop validation
3. Keep components focused on single responsibilities
4. Use meaningful component and prop names

### Animation Guidelines
1. Use GSAP for complex animations
2. Implement proper cleanup in useEffect
3. Consider performance impact of animations
4. Test animations on various devices

### Accessibility
1. Provide proper alt texts for images
2. Ensure keyboard navigation support
3. Implement proper ARIA labels
4. Consider reduced motion preferences

### Performance
1. Optimize asset loading
2. Implement lazy loading for heavy content
3. Use proper caching strategies
4. Monitor bundle size and performance metrics

---

This documentation provides a comprehensive guide to all public APIs, components, and features in the Zentry Gaming application. Each component is designed to be reusable and well-documented for easy integration and maintenance.