# Sulayman Seid Ymam — Personal Website
### Laboratory Work 1 & 2 | Lobachevsky University

A personal portfolio website built across two lab assignments, progressively adding HTML/CSS structure (Lab 1) and JavaScript DOM manipulation with prototype-based inheritance (Lab 2).

---

## Project Structure

```
/
├── main.html       # Single-file application (HTML + CSS + JS)
├── pic.jpg         # Profile photo
└── README.md       # This file
```

---

## Lab 1 — HTML & CSS

**Objective:** Build a well-structured personal portfolio page with clean styling.

### Task 1 — Page Setup & Profile Header

The page opens with a `<header>` containing a profile photo loaded via `<img>` and a name/subtitle.

```html
<header>
  <img
    class="profile-img"
    src="./pic.jpg"
    alt="Profile photo of Sulayman Seid Ymam"
  />
  <h1>Sulayman Seid Ymam</h1>
  <p>Information Technology Student · DevOps Engineer · Tech Enthusiast</p>
</header>
```

The profile image is made circular and centred with CSS:

```css
.profile-img {
  width: 130px;
  height: 130px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #7f5af0;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
```

---

### Task 2 — About Me Section

A `<section>` tag holds a descriptive paragraph about interests, goals, and background.

```html
<section id="about">
  <h2>About Me</h2>
  <p>
    I'm a 3rd-year Information Technology student at
    <strong>Lobachevsky University</strong>, but my real passion lies in
    <strong>DevOps</strong>. I love working close to the metal — setting up
    Linux servers, writing automation scripts, containerising services...
  </p>
</section>
```

---

### Task 3 — Education & Skills Lists

`<ul>` and `<li>` elements present education history and key technical skills side by side using a flex layout.

```html
<ul class="styled-list">
  <li>B.Sc. Information Technology — Lobachevsky University (2023–2027)</li>
  <li>IT Specialist — Google (2021)</li>
  <li>Network Security — Microsoft (2024)</li>
</ul>
```

Custom bullet styling using CSS `::before` pseudo-element:

```css
.styled-list li::before {
  content: '▸';
  color: #7f5af0;
  font-size: 0.85rem;
  flex-shrink: 0;
}
```

---

### Task 4 — Projects Section

Three project cards, each describing a real self-hosted infrastructure project. Cards use a `display: flex` grid with hover lift effects.

```html
<div class="project-card">
  <div class="card-header">
    <div class="card-icon">🕷️</div>
    <div>
      <h3>Python Web Scraper</h3>
      <span class="card-sub">Automation · Data Collection</span>
    </div>
  </div>
  <p>A Python-based scraping tool that extracts structured data...</p>
  <span class="tag">Python</span>
  <span class="tag">BeautifulSoup</span>
</div>
```

Hover animation:

```css
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(127, 90, 240, 0.12);
}
```

---

### Task 5 — External Stylesheet (Linked CSS)

In a multi-file setup the `<style>` block moves to an external `style.css` and is linked in `<head>`:

```html
<link rel="stylesheet" href="style.css" />
```

For this single-file lab submission all styles are kept in the embedded `<style>` block, which maps directly to that external file structure.

---

### Task 6 — Block & Flex Layout (CSS Box Model)

A `.container` class centres content with a max-width and auto margins (block layout).  
A `.two-col` flex wrapper puts Education and Skills side by side.  
The projects grid also uses flex with wrapping for responsiveness.

```css
/* Block container */
.container {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 24px;
}

/* Flex two-column layout */
.two-col {
  display: flex;
  gap: 48px;
  flex-wrap: wrap;
}

/* Flex project grid */
.projects-grid {
  display: flex;
  gap: 24px;
  flex-wrap: wrap;
}
```

---

### Task 7 — Navigation Menu

A sticky `<nav>` bar with `<ul>` / `<li>` / `<a>` elements links to each page section via anchor IDs.

```html
<nav>
  <ul>
    <li><a href="#about">About</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
```

```css
nav {
  background-color: #1a1a2e;
  position: sticky;
  top: 0;
  z-index: 100;
}

nav ul li a:hover {
  color: #7f5af0;
}
```

---

## Lab 2 — JavaScript DOM Manipulation & Prototypes

**Objective:** Add dynamic interactivity using DOM manipulation and demonstrate prototype-based inheritance.

---

### Task 1 — CSS Variables & Dark/Light Theme (DOM)

CSS custom properties (variables) allow the entire colour palette to switch with a single attribute change on `<html>`.

