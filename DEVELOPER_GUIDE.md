# Developer Guide

## Quick Start

### Prerequisites
- Node.js 16+ 
- npm or yarn package manager
- Modern web browser with ES6+ support

### Installation & Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd zentry-gaming
```

2. **Install dependencies**
```bash
npm install
```

3. **Start development server**
```bash
npm run dev
```

4. **Open in browser**
Navigate to `http://localhost:5173`

### Available Scripts

```bash
# Development
npm run dev          # Start development server with HMR
npm run build        # Build for production
npm run preview      # Preview production build locally
npm run lint         # Run ESLint
npm run deploy       # Deploy to GitHub Pages

# Deployment
npm run predeploy    # Build before deployment
npm run deploy       # Deploy to GitHub Pages
```

---

## Project Structure

```
src/
├── components/           # React components
│   ├── About.jsx        # About section component
│   ├── AnimatedTitle.jsx # Reusable animated title
│   ├── Button.jsx       # Reusable button component
│   ├── Contact.jsx      # Contact section component
│   ├── Features.jsx     # Features showcase component
│   ├── Footer.jsx       # Footer component
│   ├── Hero.jsx         # Hero section with video
│   ├── Navbar.jsx       # Navigation component
│   ├── RoundedCorners.jsx # SVG filter utility
│   └── Story.jsx        # Story section component
├── App.jsx              # Main app component
├── main.jsx             # Application entry point
└── index.css            # Global styles and utilities

public/
├── img/                 # Static images
├── videos/              # Video assets
├── audio/               # Audio files
├── fonts/               # Custom font files
└── index.html           # HTML template

config files:
├── package.json         # Dependencies and scripts
├── vite.config.js       # Vite configuration
├── tailwind.config.js   # Tailwind CSS configuration
├── postcss.config.js    # PostCSS configuration
└── eslint.config.js     # ESLint configuration
```

---

## Technical Architecture

### State Management Pattern

The application uses React's built-in state management with hooks:

```jsx
// Local component state
const [currentIndex, setCurrentIndex] = useState(1);
const [hasClicked, setHasClicked] = useState(false);

// Refs for DOM manipulation
const nextVideoRef = useRef(null);
const navContainerRef = useRef(null);

// Custom hooks for external state
const { y: currentScrollY } = useWindowScroll();
```

### Animation System

#### GSAP Integration Pattern
```jsx
import { useGSAP } from '@gsap/react';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/all';

// Register plugins
gsap.registerPlugin(ScrollTrigger);

const Component = () => {
  useGSAP(() => {
    // Animation code with automatic cleanup
    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: '.element',
        start: 'top bottom',
        end: 'bottom top',
        scrub: 1
      }
    });
    
    tl.to('.element', { opacity: 1, duration: 1 });
  }, { dependencies: [someDependency] });
};
```

#### Performance Optimizations
- Use `will-change` CSS property for animated elements
- Implement proper cleanup in `useGSAP`
- Use `gsap.set()` for initial states
- Leverage hardware acceleration with `transform3d`

---

## Component Development Guidelines

### Component Structure Template

```jsx
import React, { useState, useRef, useEffect } from 'react';
import { useGSAP } from '@gsap/react';
import gsap from 'gsap';

const ComponentName = ({ prop1, prop2, ...props }) => {
  // State declarations
  const [localState, setLocalState] = useState(initialValue);
  
  // Refs
  const elementRef = useRef(null);
  
  // GSAP animations
  useGSAP(() => {
    // Animation logic
  }, { dependencies: [localState] });
  
  // Effect hooks
  useEffect(() => {
    // Side effects
  }, [dependencies]);
  
  // Event handlers
  const handleEvent = () => {
    // Handler logic
  };
  
  return (
    <div ref={elementRef} {...props}>
      {/* Component JSX */}
    </div>
  );
};

export default ComponentName;
```

### Props Pattern

```jsx
// Define prop interfaces for TypeScript-like documentation
/**
 * @typedef {Object} ComponentProps
 * @property {string} title - The component title
 * @property {ReactNode} [children] - Optional children elements
 * @property {string} [className] - Additional CSS classes
 * @property {Function} [onClick] - Click handler function
 */

const Component = ({ title, children, className = '', onClick }) => {
  return (
    <div 
      className={`base-styles ${className}`}
      onClick={onClick}
    >
      <h2>{title}</h2>
      {children}
    </div>
  );
};
```

---

## Animation Recipes

### Scroll-Triggered Animations

#### Basic Fade In
```jsx
useGSAP(() => {
  gsap.from('.fade-in', {
    opacity: 0,
    y: 50,
    duration: 1,
    scrollTrigger: {
      trigger: '.fade-in',
      start: 'top 80%',
      toggleActions: 'play none none reverse'
    }
  });
});
```

