# Framer Motion - Complete Guide

**Framer Motion** is a React library for animations and gestures that simplifies the process of creating complex animations with a declarative API. This guide covers essential features, advanced properties, and common use cases.

## Installation

```bash
npm install framer-motion
# or
yarn add framer-motion
```

---

## Basic Usage

### Animating Components

Use the `motion` component to add animations to any HTML or SVG element.

```jsx
import { motion } from 'framer-motion';

function BasicAnimation() {
  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.8 }}
      animate={{ opacity: 1, scale: 1 }}
      transition={{ duration: 0.5 }}
    >
      Animated Content
    </motion.div>
  );
}
```

- **`initial`**: Initial state of the component.
- **`animate`**: Target state of the animation.
- **`transition`**: Configuration of the animation's timing and easing.

---

## Key Properties

### `initial`
Defines the starting state of the animation.

```jsx
initial={{ opacity: 0, x: -100 }}
```

### `animate`
Specifies the end state of the animation.

```jsx
animate={{ opacity: 1, x: 0 }}
```

### `exit`
Animation configuration for when the component is removed from the DOM.

```jsx
exit={{ opacity: 0, scale: 0.8 }}
```

### `transition`
Controls how the animation progresses, including duration, easing, and delay.

```jsx
transition={{ duration: 0.5, ease: "easeInOut" }}
```

### `whileHover`
Animation configuration while the element is hovered.

```jsx
<motion.div whileHover={{ scale: 1.2 }} />
```

### `whileTap`
Animation configuration while the element is tapped or clicked.

```jsx
<motion.div whileTap={{ scale: 0.9 }} />
```

---

## Variants

**Variants** are a way to define multiple animation states and switch between them.

### Example: Using Variants

```jsx
const variants = {
  hidden: { opacity: 0, y: -50 },
  visible: { opacity: 1, y: 0 },
};

function VariantExample() {
  return (
    <motion.div
      variants={variants}
      initial="hidden"
      animate="visible"
      exit="hidden"
      transition={{ duration: 0.5 }}
    >
      Animated with Variants
    </motion.div>
  );
}
```

### Key Points:
- **`variants`**: Object defining animation states.
- **`initial`**: Starting state.
- **`animate`**: Target state.
- **`exit`**: Animation when exiting.

---

## Gestures

Framer Motion provides gesture-based animations such as hover, tap, and drag.

### Hover Animation

```jsx
<motion.div
  whileHover={{ scale: 1.2, rotate: 10 }}
  transition={{ duration: 0.3 }}
>
  Hover Me
</motion.div>
```

### Tap Animation

```jsx
<motion.div
  whileTap={{ scale: 0.9, backgroundColor: "#D32F2F" }}
>
  Tap Me
</motion.div>
```

### Drag and Drop

Enable drag functionality with `drag` and constrain the draggable area with `dragConstraints`.

```jsx
<motion.div
  drag
  dragConstraints={{ left: 0, right: 300, top: 0, bottom: 300 }}
>
  Drag Me
</motion.div>
```

### Pan Events

```jsx
<motion.div
  drag
  onPanStart={(event, info) => console.log('Pan Start:', info)}
  onPanEnd={(event, info) => console.log('Pan End:', info)}
>
  Drag Me with Events
</motion.div>
```

---

## Advanced Animation Features

### Custom Transitions

Control the timing and easing of animations more precisely.

```jsx
<motion.div
  animate={{ x: 100 }}
  transition={{
    type: "spring",
    stiffness: 300,
    damping: 20,
    mass: 1,
  }}
>
  Custom Spring Animation
</motion.div>
```

### Spring Animations

Framer Motion uses spring physics by default, allowing natural movement.

```jsx
<motion.div
  animate={{ x: 100 }}
  transition={{ type: "spring", stiffness: 100, damping: 10 }}
>
  Spring Animation
</motion.div>
```

### Keyframes

Animate through multiple states using keyframes.

```jsx
<motion.div
  animate={{ x: [0, 100, 50, 200], opacity: [1, 0.5, 1] }}
  transition={{ duration: 2 }}
>
  Keyframes Animation
</motion.div>
```

