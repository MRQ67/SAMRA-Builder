# SAMRA Landing Page - Implementation Plan

## Project Context

You are building the marketing landing page for **SAMRA** - a no-code 3D website builder.

**Read First:** `PROMPT.md` for full project context.

---

## Design System

### Color Palette
```css
--primary: #FAF3E1      /* Warm cream - backgrounds, cards */
--secondary: #F5E7C6    /* Light beige - secondary elements */
--accent: #FF6D1F       /* Vibrant orange - CTAs, highlights */
--dark: #222222         /* Near black - text, UI elements */
```

**Usage Guidelines:**
- **Primary (#FAF3E1):** Main background, hero section
- **Secondary (#F5E7C6):** Card backgrounds, alternating sections
- **Accent (#FF6D1F):** Buttons, links, important elements, 3D accents
- **Dark (#222222):** All text, icons, borders

**Additional Colors (Derived):**
```css
--accent-light: #FF8C4A   /* Hover states */
--accent-dark: #E85D0F    /* Active states */
--dark-soft: #444444      /* Secondary text */
--cream-dark: #E8DCC8     /* Borders on light backgrounds */
```

### Typography
```css
/* Headings */
font-family: 'Inter', sans-serif;
font-weight: 700-900 (Bold to Black);
color: #222222;

/* Body */
font-family: 'Inter', sans-serif;
font-weight: 400-500 (Regular to Medium);
color: #444444;

/* CTA Buttons */
font-family: 'Inter', sans-serif;
font-weight: 600 (Semibold);
color: #FAF3E1; /* on orange background */
```

### Component Style

**Aesthetic:** Modern, warm, professional with playful energy

**Principles:**
- Generous white space (cream space)
- Rounded corners (8-16px)
- Subtle shadows with warm tones
- 3D elements use orange accent lighting
- Smooth animations (300-500ms)

---

## Landing Page Structure

### Complete Page Flow
```
1. Hero Section (Fullscreen)
   ├─ 3D Morphing Product Display
   ├─ Headline + Subheadline
   ├─ Primary CTA Button
   └─ Scroll Indicator

2. Value Proposition (3 Columns)
   ├─ "No Code Required"
   ├─ "Real-Time Collaboration"
   └─ "3D Without Complexity"

3. Interactive Demo (Split Screen)
   ├─ Left: Simple Controls Preview
   └─ Right: Live 3D Result

4. Template Gallery (Carousel)
   ├─ 3D Rotating Carousel
   ├─ 5 Template Previews
   └─ "Browse All Templates" CTA

5. How It Works (3 Steps)
   ├─ Pick Template
   ├─ Customize
   └─ Publish

6. Final CTA
   ├─ Energy Sphere (3D)
   ├─ Headline
   └─ Large CTA Button

7. Footer
   ├─ Links
   ├─ Social Media
   └─ Copyright
```

---

## Implementation Phases

**CRITICAL INSTRUCTIONS:**
1. Implement ONE phase at a time
2. After completing each phase, STOP and wait for approval
3. Document what you built
4. Ask for feedback before proceeding
5. Do NOT skip phases or combine them

---

## Phase 1: Setup & Basic Layout

### Goals
- Configure Tailwind with SAMRA color palette
- Create root layout with navigation
- Setup basic page structure
- Test responsive design

### Tasks

#### 1.1 Update Tailwind Config

**File:** `tailwind.config.js`
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  darkMode: ["class"],
  content: [
    "./app/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        cream: {
          DEFAULT: "#FAF3E1",
          light: "#FFFFFF",
          dark: "#E8DCC8",
        },
        beige: {
          DEFAULT: "#F5E7C6",
          light: "#F9EDD6",
          dark: "#E8DCC8",
        },
        orange: {
          DEFAULT: "#FF6D1F",
          light: "#FF8C4A",
          dark: "#E85D0F",
        },
        dark: {
          DEFAULT: "#222222",
          soft: "#444444",
          lighter: "#666666",
        },
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
      boxShadow: {
        'warm': '0 4px 20px rgba(255, 109, 31, 0.15)',
        'warm-lg': '0 10px 40px rgba(255, 109, 31, 0.2)',
      },
    },
  },
  plugins: [],
}
```

#### 1.2 Update Global Styles

**File:** `app/styles/globals.css`
```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  * {
    @apply border-cream-dark;
  }
  
  body {
    @apply bg-cream text-dark font-sans antialiased;
  }

  h1, h2, h3, h4, h5, h6 {
    @apply text-dark font-bold;
  }

  h1 {
    @apply text-5xl md:text-7xl;
  }

  h2 {
    @apply text-4xl md:text-5xl;
  }

  h3 {
    @apply text-2xl md:text-3xl;
  }

  p {
    @apply text-dark-soft text-base md:text-lg leading-relaxed;
  }
}

