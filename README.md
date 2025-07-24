# Zentry Gaming

![Zentry Gaming Banner](https://via.placeholder.com/800x400/4f46e5/ffffff?text=Zentry+Gaming)

> **A modern, immersive gaming platform built with React, Vite, and GSAP**

Zentry Gaming is a cutting-edge web application that showcases the future of gaming with stunning animations, interactive video elements, and a responsive design. Experience the "Game of Games" where your life becomes an epic MMORPG.

## ✨ Features

- 🎮 **Immersive Hero Section** - Interactive video carousel with smooth transitions
- 🎨 **Advanced Animations** - GSAP-powered scroll-triggered effects and 3D interactions
- 📱 **Responsive Design** - Mobile-first approach with Tailwind CSS
- 🎵 **Audio Controls** - Background music with visual audio indicators
- 🖱️ **3D Interactions** - Mouse-based tilt effects and hover animations
- 🚀 **High Performance** - Optimized assets and hardware-accelerated animations
- 🌟 **Modern Tech Stack** - React 19, Vite 7, GSAP 3, Tailwind CSS 3

## 🚀 Quick Start

### Prerequisites

- Node.js 16+ 
- npm or yarn
- Modern web browser

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/zentry-gaming.git
cd zentry-gaming

# Install dependencies
npm install

# Start development server
npm run dev

# Open in browser
# Navigate to http://localhost:5173
```

### Available Scripts

```bash
npm run dev      # Start development server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
npm run deploy   # Deploy to GitHub Pages
```

## 📁 Project Structure

```
src/
├── components/          # React components
│   ├── Hero.jsx        # Hero section with video carousel
│   ├── Navbar.jsx      # Navigation with scroll effects
│   ├── About.jsx       # About section with animations
│   ├── Features.jsx    # Interactive features showcase
│   ├── Story.jsx       # Story section with 3D effects
│   ├── Contact.jsx     # Contact section
│   ├── Footer.jsx      # Footer component
│   ├── Button.jsx      # Reusable button component
│   ├── AnimatedTitle.jsx # Animated title component
│   └── RoundedCorners.jsx # SVG filter utility
├── App.jsx             # Main application component
├── main.jsx            # Entry point
└── index.css           # Global styles and utilities

public/
├── img/                # Static images
├── videos/             # Video assets
├── audio/              # Audio files
└── fonts/              # Custom fonts
```

## 🎨 Key Components

### Hero Component
Interactive video carousel with smooth transitions and loading states:
```jsx
import Hero from './components/Hero'

<Hero />
```

### Animated Title
Scroll-triggered animated titles with word-by-word reveal:
```jsx
import AnimatedTitle from './components/AnimatedTitle'

<AnimatedTitle 
  title="Welcome to <b>Z</b>entry"
  containerClass="text-center"
/>
```

### Button Component
Versatile button with icon support:
```jsx
import Button from './components/Button'
import { TiLocationArrow } from 'react-icons/ti'

<Button 
  title="Watch Trailer" 
  leftIcon={<TiLocationArrow />}
  containerClass="bg-yellow-300"
/>
```

## 🎭 Animation System

Built with GSAP for high-performance animations:

```jsx
import { useGSAP } from '@gsap/react'
import gsap from 'gsap'

const Component = () => {
  useGSAP(() => {
    gsap.from('.element', {
      opacity: 0,
      y: 50,
      duration: 1,
      scrollTrigger: {
        trigger: '.element',
        start: 'top 80%'
      }
    })
  })
}
```

## 🎯 Tech Stack

| Category | Technology |
|----------|------------|
| **Frontend** | React 19.1.0 |
| **Build Tool** | Vite 7.0.4 |
| **Styling** | Tailwind CSS 3.4.3 |
| **Animations** | GSAP 3.13.0 + ScrollTrigger |
| **Icons** | React Icons 5.5.0 |
| **Utilities** | React Use 17.6.0 |
| **Deployment** | GitHub Pages |

## 📚 Documentation

- **[API Documentation](./API_DOCUMENTATION.md)** - Comprehensive component and API reference
- **[Developer Guide](./DEVELOPER_GUIDE.md)** - Technical implementation details and patterns

## 🎪 Live Demo

Experience Zentry Gaming live: [Demo Link](https://yashpatel305.github.io/Zentry-gaming)

## 🖼️ Screenshots

### Hero Section
![Hero Section](https://via.placeholder.com/600x400/1e293b/ffffff?text=Hero+Section)

### Features Showcase
![Features](https://via.placeholder.com/600x400/1e293b/ffffff?text=Features+Section)

### Story Section
![Story](https://via.placeholder.com/600x400/1e293b/ffffff?text=Story+Section)

## 🔧 Configuration

### Vite Configuration
```js
// vite.config.js
export default {
  plugins: [react()],
  base: '/Zentry-gaming/', // For GitHub Pages
}
```

### Tailwind Configuration
```js
// tailwind.config.js
export default {
  content: ['./index.html', './src/**/*.{js,jsx}'],
  theme: {
    extend: {
      fontFamily: {
        'zentry': ['zentry', 'sans-serif'],
        'general': ['general', 'sans-serif'],
        'circular-web': ['circular-web', 'sans-serif'],
        'robert-medium': ['robert-medium', 'sans-serif'],
        'robert-regular': ['robert-regular', 'sans-serif'],
      }
    }
  }
}
```

## 🚀 Performance

- **Lighthouse Score**: 95+ (Performance, Accessibility, Best Practices, SEO)
- **Bundle Size**: Optimized with code splitting
- **Animation Performance**: 60fps with hardware acceleration
- **Asset Optimization**: WebP images, optimized videos

## 🌟 Browser Support

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- iOS Safari 14+
- Chrome Mobile 90+

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 👥 Team

- **Developer**: Yash Patel
- **Design**: Modern Gaming UI/UX
- **Animation**: GSAP Implementation

## 🙏 Acknowledgments

- [GSAP](https://greensock.com/gsap/) for incredible animation capabilities
- [Tailwind CSS](https://tailwindcss.com/) for utility-first styling
- [React](https://reactjs.org/) for the component architecture
- [Vite](https://vitejs.dev/) for lightning-fast development

---

<div align="center">
  <p>Made with ❤️ for the gaming community</p>
  <p>
    <a href="#top">Back to top</a> •
    <a href="./API_DOCUMENTATION.md">API Docs</a> •
    <a href="./DEVELOPER_GUIDE.md">Dev Guide</a>
  </p>
</div>