---

## Animating Presence

Use **`AnimatePresence`** to animate components as they enter and leave the DOM.

### Example: Animate on Mount and Unmount

```jsx
import { AnimatePresence, motion } from 'framer-motion';

function PresenceExample({ isVisible }) {
  return (
    <AnimatePresence>
      {isVisible && (
        <motion.div
          key="box"
          initial={{ opacity: 0, y: 50 }}
          animate={{ opacity: 1, y: 0 }}
          exit={{ opacity: 0, y: -50 }}
          transition={{ duration: 0.5 }}
        >
          Animate Me!
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

---

## Layout Animations

Animate layout changes by applying the `layout` prop to a component.

### Example: Layout Animation

```jsx
<motion.div layout>
  <h1>Animated Layout</h1>
</motion.div>
```

### Example: Reordering List Items

```jsx
function Item({ id }) {
  return (
    <motion.li layout>
      Item {id}
    </motion.li>
  );
}

function List({ items }) {
  return (
    <ul>
      {items.map(item => (
        <Item key={item.id} id={item.id} />
      ))}
    </ul>
  );
}
```

---

## Motion Values

**Motion Values** provide fine-grained control over animatable properties.

### Example: Using Motion Values

```jsx
import { motion, useMotionValue, useTransform } from 'framer-motion';

function MotionValueExample() {
  const x = useMotionValue(0);
  const scale = useTransform(x, [-100, 100], [0.5, 1.5]);

  return (
    <motion.div
      style={{ x, scale }}
      drag="x"
      dragConstraints={{ left: 0, right: 300 }}
    >
      Drag Me
    </motion.div>
  );
}
```

---

## SVG Animations

Animate SVG elements using Framer Motion.

### Example: SVG Path Animation

```jsx
<motion.path
  d="M10 80 Q 95 10 180 80 T 360 80"
  initial={{ pathLength: 0 }}
  animate={{ pathLength: 1 }}
  transition={{ duration: 2 }}
/>
```

---

## Scroll-based Animations

Animate elements based on scroll position using the `useViewportScroll` hook.

### Example: Scroll Animation

```jsx
import { motion, useViewportScroll, useTransform } from 'framer-motion';

function ScrollAnimation() {
  const { scrollYProgress } = useViewportScroll();
  const scale = useTransform(scrollYProgress, [0, 1], [1, 2]);

  return <motion.div style={{ scale }}>Scroll to Scale</motion.div>;
}
```

---

## Custom Hooks

### `useAnimation`

Control animations programmatically with the `useAnimation` hook.

### Example: Manual Control

```jsx
import { useAnimation, motion } from 'framer-motion';

function ControlledAnimation() {
  const controls = useAnimation();

  return (
    <div>
      <motion.div
        animate={controls}
        initial={{ opacity: 0 }}
        transition={{ duration: 0.5 }}
      >
        Controlled Animation
      </motion.div>
      <button onClick={() => controls.start({ opacity: 1 })}>
        Start Animation
      </button>
    </div>
  );
}
```

---

## Server-Side Rendering (SSR) Considerations

For SSR with Next.js or other frameworks, you might need to disable animations on the server side.

### Example: Disabling Animations on Server

```jsx
import { isServer } from './utils'; // Utility to check if running on server

const animationsDisabled = isServer;

<motion.div
  initial={animationsDisabled ? false : { opacity: 0 }}
  animate={animationsDisabled ? false : { opacity: 1 }}
>
  Content
</motion.div>
```

---

## Summary of Features

- **Basic Animations**: Use `initial`, `animate`, `exit`, and `transition` to create smooth animations.
- **Variants**: Define multiple animation states and transition between them.
- **Gestures**: Animate based on user interactions such as hover, tap, and drag.
- **Advanced Transitions**: Customize animations with springs, tweens, and keyframes.
- **Animate Presence**: Animate elements as they enter and leave the DOM with `AnimatePresence`.
- **Layout Animations**: Smoothly animate