@layer components {
  .btn-primary {
    @apply bg-orange hover:bg-orange-light active:bg-orange-dark 
           text-cream font-semibold px-8 py-4 rounded-lg
           transition-all duration-300 shadow-warm hover:shadow-warm-lg
           transform hover:-translate-y-0.5;
  }

  .btn-secondary {
    @apply bg-transparent border-2 border-orange text-orange
           hover:bg-orange hover:text-cream font-semibold px-8 py-4 rounded-lg
           transition-all duration-300;
  }

  .section-padding {
    @apply py-20 md:py-32 px-4 md:px-8;
  }

  .container-custom {
    @apply max-w-7xl mx-auto;
  }
}

@layer utilities {
  .text-gradient {
    @apply bg-gradient-to-r from-orange to-orange-light bg-clip-text text-transparent;
  }
}
```

#### 1.3 Create Navigation Component

**File:** `app/components/layout/Navigation.tsx`
```typescript
import { Link } from '@tanstack/react-router'
import { useState } from 'react'

export function Navigation() {
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false)

  return (
    <nav className="fixed top-0 left-0 right-0 z-50 bg-cream/80 backdrop-blur-md border-b border-cream-dark">
      <div className="container-custom">
        <div className="flex items-center justify-between h-20">
          {/* Logo */}
          <Link to="/" className="flex items-center space-x-2">
            <div className="w-10 h-10 bg-orange rounded-lg flex items-center justify-center">
              <span className="text-cream font-bold text-xl">S</span>
            </div>
            <span className="text-2xl font-bold text-dark">SAMRA</span>
          </Link>

          {/* Desktop Navigation */}
          <div className="hidden md:flex items-center space-x-8">
            <a href="#features" className="text-dark-soft hover:text-orange transition-colors">
              Features
            </a>
            <a href="#templates" className="text-dark-soft hover:text-orange transition-colors">
              Templates
            </a>
            <a href="#how-it-works" className="text-dark-soft hover:text-orange transition-colors">
              How It Works
            </a>
          </div>

          {/* CTA Buttons */}
          <div className="hidden md:flex items-center space-x-4">
            <button className="text-dark-soft hover:text-orange transition-colors font-medium">
              Sign In
            </button>
            <button className="btn-primary">
              Start Building
            </button>
          </div>

          {/* Mobile Menu Button */}
          <button 
            className="md:hidden text-dark"
            onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
          >
            <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              {mobileMenuOpen ? (
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
              ) : (
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
              )}
            </svg>
          </button>
        </div>

        {/* Mobile Menu */}
        {mobileMenuOpen && (
          <div className="md:hidden py-4 border-t border-cream-dark">
            <div className="flex flex-col space-y-4">
              <a href="#features" className="text-dark-soft hover:text-orange transition-colors">
                Features
              </a>
              <a href="#templates" className="text-dark-soft hover:text-orange transition-colors">
                Templates
              </a>
              <a href="#how-it-works" className="text-dark-soft hover:text-orange transition-colors">
                How It Works
              </a>
              <div className="pt-4 border-t border-cream-dark space-y-2">
                <button className="w-full text-dark-soft hover:text-orange transition-colors font-medium py-2">
                  Sign In
                </button>
                <button className="btn-primary w-full">
                  Start Building
                </button>
              </div>
            </div>
          </div>
        )}
      </div>
    </nav>
  )
}
```

#### 1.4 Update Landing Page Route

**File:** `app/routes/index.tsx`
```typescript
import { createFileRoute } from '@tanstack/react-router'
import { Navigation } from '@/components/layout/Navigation'

