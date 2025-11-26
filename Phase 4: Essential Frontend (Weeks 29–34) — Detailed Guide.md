# **Phase 4: Essential Frontend (Weeks 29–34) — Detailed Guide**

This phase introduces learners to **frontend development** and connecting it to their **Python backend APIs**. The goal is to build a **portfolio-ready frontend** with responsive design, minimal interactivity, and optional React/NextJS integration.

---

## **1. HTML & CSS Basics (Weeks 29–30)**

**Purpose:** Structure content and style pages.

### **1.1 HTML Structure**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Portfolio</title>
</head>
<body>
    <header>
        <h1>My Projects</h1>
    </header>
    <main>
        <section id="projects"></section>
    </main>
    <footer>
        <p>&copy; 2025 My Portfolio</p>
    </footer>
</body>
</html>
```

### **1.2 CSS Styling**

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}
header {
    background-color: #333;
    color: white;
    padding: 1rem;
    text-align: center;
}
main {
    padding: 2rem;
}
```

### **Assignment:** Build a multi-section **portfolio landing page** using HTML and CSS, fully responsive with flexbox or grid.

---

## **2. Minimal JavaScript for API Integration (Weeks 31–32)**

**Purpose:** Fetch data from backend APIs and display dynamically.

### **2.1 Fetch Example**

```javascript
fetch('http://localhost:8000/posts/')
    .then(response => response.json())
    .then(data => {
        const container = document.getElementById('projects');
        data.forEach(post => {
            const div = document.createElement('div');
            div.innerHTML = `<h2>${post.title}</h2><p>${post.content}</p>`;
            container.appendChild(div);
        });
    })
    .catch(err => console.error('Error fetching posts:', err));
```

### **2.2 Assignment**

* Fetch posts or notes from your backend
* Display in a **grid or card layout**
* Handle loading states and errors gracefully

---

## **3. ReactJS / NextJS (Optional) (Weeks 33–34)**

**Purpose:** Build modern frontend with reusable components, state management, and API interaction.

### **3.1 React Functional Component Example**

```javascript
import React, { useEffect, useState } from "react";

function Projects() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch("http://localhost:8000/posts/")
      .then(res => res.json())
      .then(data => setPosts(data))
      .catch(err => console.error(err));
  }, []);

  return (
    <div>
      {posts.map(post => (
        <div key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.content}</p>
        </div>
      ))}
    </div>
  );
}

export default Projects;
```

### **3.2 NextJS Page Example**

```javascript
import Projects from "../components/Projects";

export default function Home() {
  return (
    <main>
      <h1>My Portfolio</h1>
      <Projects />
    </main>
  );
}
```

### **Assignment**

* Create a **React or NextJS frontend**
* Connect to your Python backend API
* Implement a **simple portfolio site** showing your projects dynamically

---

## **4. Project: Portfolio Website**

### **Features**

1. Landing page with project sections
2. Fetch and display backend posts, notes, or API data
3. Responsive design for mobile and desktop
4. Optional: React/NextJS with reusable components
5. Loading/error handling for API data

### **Suggested File Structure**

```
portfolio-frontend/
├─ index.html        # Static HTML
├─ style.css         # CSS
├─ script.js         # Vanilla JS API fetch
├─ package.json      # If using React/NextJS
├─ src/
│   ├─ components/
│   └─ pages/
└─ README.md
```

---

## **5. Learning Outcomes (Weeks 29–34)**

By the end of this phase, learners will be able to:

* Build **responsive web pages** using HTML and CSS
* Fetch data from **Python backend APIs** using JavaScript
* Create dynamic, interactive UIs with **React or NextJS**
* Integrate frontend with backend to produce a **production-ready portfolio website**
* Handle **loading states, errors, and basic client-side validation**

---

## **6. Assignments**

1. **HTML/CSS:** Build responsive landing page for portfolio
2. **JavaScript:** Fetch backend data, display dynamically, handle errors
3. **React/NextJS (Optional):** Build component-based portfolio connecting to API
4. **Portfolio Project:** Deploy a full stack portfolio website (backend + frontend)
5. **Optional Enhancements:** Add routing, state management, or styling frameworks (Tailwind, Bootstrap)

---