```css
:root {
  --bg:        #f4f6fb;
  --accent:    #7f5af0;
  --nav-bg:    #1a1a2e;
  --text:      #2d2d2d;
  --border:    #e2e8f0;
}

[data-theme="dark"] {
  --bg:        #0f0f1a;
  --accent:    #9d7df5;
  --nav-bg:    #0a0a14;
  --text:      #e0e0f0;
}
```

JavaScript toggles the attribute on button click:

```js
btn.addEventListener('click', function () {
  dark = !dark;
  if (dark) {
    document.documentElement.setAttribute('data-theme', 'dark');
    btn.textContent = '☀ Light';
  } else {
    document.documentElement.removeAttribute('data-theme');
    btn.textContent = '🌙 Dark';
  }
});
```

---

### Task 2 — Typing Animation (DOM Manipulation)

A self-invoking function cycles through an array of subtitle phrases, updating the text content of a `<span>` character by character to create a typewriter effect.

```js
(function typewriter() {
  const phrases = [
    'Information Technology Student',
    'DevOps Engineer',
    'Linux Enthusiast',
    'Open-Source Builder'
  ];
  let pi = 0, ci = 0, deleting = false;
  const el = document.getElementById('typed-text');

  function tick() {
    const phrase = phrases[pi];
    if (!deleting) {
      el.textContent = phrase.slice(0, ++ci);       // add one character
      if (ci === phrase.length) {
        deleting = true;
        setTimeout(tick, 1600);                     // pause before deleting
        return;
      }
    } else {
      el.textContent = phrase.slice(0, --ci);       // remove one character
      if (ci === 0) {
        deleting = false;
        pi = (pi + 1) % phrases.length;            // advance to next phrase
      }
    }
    setTimeout(tick, deleting ? 45 : 80);
  }
  tick();
})();
```

The blinking cursor is a pure CSS animation:

```css
.cursor {
  display: inline-block;
  width: 2px; height: 1em;
  background: var(--accent);
  animation: blink 0.75s step-end infinite;
}
@keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }
```

---

### Task 3 — Project Filter Buttons (DOM Manipulation)

Filter buttons dynamically show or hide project cards based on their technology tags, without any page reload.

```html
<div class="filter-bar" id="filter-bar">
  <button class="filter-btn active" data-filter="all">All</button>
  <button class="filter-btn" data-filter="Python">Python</button>
  <button class="filter-btn" data-filter="Docker">Docker</button>
  <button class="filter-btn" data-filter="Ansible">Ansible</button>
</div>
```

```js
document.getElementById('filter-bar').addEventListener('click', function (e) {
  if (!e.target.matches('.filter-btn')) return;

  // Update active state on buttons
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  e.target.classList.add('active');

  // Re-render cards with selected filter
  renderProjects(e.target.dataset.filter);
});
```

Cards are shown or hidden inside `renderProjects()` using the `hasTag()` method inherited from the prototype:

```js
function renderProjects(filter) {
  const grid = document.getElementById('projects-grid');
  grid.innerHTML = '';
  projects.forEach(function (p) {
    const card = p.render();
    if (filter && filter !== 'all' && !p.hasTag(filter)) {
      card.classList.add('hidden');   // CSS: display: none
    }
    grid.appendChild(card);
  });
}
```

---

### Task 4 — Expandable Project Details (DOM Manipulation)

Each project card has a "Show details" button that toggles the feature list open and closed using CSS `max-height` transition and a class toggle.

```js
// Inside ProjectCard.prototype.render()
const btn  = card.querySelector('.toggle-details-btn');
const list = card.querySelector('.feature-list');

btn.addEventListener('click', function () {
  const isOpen = list.classList.toggle('expanded');  // toggle class
  btn.classList.toggle('open', isOpen);
  btn.querySelector('.arrow').nextSibling.textContent =
    isOpen ? ' Hide details' : ' Show details';
});
```

```css
.feature-list {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s ease;
}
.feature-list.expanded {
  max-height: 200px;   /* triggers CSS transition */
}
```

---

### Task 5 — Scroll Reveal (DOM + IntersectionObserver)

Sections start invisible and slide up into view as the user scrolls, using the browser's `IntersectionObserver` API.

```css
.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible {
  opacity: 1;
  transform: none;
}
```

```js
const observer = new IntersectionObserver(function (entries) {
  entries.forEach(function (entry) {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');  // triggers CSS transition
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
```

---

### Task 6 — Prototype-based Inheritance

Three constructor functions form a two-level inheritance chain.

#### Base Constructor — `PortfolioItem`