export const Route = createFileRoute('/')({
  component: LandingPage,
})

function LandingPage() {
  return (
    <div className="min-h-screen bg-cream">
      <Navigation />
      
      {/* Placeholder sections - will build in next phases */}
      <main className="pt-20">
        <section className="section-padding">
          <div className="container-custom">
            <h1 className="text-center mb-4">
              Build <span className="text-gradient">3D Landing Pages</span>
            </h1>
            <p className="text-center text-xl max-w-3xl mx-auto">
              No code required. Real-time collaboration. Professional results in minutes.
            </p>
          </div>
        </section>

        {/* Placeholder for other sections */}
        <section className="section-padding bg-beige">
          <div className="container-custom">
            <p className="text-center text-dark-soft">
              More sections coming in next phases...
            </p>
          </div>
        </section>
      </main>
    </div>
  )
}
```

### Acceptance Criteria

- [ ] Tailwind configured with SAMRA colors
- [ ] Navigation bar with logo and menu
- [ ] Mobile-responsive navigation
- [ ] Typography scales properly on mobile/desktop
- [ ] Button styles working (hover, active states)
- [ ] No console errors
- [ ] Page loads at http://localhost:3000

### Deliverables

1. Updated `tailwind.config.js`
2. Updated `app/styles/globals.css`
3. New `app/components/layout/Navigation.tsx`
4. Updated `app/routes/index.tsx`
5. Screenshot of the page showing colors and navigation

---

**🛑 STOP HERE - WAIT FOR APPROVAL BEFORE PHASE 2**

Document what you built:
- What works?
- Any challenges?
- What needs adjustment?

---

## Phase 2: Hero Section with 3D Scene

### Goals
- Create fullscreen hero with Three.js
- Implement morphing 3D product
- Add scroll-based animation
- Responsive design

### Tasks

#### 2.1 Install Three.js Dependencies
```bash
bun add three @react-three/fiber @react-three/drei
bun add -D @types/three
```

#### 2.2 Create 3D Canvas Component

**File:** `app/components/landing/Hero3D.tsx`
```typescript
'use client'

import { Canvas } from '@react-three/fiber'
import { OrbitControls, PerspectiveCamera, Environment } from '@react-three/drei'
import { Suspense } from 'react'

export function Hero3D() {
  return (
    <div className="absolute inset-0 z-0">
      <Canvas>
        <Suspense fallback={null}>
          <PerspectiveCamera makeDefault position={[0, 0, 5]} />
          
          {/* Lighting */}
          <ambientLight intensity={0.5} />
          <directionalLight 
            position={[10, 10, 5]} 
            intensity={1}
            castShadow
          />
          <pointLight 
            position={[-5, 5, 5]} 
            intensity={0.8}
            color="#FF6D1F" 
          />

          {/* 3D Object */}
          <ProductMorph />

          {/* Environment */}
          <Environment preset="sunset" />
          
          {/* Controls (will disable later) */}
          <OrbitControls enableZoom={false} enablePan={false} />
        </Suspense>
      </Canvas>
    </div>
  )
}

function ProductMorph() {
  // Placeholder - will implement morphing in next iteration
  return (
    <mesh>
      <boxGeometry args={[2, 2, 2]} />
      <meshStandardMaterial 
        color="#FF6D1F" 
        metalness={0.8} 
        roughness={0.2} 
      />
    </mesh>
  )
}
```

#### 2.3 Create Hero Section Component

**File:** `app/components/landing/HeroSection.tsx`
```typescript
import { Hero3D } from './Hero3D'