#### Staggered Animation
```jsx
useGSAP(() => {
  gsap.from('.stagger-item', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    stagger: 0.1,
    scrollTrigger: {
      trigger: '.stagger-container',
      start: 'top 75%'
    }
  });
});
```

#### Pinned Section with Scrub
```jsx
useGSAP(() => {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: '.pinned-section',
      start: 'top top',
      end: '+=1000',
      scrub: 1,
      pin: true
    }
  });
  
  tl.to('.animated-element', { scale: 2, rotation: 360 });
});
```

### Mouse Interaction Animations

#### 3D Tilt Effect
```jsx
const handleMouseMove = (e) => {
  if (!elementRef.current) return;
  
  const { left, top, width, height } = elementRef.current.getBoundingClientRect();
  const x = (e.clientX - left) / width;
  const y = (e.clientY - top) / height;
  
  const rotateX = (y - 0.5) * 20;
  const rotateY = (x - 0.5) * -20;
  
  gsap.to(elementRef.current, {
    rotateX,
    rotateY,
    transformPerspective: 1000,
    duration: 0.3,
    ease: 'power2.out'
  });
};

const handleMouseLeave = () => {
  gsap.to(elementRef.current, {
    rotateX: 0,
    rotateY: 0,
    duration: 0.5,
    ease: 'power2.out'
  });
};
```

#### Magnetic Button Effect
```jsx
const handleMouseMove = (e) => {
  const { left, top, width, height } = buttonRef.current.getBoundingClientRect();
  const centerX = left + width / 2;
  const centerY = top + height / 2;
  
  const deltaX = e.clientX - centerX;
  const deltaY = e.clientY - centerY;
  const distance = Math.sqrt(deltaX ** 2 + deltaY ** 2);
  
  if (distance < 100) {
    const strength = (100 - distance) / 100;
    gsap.to(buttonRef.current, {
      x: deltaX * strength * 0.3,
      y: deltaY * strength * 0.3,
      duration: 0.3
    });
  }
};
```

---

## Styling Guidelines

### Tailwind CSS Custom Utilities

The project extends Tailwind with custom utilities in `src/index.css`:

```css
@layer utilities {
  /* Border utilities */
  .border-hsla {
    @apply border border-white/20;
  }
  
  /* Layout utilities */
  .absolute-center {
    @apply absolute top-1/2 left-1/2 translate-x-[-50%] translate-y-[-50%];
  }
  
  .flex-center {
    @apply flex justify-center items-center;
  }
  
  /* Animation utilities */
  .mask-clip-path {
    clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
  }
  
  /* Typography utilities */
  .special-font b {
    font-family: "Zentry";
    font-feature-settings: "ss01" on;
  }
}
```

### Component-Specific Styles

```css
/* Navigation styles */
.nav-hover-btn {
  @apply relative ms-10 font-general text-xs uppercase text-blue-50 
         after:absolute after:-bottom-0.5 after:left-0 after:h-[2px] 
         after:w-full after:origin-bottom-right after:scale-x-0 
         after:bg-neutral-800 after:transition-transform after:duration-300 
         after:ease-[cubic-bezier(0.65_0.05_0.36_1)] 
         hover:after:origin-bottom-left hover:after:scale-x-100;
}

/* Floating navigation */
.floating-nav {
  @apply bg-black rounded-lg border;
}

/* Hero styles */
.hero-heading {
  @apply uppercase font-zentry font-black text-5xl 
         sm:right-10 sm:text-7xl md:text-9xl lg:text-[12rem];
}
```

### Responsive Design Patterns

```jsx
// Mobile-first responsive classes
<div className="
  w-full px-4 
  sm:px-6 sm:max-w-2xl 
  md:px-8 md:max-w-4xl 
  lg:px-12 lg:max-w-6xl 
  xl:px-16 xl:max-w-7xl
">
  Content
</div>

// Responsive grid
<div className="
  grid grid-cols-1 gap-4
  md:grid-cols-2 md:gap-6
  lg:grid-cols-3 lg:gap-8
">
  {items.map(item => <GridItem key={item.id} {...item} />)}
</div>
```

---

## Performance Optimization

### Code Splitting

```jsx
import { lazy, Suspense } from 'react';

// Lazy load heavy components
const HeavyComponent = lazy(() => import('./HeavyComponent'));

const App = () => (
  <Suspense fallback={<LoadingSpinner />}>
    <HeavyComponent />
  </Suspense>
);
```

### Asset Optimization

```jsx
// Preload critical assets
useEffect(() => {
  const preloadAssets = [
    'videos/hero-1.mp4',
    'img/about.webp',
    'audio/loop.mp3'
  ];
  
  preloadAssets.forEach(asset => {
    const link = document.createElement('link');
    link.rel = 'preload';
    link.href = asset;
    link.as = asset.includes('.mp4') ? 'video' : 
              asset.includes('.mp3') ? 'audio' : 'image';
    document.head.appendChild(link);
  });
}, []);
```

