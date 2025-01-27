# About React Router

Keturah Smith, Jan 2025

References: -[Step by step](https://hygraph.com/blog/routing-in-react)

## _Description_:

## Core Concepts:

## Getting set up:

1. npm install react-router-dom
2. In Wherever App is rendered, import BrowserRouter, and wrap `<BroswerRouter>` around `<App /`
   `import { BrowserRouter } from 'react-router-dom';`
3. In App.jsx, use syntax to establish routes:

```js
// App.js
import { Routes, Route } from "react-router-dom";
import Home from "./Pages/Home";
import About from "./Pages/About";
import Products from "./Pages/Products";

const App = () => {
  return (
    <>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/products" element={<Products />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </>
  );
};

export default App;
```

4. Navbar code if applicable:

```js
// component/NavBar.js

import { NavLink } from "react-router-dom";

const NavBar = () => {
  return (
    <nav>
      <ul>
        <li>
          <NavLink to="/">Home</NavLink>
        </li>
        <li>
          <NavLink to="/about">About</NavLink>
        </li>
        <li>
          <NavLink to="/products">Products</NavLink>
        </li>
      </ul>
    </nav>
  );
};

export default NavBar;
```

5. Programatic Navigation example:

```js
import { useNavigate } from "react-router-dom";

const Products = () => {
  const navigate = useNavigate();
  return (
    <div className="container">
      <div className="title">
        <h1>Order Product CockTails</h1>
      </div>
      <button className="btn" onClick={() => navigate("order-summary")}>
        Place Order
      </button>
    </div>
  );
};

export default Products;
```

### Projects Used:

- []()