export function HeroSection() {
  return (
    <section className="relative h-screen flex items-center justify-center overflow-hidden">
      {/* 3D Background */}
      <Hero3D />

      {/* Content Overlay */}
      <div className="relative z-10 container-custom text-center px-4">
        <h1 className="mb-6 text-cream drop-shadow-lg">
          Build Stunning
          <br />
          <span className="text-gradient">3D Landing Pages</span>
        </h1>
        
        <p className="text-xl md:text-2xl text-beige mb-12 max-w-3xl mx-auto drop-shadow">
          No code required. Create professional 3D websites with our visual builder.
          Real-time collaboration included.
        </p>

        <div className="flex flex-col sm:flex-row gap-4 justify-center">
          <button className="btn-primary text-lg">
            Start Building Free
          </button>
          <button className="btn-secondary text-lg bg-cream/10 backdrop-blur-sm border-cream text-cream hover:bg-cream hover:text-dark">
            Watch Demo
          </button>
        </div>

        {/* Scroll Indicator */}
        <div className="absolute bottom-12 left-1/2 transform -translate-x-1/2 animate-bounce">
          <svg 
            className="w-6 h-6 text-cream" 
            fill="none" 
            stroke="currentColor" 
            viewBox="0 0 24 24"
          >
            <path 
              strokeLinecap="round" 
              strokeLinejoin="round" 
              strokeWidth={2} 
              d="M19 14l-7 7m0 0l-7-7m7 7V3" 
            />
          </svg>
        </div>
      </div>

      {/* Gradient Overlay for better text readability */}
      <div className="absolute inset-0 bg-gradient-to-b from-dark/20 via-transparent to-cream/50 pointer-events-none" />
    </section>
  )
}
```

#### 2.4 Update Landing Page

**File:** `app/routes/index.tsx`
```typescript
import { createFileRoute } from '@tanstack/react-router'
import { Navigation } from '@/components/layout/Navigation'
import { HeroSection } from '@/components/landing/HeroSection'

export const Route = createFileRoute('/')({
  component: LandingPage,
})

function LandingPage() {
  return (
    <div className="min-h-screen bg-cream">
      <Navigation />
      
      <main>
        <HeroSection />
        
        {/* Placeholder for next sections */}
        <section className="section-padding">
          <div className="container-custom">
            <p className="text-center text-dark-soft">
              More sections coming in Phase 3...
            </p>
          </div>
        </section>
      </main>
    </div>
  )
}
```

### Acceptance Criteria

- [ ] Three.js canvas renders without errors
- [ ] 3D cube visible and rotating
- [ ] Orange accent lighting applied
- [ ] Hero text readable over 3D background
- [ ] Responsive on mobile
- [ ] Smooth animations
- [ ] Scroll indicator animates

### Deliverables

1. `app/components/landing/Hero3D.tsx`
2. `app/components/landing/HeroSection.tsx`
3. Updated `app/routes/index.tsx`
4. Screenshot of hero with 3D element
5. Video/GIF of rotation animation

---

**🛑 STOP HERE - WAIT FOR APPROVAL BEFORE PHASE 3**

---

## Phase 3: Value Proposition Section

### Goals
- Create 3-column feature cards
- Add floating animation (subtle)
- Mouse parallax effect
- Icons for each feature

### Tasks

#### 3.1 Create Feature Card Component

**File:** `app/components/landing/FeatureCard.tsx`
```typescript
'use client'

import { useState } from 'react'
import { motion } from 'framer-motion'

interface FeatureCardProps {
  icon: React.ReactNode
  title: string
  description: string
  index: number
}

export function FeatureCard({ icon, title, description, index }: FeatureCardProps) {
  const [isHovered, setIsHovered] = useState(false)

  return (
    <motion.div
      initial={{ opacity: 0, y: 50 }}
      whileInView={{ opacity: 1, y: 0 }}
      transition={{ duration: 0.5, delay: index * 0.1 }}
      viewport={{ once: true }}
      onHoverStart={() => setIsHovered(true)}
      onHoverEnd={() => setIsHovered(false)}
      className="relative"
    >
      <motion.div
        animate={{
          y: isHovered ? -10 : 0,
          scale: isHovered ? 1.05 : 1,
        }}
        transition={{ duration: 0.3 }}
        className="bg-beige rounded-2xl p-8 shadow-warm hover:shadow-warm-lg transition-shadow"
      >
        {/* Icon */}
        <div className="w-16 h-16 bg-orange rounded-xl flex items-center justify-center mb-6 text-cream">
          {icon}
        </div>

        {/* Content */}
        <h3 className="text-dark mb-4">{title}</h3>
        <p className="text-dark-soft">{description}</p>

        {/* Decorative Element */}
        <div className="absolute top-0 right-0 w-32 h-32 bg-orange/5 rounded-full blur-3xl -z-10" />
      </motion.div>
    </motion.div>
  )
}
```

#### 3.2 Create Value Proposition Section

**File:** `app/components/landing/ValuePropSection.tsx`
```typescript
import { FeatureCard } from './FeatureCard'