### GSAP Performance

```jsx
// Use GSAP's performance optimizations
gsap.config({
  force3D: true,        // Force hardware acceleration
  nullTargetWarn: false // Disable warnings for performance
});

// Batch DOM reads and writes
useGSAP(() => {
  const elements = gsap.utils.toArray('.animate');
  
  // Batch read operations
  const positions = elements.map(el => el.getBoundingClientRect());
  
  // Batch write operations
  gsap.set(elements, { 
    y: (i) => positions[i].height,
    opacity: 0 
  });
});
```

---

## Testing Strategies

### Component Testing Template

```jsx
import { render, screen, fireEvent } from '@testing-library/react';
import { vi } from 'vitest';
import Component from './Component';

describe('Component', () => {
  beforeEach(() => {
    // Mock GSAP if needed
    vi.mock('gsap', () => ({
      to: vi.fn(),
      from: vi.fn(),
      set: vi.fn(),
      timeline: vi.fn(() => ({
        to: vi.fn(),
        from: vi.fn()
      }))
    }));
  });

  it('renders with correct props', () => {
    render(<Component title="Test Title" />);
    expect(screen.getByText('Test Title')).toBeInTheDocument();
  });

  it('handles user interactions', () => {
    const handleClick = vi.fn();
    render(<Component onClick={handleClick} />);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalled();
  });
});
```

### Animation Testing

```jsx
// Test animation state changes
it('triggers animation on scroll', async () => {
  const { container } = render(<AnimatedComponent />);
  
  // Mock IntersectionObserver for scroll testing
  const mockIntersectionObserver = vi.fn();
  mockIntersectionObserver.mockReturnValue({
    observe: () => null,
    unobserve: () => null,
    disconnect: () => null
  });
  
  global.IntersectionObserver = mockIntersectionObserver;
  
  // Trigger scroll event
  fireEvent.scroll(window, { target: { scrollY: 500 } });
  
  // Assert animation state
  expect(container.querySelector('.animated-element')).toHaveClass('animate-in');
});
```

---

## Deployment

### Build Configuration

```js
// vite.config.js
export default {
  base: '/repository-name/', // For GitHub Pages
  build: {
    outDir: 'dist',
    assetsDir: 'assets',
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom'],
          gsap: ['gsap', '@gsap/react']
        }
      }
    }
  }
};
```

### Environment Configuration

```js
// Different configs for development/production
const config = {
  development: {
    apiUrl: 'http://localhost:3000',
    debug: true
  },
  production: {
    apiUrl: 'https://api.production.com',
    debug: false
  }
};

export default config[import.meta.env.MODE];
```

### GitHub Pages Deployment

```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

---

## Troubleshooting

### Common Issues

#### GSAP Animations Not Working
```jsx
// Ensure proper plugin registration
import { ScrollTrigger } from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Check for proper cleanup
useGSAP(() => {
  // Animation code
}, { dependencies: [], scope: containerRef });
```

#### Video Loading Issues
```jsx
// Handle video loading states properly
const [videoLoaded, setVideoLoaded] = useState(false);

<video
  onLoadedData={() => setVideoLoaded(true)}
  onError={(e) => console.error('Video load error:', e)}
  preload="metadata" // or "auto" for critical videos
>
  <source src="video.mp4" type="video/mp4" />
</video>
```

#### Performance Issues
```jsx
// Debounce scroll/resize handlers
import { debounce } from 'lodash';

const handleScroll = debounce(() => {
  // Scroll logic
}, 16); // ~60fps

useEffect(() => {
  window.addEventListener('scroll', handleScroll);
  return () => window.removeEventListener('scroll', handleScroll);
}, []);
```

### Debug Tools

```jsx
// Add debug helpers in development
if (import.meta.env.DEV) {
  // GSAP debug
  window.gsap = gsap;
  
  // Performance monitoring
  const observer = new PerformanceObserver((list) => {
    console.log('Performance entries:', list.getEntries());
  });
  observer.observe({ entryTypes: ['measure', 'navigation'] });
}
```

---

## Contributing Guidelines

### Code Standards

1. **Use ESLint configuration** - Follow the project's ESLint rules
2. **Consistent naming** - Use camelCase for variables, PascalCase for components
3. **Component structure** - Follow the established component template
4. **Animation patterns** - Use GSAP consistently across components
5. **Responsive design** - Mobile-first approach with Tailwind classes

### Pull Request Checklist

- [ ] Code follows style guidelines
- [ ] Components are properly documented
- [ ] Animations are performant and accessible
- [ ] Assets are optimized
- [ ] Tests pass (if applicable)
- [ ] Browser compatibility verified
- [ ] Mobile responsiveness tested

---

This developer guide provides the technical foundation for working with the Zentry Gaming codebase effectively. Follow these patterns and guidelines to maintain consistency and performance across the application.