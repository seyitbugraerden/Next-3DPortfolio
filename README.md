<div align="center">

# Next.js 15 Interactive Portfolio

### Animated portfolio experience built with Next.js, React, Motion and React Three Fiber

A modern portfolio interface focused on **motion design, interactive hero experiences, smooth section navigation and experimental 3D integration**.

<br />

![Next.js](https://img.shields.io/badge/Next.js-15.1-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Three.js](https://img.shields.io/badge/React_Three_Fiber-3D-000000?style=for-the-badge&logo=threedotjs&logoColor=white)

</div>

---

## About the Project

**Next15-3DPortfolio** is an experimental developer/designer portfolio built with **Next.js 15 and React 19**.

The project explores a more interactive alternative to traditional portfolio websites by combining:

- Motion-based entrance animations
- Typewriter effects
- Full-screen scroll-snapping sections
- Interactive call-to-action elements
- Modern responsive layout techniques
- React Three Fiber / Drei based 3D experiments

The current implementation focuses primarily on the animated hero section, while the Services, Portfolio and Contact areas provide the structural foundation for further development.

---

## Current Status

The project is currently a **work in progress**.

The hero experience is substantially implemented, while the following sections are currently placeholders:

```text
Services
Portfolio
Contact
```

The repository also contains a React Three Fiber based 3D shape component. However, the `<Canvas>` implementation is currently commented out in the hero section, meaning the active version uses the static hero visual instead of rendering the 3D scene.

---

## Features

### Animated Hero Experience

The hero area contains several independent motion sequences built with `motion/react`.

Current animations include:

- Animated hero title entrance
- Staggered award section
- Animated social media links
- Fade-in certificate section
- Infinite scroll indicator animation
- Animated contact CTA entrance
- Continuously rotating contact button
- Typewriter speech bubble animation

---

### Typewriter Interaction

The speech bubble uses:

```text
react-type-animation
```

to continuously cycle between text sequences.

This provides an additional dynamic layer to the hero interface without requiring custom animation timing logic.

---

### Scroll Snap Navigation

The portfolio uses native CSS scroll snapping:

```css
html {
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
}

section {
  height: 100vh;
  scroll-snap-align: center;
}
```

Each primary portfolio section therefore behaves like an individual viewport-sized experience.

---

### Experimental 3D Support

The project includes:

- `@react-three/fiber`
- `@react-three/drei`
- `MeshDistortMaterial`
- Drei `Sphere`

The existing `Shape.tsx` component creates a distorted animated sphere:

```tsx
<Sphere args={[1, 100, 200]} scale={2.4}>
  <MeshDistortMaterial
    color="#DB8B9B"
    distort={0.5}
    speed={2}
  />
</Sphere>
```

The component is prepared for use inside React Three Fiber's `<Canvas>` environment.

> The Canvas integration is currently disabled in the active hero implementation.

---

## Tech Stack

| Technology | Purpose |
| --- | --- |
| **Next.js 15.1** | Application framework |
| **React 19** | Component architecture |
| **TypeScript** | Type-safe development |
| **Tailwind CSS 3.4** | Utility-based styling |
| **Motion 11** | UI and entrance animations |
| **React Three Fiber** | React renderer for Three.js |
| **React Three Drei** | Three.js helper components |
| **React Type Animation** | Typewriter animations |
| **Turbopack** | Development bundler |

---

## Architecture

The project uses the **Next.js App Router** architecture.

```text
Next15-3DPortfolio/
│
├── public/
│   ├── award1.png
│   ├── award2.png
│   ├── award3.png
│   ├── certificate.png
│   ├── hero.png
│   ├── man.png
│   ├── p1.jpg
│   ├── p2.jpg
│   ├── p3.jpg
│   ├── p4.jpg
│   ├── p5.jpg
│   ├── service1.png
│   ├── service2.png
│   ├── service3.png
│   ├── instagram.png
│   ├── facebook.png
│   └── youtube.png
│
├── src/
│   ├── app/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   └── page.tsx
│   │
│   └── components/
│       ├── hero/
│       │   ├── Hero.tsx
│       │   ├── Shape.tsx
│       │   ├── Speech.tsx
│       │   └── hero.css
│       │
│       ├── services/
│       │   ├── Services.tsx
│       │   └── services.css
│       │
│       ├── portfolio/
│       │   ├── Portfolio.tsx
│       │   └── portfolio.css
│       │
│       └── contact/
│           ├── Contact.tsx
│           └── contact.css
│
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## Page Structure

The homepage is divided into four full-screen sections.

```text
Home
 │
 ├── Hero
 │    ├── Animated introduction
 │    ├── Awards
 │    ├── Social links
 │    ├── Typewriter speech
 │    ├── Certificate
 │    └── Contact CTA
 │
 ├── Services
 │
 ├── Portfolio
 │
 └── Contact
```

Each section occupies the full viewport height and participates in the scroll-snap navigation system.

---

## Motion Architecture

Animation logic is separated into reusable variant objects where appropriate.

Example:

```tsx
const awardVariants = {
  initialAward: {
    x: -100,
    opacity: 0,
  },
  animateAward: {
    x: 0,
    opacity: 1,
    transition: {
      duration: 1,
      staggerChildren: 0.2,
    },
  },
};
```

This approach allows parent and child elements to share coordinated motion behavior.

---

## Getting Started

Clone the repository:

```bash
git clone https://github.com/seyitbugraerden/Next15-3DPortfolio.git
```

Navigate to the project:

```bash
cd Next15-3DPortfolio
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

---

## Available Scripts

### Development

```bash
npm run dev
```

Runs the application using Next.js with **Turbopack**.

### Production Build

```bash
npm run build
```

Creates an optimized production build.

### Production Server

```bash
npm start
```

Runs the production build.

---

## 3D Scene

To activate the existing Three.js experiment, the hero section already contains a prepared Canvas implementation.

The intended structure is:

```tsx
<Canvas>
  <Suspense fallback="loading...">
    <Shape />
  </Suspense>
</Canvas>
```

The `Shape` component uses Drei's `Sphere` and `MeshDistortMaterial` to create an animated organic 3D object.

---

## Development Roadmap

The existing architecture provides a foundation for further development in several areas:

- Complete Services section
- Complete portfolio/project showcase
- Complete Contact section
- Enable the React Three Fiber scene
- Replace placeholder copy
- Connect real social media links
- Add real project information
- Improve metadata and SEO
- Add responsive navigation
- Improve accessibility
- Optimize Three.js rendering performance
- Add lazy loading for 3D content
- Add project detail interactions
- Add contact form functionality

---

## Technical Highlights

This repository demonstrates experience with:

- Next.js App Router
- React 19
- Client Components
- Component-based frontend architecture
- TypeScript
- Motion animation variants
- Staggered animations
- Continuous animations
- CSS Scroll Snap
- Responsive UI design
- React Three Fiber architecture
- Drei materials and geometry
- Typewriter UI interactions
- Turbopack development workflow

---

## Developer

<div align="center">

### Seyit Buğra Erden

**Full Stack Developer · Software Engineer**

[GitHub](https://github.com/seyitbugraerden) ·
[LinkedIn](https://www.linkedin.com/in/sbugraerden/)

<br />

Built with **Next.js · React · TypeScript · Motion · React Three Fiber**

</div>
