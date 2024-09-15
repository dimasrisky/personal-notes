# React Router DOM (v6) - Quick Guide

**React Router DOM** is a library for routing in React applications, allowing you to navigate between components and maintain a single-page application experience.

## Installation

```bash
npm install react-router-dom
```

## Key Features and API

### 1. **`<BrowserRouter>`**

Wrap your entire application with `<BrowserRouter>` to enable routing.

```jsx
import { BrowserRouter } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      {/* Your routes go here */}
    </BrowserRouter>
  );
}
```

### 2. **`<Routes>` and `<Route>`**

Use `<Routes>` to define all your routes. Inside `<Routes>`, use `<Route>` to specify the path and component to render.

```jsx
import { Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}
```

### 3. **Alternative: `createBrowserRouter` and `RouterProvider`**

`createBrowserRouter` is an alternative for defining routes. It simplifies route management and provides better control over route objects.

```jsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';
import Home from './Home';
import About from './About';

const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "/about",
    element: <About />,
  },
]);

function App() {
  return <RouterProvider router={router} />;
}
```

### 4. **`useNavigate`**

Use the `useNavigate` hook to programmatically navigate between routes.

```jsx
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate();

  return (
    <div>
      <h1>Home</h1>
      <button onClick={() => navigate('/about')}>Go to About</button>
    </div>
  );
}
```

### 5. **`useParams`**

Get URL parameters using the `useParams` hook.

```jsx
import { useParams } from 'react-router-dom';

function UserProfile() {
  const { userId } = useParams();

  return <h1>User Profile for User ID: {userId}</h1>;
}
```

In the route, define the URL parameter like this:

```jsx
<Route path="/user/:userId" element={<UserProfile />} />
```

### 6. **`Link` Component**

Use the `Link` component to create navigation links between routes without reloading the page.

```jsx
import { Link } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
}
```

#### **`Link` Component Properties:**
- `to`: The path to navigate to (required).
- `replace`: If `true`, replaces the current entry in the history stack instead of pushing a new entry.
- `state`: Pass custom state data to the next route.

```jsx
<Link to="/about" replace={true} state={{ from: 'home' }}>Go to About</Link>
```

### 7. **`NavLink` Component**

`NavLink` is similar to `Link`, but it adds styling to indicate when the link is active (useful for navigation bars).

```jsx
import { NavLink } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <NavLink to="/" style={({ isActive }) => ({ color: isActive ? 'red' : 'blue' })}>
        Home
      </NavLink>
      <NavLink to="/about" style={({ isActive }) => ({ color: isActive ? 'red' : 'blue' })}>
        About
      </NavLink>
    </nav>
  );
}
```

#### **`NavLink` Component Properties:**
- `to`: The path to navigate to (required).
- `end`: If `true`, the active styling is only applied if the URL matches the exact path.
- `style`: A function that takes an object with `isActive` and returns a style object.
- `className`: Similar to `style`, but returns a class name based on whether the link is active.

```jsx
<NavLink to="/" className={({ isActive }) => isActive ? "active" : ""}>Home</NavLink>
```

### 8. **Nested Routes**

You can nest routes by placing `<Route>` components inside other `<Route>` components.

```jsx
function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />}>
        <Route path="about" element={<About />} />
      </Route>
    </Routes>
  );
}
```

To render the nested route's component, use the `<Outlet>` component inside the parent component.

```jsx
import { Outlet } from 'react-router-dom';

function Home() {
  return (
    <div>
      <h1>Home</h1>
      <Outlet />
    </div>
  );
}
```

### 9. **`Navigate` Component**

Redirect users to a different route using the `Navigate` component.

```jsx
import { Navigate } from 'react-router-dom';

function ProtectedRoute({ isLoggedIn }) {
  return isLoggedIn ? <Dashboard /> : <Navigate to="/login" />;
}
```

### 10. **404 Page (Catch-All Route)**

To handle 404 pages, use the `*` wildcard path to catch all unmatched routes.

```jsx
<Route path="*" element={<NotFound />} />
```

### 11. **`useLocation`**

Get the current location object, including the current URL and other details using the `useLocation` hook.

```jsx
import { useLocation } from 'react-router-dom';

function ShowLocation() {
  const location = useLocation();

  return <div>Current URL: {location.pathname}</div>;
}
```

### 12. **Search Params (`useSearchParams`)**

Use `useSearchParams` to read and update the query parameters in the URL.

```jsx
import { useSearchParams } from 'react-router-dom';

function SearchPage() {
  const [searchParams, setSearchParams] = useSearchParams();

  return (
    <div>
      <h1>Search: {searchParams.get('query')}</h1>
      <button onClick={() => setSearchParams({ query: 'newQuery' })}>
        Update Query
      </button>
    </div>
  );
}
```

## Summary of Commonly Used APIs:
- `<BrowserRouter>`: Enables routing.
- `createBrowserRouter` and `RouterProvider`: An alternative for routing using an object-based approach.
- `<Routes>` and `<Route>`: Define routes.
- `useNavigate`: Programmatic navigation.
- `useParams`: Access URL parameters.
- `Link` and `NavLink`: Create navigation links with options for styling active links.
- `Navigate`: Redirect users.
- `useLocation`: Access current location.
- `useSearchParams`: Work with query parameters.

---

This guide now includes the `createBrowserRouter` and additional details about `Link` and `NavLink` properties to help with navigation in React Router DOM v6. For more advanced topics, refer to the [official documentation](https://reactrouter.com/en/main).