export function ValuePropSection() {
  const features = [
    {
      icon: (
        <svg className="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
        </svg>
      ),
      title: 'No Code Required',
      description: 'Build professional 3D landing pages with simple visual controls. No programming knowledge needed.',
    },
    {
      icon: (
        <svg className="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
        </svg>
      ),
      title: 'Real-Time Collaboration',
      description: 'Work together with your team like Google Docs. See changes instantly, no refresh needed.',
    },
    {
      icon: (
        <svg className="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
        </svg>
      ),
      title: '3D Without Complexity',
      description: 'Upload images, pick animations, and publish. We handle all the Three.js complexity for you.',
    },
  ]

  return (
    <section id="features" className="section-padding bg-cream">
      <div className="container-custom">
        {/* Section Header */}
        <div className="text-center mb-16">
          <h2 className="mb-4">
            Why Choose <span className="text-gradient">SAMRA</span>?
          </h2>
          <p className="text-xl text-dark-soft max-w-2xl mx-auto">
            The easiest way to create stunning 3D websites without writing a single line of code.
          </p>
        </div>

        {/* Feature Cards Grid */}
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {features.map((feature, index) => (
            <FeatureCard key={index} {...feature} index={index} />
          ))}
        </div>
      </div>
    </section>
  )
}
```

#### 3.3 Install Framer Motion
```bash
bun add framer-motion
```

#### 3.4 Update Landing Page

**File:** `app/routes/index.tsx`
```typescript
import { createFileRoute } from '@tanstack/react-router'
import { Navigation } from '@/components/layout/Navigation'
import { HeroSection } from '@/components/landing/HeroSection'
import { ValuePropSection } from '@/components/landing/ValuePropSection'

export const Route = createFileRoute('/')({
  component: LandingPage,
})

function LandingPage() {
  return (
    <div className="min-h-screen bg-cream">
      <Navigation />
      
      <main>
        <HeroSection />
        <ValuePropSection />
        
        {/* Placeholder for next sections */}
        <section className="section-padding bg-beige">
          <div className="container-custom">
            <p className="text-center text-dark-soft">
              More sections coming in Phase 4...
            </p>
          </div>
        </section>
      </main>
    </div>
  )
}
```

### Acceptance Criteria

- [ ] Three feature cards render
- [ ] Cards animate on scroll
- [ ] Hover effects work smoothly
- [ ] Icons display correctly
- [ ] Responsive grid on mobile (stacks vertically)
- [ ] Orange accent colors applied
- [ ] Text readable and styled

### Deliverables

1. `app/components/landing/FeatureCard.tsx`
2. `app/components/landing/ValuePropSection.tsx`
3. Updated `app/routes/index.tsx`
4. Screenshot of feature cards section
5. Video of hover animations

---

**🛑 STOP HERE - WAIT FOR APPROVAL BEFORE PHASE 4**

---

## Phase 4: Interactive Demo Section

### Goals
- Split screen layout (controls left, 3D preview right)
- Show simple controls that affect 3D object
- Demonstrate SAMRA's ease of use
- Interactive color/animation pickers

### Tasks

#### 4.1 Create Demo Controls Component

**File:** `app/components/landing/DemoControls.tsx`
```typescript
'use client'

import { useState } from 'react'

interface DemoControlsProps {
  onColorChange: (color: string) => void
  onAnimationChange: (animation: string) => void
}

