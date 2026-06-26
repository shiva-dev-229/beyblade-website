# Bug Bistro — A Fictional Edible-Insect Restaurant

> A playful React web app for an imaginary restaurant that serves **edible insects**. Browse a full bug-based menu by course, build your own three-course order, and watch the total update — a creative front-end project with a real-world hook: insects are one of the most sustainable protein sources on the planet.

---

## About

**Bug Bistro** is a concept restaurant site built as a React app. It takes the familiar restaurant-menu format and applies it to entomophagy — eating insects — presenting bug-based dishes the same way any restaurant would present its menu, complete with nutrition info, prices, and descriptions.

The project is half creative concept, half front-end exercise: behind the fun premise, it's a data-driven app that demonstrates React state management, lifting state across components, and computed values.

---

## Features

- **Full themed menu** — ten dishes across three courses (Appetizers, Main Dishes, Desserts), each listing its calories, protein, price, the insects it features, and recommended sides. (Where else can you order Tomato Soup with crickets, a Lemon-Ant Stir Fry, or a Tarantula dessert?)
- **Build-your-order interface** — pick one dish per course; selections are tracked in React state.
- **Live price total** — a "Buy" button tallies the chosen dishes through a `calcPrice` helper and displays the order total.
- **Q&A section** — a data-driven list of questions and answers about the concept, rendered by mapping over a questions dataset.

---

## How it's built

The app keeps its content separate from its presentation, which makes the menu easy to extend:

- **`src/Public/Data.js`** — the menu itself (dishes grouped into `appetizer`, `main_dish`, and `dessert`) plus the `calcPrice` helper. Adding a dish is just adding an object here.
- **`src/Components/Menu.js`** — holds the order state (one selection per course) and renders each course via the reusable `Food` component; the "Buy" button computes the total.
- **`src/Components/Food.js`** — renders a course's dishes as selectable cards.
- **`src/Components/QA.js`** — renders the Q&A by mapping over the questions data.
- **`src/Components/Title.js` / `Minibar.js`** — page chrome.

```
src/
├── App.js                  # Title + Menu + Q&A + Minibar
├── Components/
│   ├── Menu.js             # Order state + live total
│   ├── Food.js             # Selectable dish cards
│   ├── QA.js / Question(s) # Q&A section
│   ├── Title.js
│   └── Minibar.js
├── Public/
│   └── Data.js             # Menu data + price logic
└── Index.scss              # SCSS styling
```

---

## Getting started

This is a [Create React App](https://create-react-app.dev/) project.

```bash
npm install      # install dependencies
npm start        # run locally at http://localhost:3000
npm run build    # production build
```

---

## Tech stack

- **React 18** — components, `useState`, lifted state, computed totals
- **SCSS** — styling
- **react-icons** — iconography
- **Create React App** — tooling

---

## The real point

Behind the novelty, edible insects are a genuinely serious idea: they require a fraction of the land, water, and feed of conventional livestock per gram of protein, and are a staple food for billions of people worldwide. Bug Bistro dresses that idea up as a restaurant you'd actually want to order from.
