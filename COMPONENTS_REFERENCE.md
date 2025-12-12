# Components Quick Reference

## Core Components

### Hero
```jsx
import Hero from './components/Hero'

// Usage - No props required
<Hero />

// Features:
// - Interactive video carousel (4 videos)
// - Click mini-video to transition
// - Loading state with custom spinner
// - Scroll-triggered clip-path animations
```

### Navbar
```jsx
import Navbar from './components/Navbar'

// Usage - No props required  
<Navbar />

// Features:
// - Auto-hide/show on scroll
// - Floating effect when scrolling
// - Audio control with visual indicator
// - Responsive navigation menu
```

### About
```jsx
import About from './components/About'

// Usage - No props required
<About />

// Features:
// - Scroll-triggered clip animation
// - Pinned section during animation
// - Animated title integration
```

### Features
```jsx
import Features from './components/Features'

// Usage - No props required
<Features />

// Subcomponents:
// - BentoTilt: 3D tilt wrapper
// - BentoCard: Video background cards
```

### Story
```jsx
import Story from './components/Story'

// Usage - No props required
<Story />

// Features:
// - 3D mouse interaction effects
// - Image rotation based on cursor
// - Smooth GSAP animations
```

### Contact
```jsx
import Contact from './components/Contact'

// Usage - No props required
<Contact />

// Subcomponents:
// - ImageClipBox: Custom clipped images
```

### Footer
```jsx
import Footer from './components/Footer'

// Usage - No props required
<Footer />

// Simple copyright footer
```

---

## Utility Components

### Button
```jsx
import Button from './components/Button'
import { TiLocationArrow } from 'react-icons/ti'

// Basic button
<Button title="Click me" />

// With icons
<Button 
  title="Watch Trailer" 
  leftIcon={<TiLocationArrow />}
  containerClass="bg-yellow-300 flex-center gap-1"
/>

<Button 
  title="Products" 
  rightIcon={<TiLocationArrow />}
  containerClass="bg-blue-50"
/>

// With ID and custom styling
<Button 
  id="contact-btn"
  title="Contact Us" 
  containerClass="mt-10 cursor-pointer"
/>
```

**Props:**
- `title` (string) - Button text
- `id` (string, optional) - HTML id
- `leftIcon` (ReactElement, optional) - Left icon
- `rightIcon` (ReactElement, optional) - Right icon  
- `containerClass` (string, optional) - Additional CSS

### AnimatedTitle
```jsx
import AnimatedTitle from './components/AnimatedTitle'

// Basic usage
<AnimatedTitle 
  title="Welcome to <b>Z</b>entry"
  containerClass="text-center"
/>

// Multi-line with breaks
<AnimatedTitle
  title="Disc<b>o</b>ver the world's <br /> largest shared <b>a</b>dventure"
  containerClass="mt-5 !text-black text-center tracking-wide"
/>

// For dark backgrounds
<AnimatedTitle
  title="the st<b>o</b>ry of <br /> a hidden real<b>m</b>"
  containerClass="mt-5 pointer-events-none mix-blend-difference relative z-10"
/>
```

**Props:**
- `title` (string) - Title with HTML support
- `containerClass` (string, optional) - Container styling

### RoundedCorners
```jsx
import RoundedCorners from './components/RoundedCorners'

// Add to components that need SVG filters
<div className="story-container">
  {/* Your content */}
  <RoundedCorners />
</div>
```

---

## Subcomponents (Features)

### BentoTilt
```jsx
// Used within Features component
<BentoTilt className="custom-tilt-class">
  <div>Your content with 3D tilt effect</div>
</BentoTilt>
```

**Props:**
- `children` (ReactNode) - Content to wrap
- `className` (string, optional) - Additional CSS

### BentoCard
```jsx
// Used within BentoTilt in Features
<BentoCard
  src="videos/feature-1.mp4"
  title={<>radia<b>n</b>t</>}
  description="A cross-platform metagame app turning your activities into rewards."
/>
```

**Props:**
- `src` (string) - Video source URL
- `title` (ReactNode) - Card title (supports JSX)
- `description` (string, optional) - Card description

### ImageClipBox (Contact)
```jsx
// Used within Contact component
<ImageClipBox
  clipClass="contact-clip-path-1"
  src="img/contact-1.webp"
/>
```

**Props:**
- `src` (string) - Image source URL
- `clipClass` (string) - CSS class for clip styling

---

## Animation Patterns

### Basic GSAP Setup
```jsx
import { useGSAP } from '@gsap/react'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/all'

gsap.registerPlugin(ScrollTrigger)

const Component = () => {
  useGSAP(() => {
    // Your animations here
  }, { dependencies: [] })
}
```

### Scroll Triggered Animation
```jsx
useGSAP(() => {
  gsap.from('.element', {
    opacity: 0,
    y: 50,
    duration: 1,
    scrollTrigger: {
      trigger: '.element',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  })
})
```

### 3D Mouse Interaction
```jsx
const handleMouseMove = (e) => {
  const { left, top, width, height } = ref.current.getBoundingClientRect()
  const x = (e.clientX - left) / width
  const y = (e.clientY - top) / height
  
  const rotateX = (y - 0.5) * 10
  const rotateY = (x - 0.5) * -10
  
  gsap.to(ref.current, {
    rotateX, rotateY,
    transformPerspective: 500,
    duration: 0.3,
    ease: 'power1.inOut'
  })
}
```

---

## Common CSS Classes

### Layout Utilities
```css
.absolute-center     /* Absolute center positioning */
.flex-center        /* Flex center alignment */
.border-hsla        /* Semi-transparent border */
.mask-clip-path     /* Basic clip path */
```

### Animation Classes
```css
.hero-heading       /* Large responsive heading */
.nav-hover-btn      /* Navbar button with underline effect */
.floating-nav       /* Floating navigation style */
.animated-title     /* Container for animated titles */
.animated-word      /* Individual animated words */
```

### Component Specific
```css
.bento-tilt_1       /* Bento grid item span 2 */
.bento-tilt_2       /* Bento grid item span 1 */
.about-subtext      /* About section description */
.about-image        /* About section image container */
```

---

## Asset Requirements

### Images (public/img/)
- `logo.png` - Navigation logo
- `about.webp` - About section background
- `entrance.webp` - Story section image
- `contact-1.webp`, `contact-2.webp` - Contact decorative images
- `swordman-partial.webp`, `swordman.webp` - Contact character images

### Videos (public/videos/)
- `hero-1.mp4` through `hero-4.mp4` - Hero carousel videos
- `feature-1.mp4` through `feature-5.mp4` - Feature showcase videos

### Audio (public/audio/)
- `loop.mp3` - Background music for navbar audio control

### Fonts (public/fonts/)
- `zentry-regular.woff2` - Main brand font
- `general.woff2` - General text font
- `circular-web-book.woff2` - Body text font
- `robert-medium.woff2`, `robert-regular.woff2` - Accent fonts

---

## Responsive Breakpoints

```css
/* Tailwind CSS breakpoints used throughout */
sm: 640px   /* Small devices */
md: 768px   /* Medium devices */
lg: 1024px  /* Large devices */
xl: 1280px  /* Extra large devices */
2xl: 1536px /* 2X large devices */
```

---

## Performance Tips

1. **Preload critical assets** in Hero component
2. **Use `will-change: transform`** for animated elements
3. **Implement proper video loading states**
4. **Batch GSAP operations** when possible
5. **Use hardware acceleration** with `transform3d`

---

This reference provides quick access to all component APIs and common usage patterns for the Zentry Gaming application.