export function DemoControls({ onColorChange, onAnimationChange }: DemoControlsProps) {
  const [selectedColor, setSelectedColor] = useState('#FF6D1F')
  const [selectedAnimation, setSelectedAnimation] = useState('rotate')

  const colors = [
    { name: 'Orange', value: '#FF6D1F' },
    { name: 'Purple', value: '#9333EA' },
    { name: 'Blue', value: '#3B82F6' },
    { name: 'Pink', value: '#EC4899' },
  ]

  const animations = [
    { name: 'Rotate', value: 'rotate' },
    { name: 'Float', value: 'float' },
    { name: 'Pulse', value: 'pulse' },
  ]

  const handleColorChange = (color: string) => {
    setSelectedColor(color)
    onColorChange(color)
  }

  const handleAnimationChange = (animation: string) => {
    setSelectedAnimation(animation)
    onAnimationChange(animation)
  }

  return (
    <div className="space-y-8">
      <div>
        <h3 className="text-2xl font-bold mb-4 text-dark">Simple Controls</h3>
        <p className="text-dark-soft mb-6">
          Change colors and animations with just a click. No coding required.
        </p>
      </div>

      {/* Color Picker */}
      <div>
        <label className="block text-dark font-semibold mb-3">Choose Color</label>
        <div className="grid grid-cols-2 gap-3">
          {colors.map((color) => (
            <button
              key={color.value}
              onClick={() => handleColorChange(color.value)}
              className={`
                flex items-center space-x-3 p-3 rounded-lg border-2 transition-all
                ${selectedColor === color.value 
                  ? 'border-orange bg-beige' 
                  : 'border-cream-dark hover:border-orange/50'
                }
              `}
            >
              <div 
                className="w-8 h-8 rounded-md shadow-sm" 
                style={{ backgroundColor: color.value }}
              />
              <span className="font-medium text-dark">{color.name}</span>
            </button>
          ))}
        </div>
      </div>

      {/* Animation Picker */}
      <div>
        <label className="block text-dark font-semibold mb-3">Choose Animation</label>
        <div className="space-y-2">
          {animations.map((animation) => (
            <button
              key={animation.value}
              onClick={() => handleAnimationChange(animation.value)}
              className={`
                w-full text-left p-4 rounded-lg border-2 transition-all
                ${selectedAnimation === animation.value 
                  ? 'border-orange bg-beige' 
                  : 'border-cream-dark hover:border-orange/50'
                }
              `}
            >
              <span className="font-medium text-dark">{animation.name}</span>
            </button>
          ))}
        </div>
      </div>

      <div className="pt-4 border-t border-cream-dark">
        <p className="text-sm text-dark-soft italic">
          ✨ Changes happen instantly in real-time
        </p>
      </div>
    </div>
  )
}
```

#### 4.2 Create Interactive 3D Preview

**File:** `app/components/landing/DemoPreview3D.tsx`
```typescript
'use client'

import { Canvas, useFrame } from '@react-three/fiber'
import { OrbitControls, PerspectiveCamera } from '@react-three/drei'
import { useRef } from 'react'
import * as THREE from 'three'

interface DemoPreview3DProps {
  color: string
  animation: string
}

export function DemoPreview3D({ color, animation }: DemoPreview3DProps) {
  return (
    <div className="w-full h-full bg-gradient-to-br from-dark to-dark-soft rounded-2xl overflow-hidden shadow-warm-lg">
      <Canvas>
        <PerspectiveCamera makeDefault position={[0, 0, 5]} />
        <ambientLight intensity={0.5} />
        <pointLight position={[10, 10, 10]} intensity={1} color={color} />
        <AnimatedBox color={color} animation={animation} />
        <OrbitControls enableZoom={false} autoRotate autoRotateSpeed={1} />
      </Canvas>
    </div>
  )
}

function AnimatedBox({ color, animation }: { color: string; animation: string }) {
  const meshRef = useRef<THREE.Mesh>(null)

  useFrame((state) => {
    if (!meshRef.current) return

    const time = state.clock.getElapsedTime()

    switch (animation) {
      case 'rotate':
        meshRef.current.rotation.y = time * 0.5
        meshRef.current