```js
function PortfolioItem(name, tags) {
  this.name = name;
  this.tags = tags || [];
}

// Shared method — available to all inheriting constructors
PortfolioItem.prototype.tagSummary = function () {
  return this.tags.join(' · ');
};

PortfolioItem.prototype.hasTag = function (tag) {
  return this.tags.includes(tag);
};
```

#### Child Constructor — `ProjectCard`

```js
function ProjectCard(name, icon, subtitle, description, features, tags) {
  PortfolioItem.call(this, name, tags);   // call parent constructor
  this.icon        = icon;
  this.subtitle    = subtitle;
  this.description = description;
  this.features    = features || [];
}

// Set up prototype chain
ProjectCard.prototype = Object.create(PortfolioItem.prototype);
ProjectCard.prototype.constructor = ProjectCard;

// Own method — renders a DOM card element
ProjectCard.prototype.render = function () {
  const card = document.createElement('div');
  card.className = 'project-card';
  // ... builds innerHTML, attaches event listeners, returns card
  return card;
};
```

#### Child Constructor — `SkillBar`

```js
function SkillBar(name, icon, level, tags) {
  PortfolioItem.call(this, name, tags);
  this.icon  = icon;
  this.level = level;   // 0-100
}

SkillBar.prototype = Object.create(PortfolioItem.prototype);
SkillBar.prototype.constructor = SkillBar;

// Own method — returns a text label for the level
SkillBar.prototype.levelLabel = function () {
  if (this.level >= 80) return 'Advanced';
  if (this.level >= 55) return 'Proficient';
  return 'Familiar';
};

// Own method — renders a DOM skill bar element
SkillBar.prototype.render = function () {
  const item = document.createElement('div');
  item.className = 'skill-bar-item';
  item.innerHTML = `
    <div class="skill-bar-label">
      <span>${this.icon} ${this.name}</span>
      <span>${this.levelLabel()} — ${this.level}%</span>
    </div>
    <div class="skill-bar-track">
      <div class="skill-bar-fill" data-level="${this.level}"></div>
    </div>
  `;
  return item;
};
```

#### Prototype Chain Verification

The on-page console widget proves the chain is correct:

```js
projects[0] instanceof ProjectCard   // → true
projects[0] instanceof PortfolioItem // → true  (inherited)
skills[0]   instanceof SkillBar      // → true
skills[0]   instanceof PortfolioItem // → true  (inherited)

ProjectCard.prototype.hasOwnProperty('render')      // → true  (own)
ProjectCard.prototype.hasOwnProperty('tagSummary')  // → false (inherited)

projects[1].tagSummary()
// → "Docker · Ansible · Linux · Bash · Virtualization"
```

---

### Task 7 — Animated Skill Bars (DOM + CSS Transition)

Skill bars start at `width: 0` and animate to their real value when the Education section scrolls into view. This is triggered by the `IntersectionObserver` from Task 5.

```js
function animateSkillBars() {
  document.querySelectorAll('.skill-bar-fill').forEach(function (fill) {
    const level = fill.dataset.level;       // read from data attribute
    setTimeout(function () {
      fill.style.width = level + '%';       // triggers CSS width transition
    }, 100);
  });
}
```

```css
.skill-bar-fill {
  height: 100%;
  background: var(--accent);
  width: 0;
  transition: width 1s ease;   /* animates when JS sets the width */
}
```

---

## Git Workflow

```bash
# Initialise repository
git init
git add main.html pic.jpg README.md

# Lab 1 commit
git commit -m "feat: Lab 1 – HTML structure and CSS styling"

# Create Lab 2 branch
git checkout -b lab2-js

# Lab 2 commit
git commit -m "feat: Lab 2 – DOM manipulation and prototype inheritance"

# Push both branches to GitHub
git remote add origin https://github.com/Sulaiman3352/Laboratory_2.git
git push -u origin main
git push -u origin lab2-js
```

---

## Technologies Used

| Technology | Purpose |
|---|---|
| HTML5 | Page structure and semantic markup |
| CSS3 | Styling, Flexbox layout, custom properties, transitions |
| JavaScript (ES5/ES6) | DOM manipulation, prototype inheritance, animations |
| Google Fonts | `Inter` (body) + `Space Mono` (headings/code) |
| IntersectionObserver API | Scroll reveal and skill bar trigger |
| Git / GitHub | Version control and submission |

---

## Author

**Sulayman Seid Ymam**  
B.Sc. Information Technology, Lobachevsky University (2023–2027)  
[sulaiman3352@email.com](mailto:sulaiman3352@email.com) · [GitHub](https://github.com/Sulaiman3352)
