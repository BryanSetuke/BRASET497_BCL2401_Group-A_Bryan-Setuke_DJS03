# Book Connect

Welcome to **Book Connect** – your gateway to discovering and exploring a world of literary adventures! Whether you're a fan of thrilling mysteries, epic fantasies, or heartwarming romances, Book Connect brings the magic of books directly to you. Happy reading!

## Project Overview

The "Book Connect" project aims to provide a refined and fully functional version of a book browsing application. The focus is on enhancing the code's maintainability, extendibility, and readability by applying concepts of objects and functions for abstraction. This will streamline future modifications and consolidate a deeper understanding of higher-level programming concepts, including documentation, style guides, and abstraction principles.

![Book Connect](image.png)

## Goals

- **Refactor Existing Code**: Analyse and refactor the existing JavaScript and HTML code to improve its structure using objects and functions.
- **Implement Abstraction**: Use abstraction to hide complex realities while exposing only the necessary parts, creating more generic functions that can perform tasks flexibly.
- **Documentation**: Write clear comments and documentation for the new code structure to explain the purpose and functionality of code blocks, functions, and objects.
- **Follow Style Guides**: Adhere to established coding conventions and style guides to ensure code readability and maintainability.

## Tasks

1. **Code Analysis**: Understand the current implementation of the "Book Connect" application, including its HTML structure and JavaScript functionality.
2. **Plan Refactoring**: Identify sections of the code that can be made more abstract and modular. Look for patterns and repetitive code that can be simplified.
3. **Implement Abstraction**:
   - **Objects**: Define objects to represent key elements of the application, such as books, authors, and genres. Utilize the provided data (e.g., `authors`, `genres`, `books`) to populate these objects.
   - **Functions**: Create functions that handle repetitive tasks, such as rendering the book list, handling user interactions, and applying filters.
4. **Enhance Functionality**: Ensure the application remains fully functional after refactoring. Test all features to confirm users can still search, filter, and view books as intended.
5. **Documentation and Comments**: Throughout the refactoring process, document your code. Provide comments that explain the purpose and functionality of objects and functions.

## Challenges and Learnings

### Challenges

1. **Understanding Legacy Code**: One of the initial challenges was understanding the existing codebase. It was a mix of intertwined JavaScript and HTML with minimal documentation, making it hard to decipher the flow and functionality.
2. **Implementing Abstraction**: Moving from a procedural code structure to an abstracted, object-oriented approach was challenging. It required a deep understanding of how to generalize functions and create modular code blocks.
3. **Maintaining Functionality**: Ensuring that the application remained fully functional throughout the refactoring process was crucial. This meant constant testing and debugging to catch any issues that arose from changes in the code structure.

### Learnings

1. **Importance of Abstraction**: Abstraction proved to be a powerful tool in simplifying the codebase. By hiding complex details and exposing only necessary components, the code became more manageable and extendable.
2. **Enhanced Readability and Maintainability**: The refactoring process emphasized the value of writing clean, readable, and maintainable code. Adhering to style guides and documenting the code made it easier to understand and modify.
3. **Effective Use of Functions and Objects**: Creating reusable functions and defining clear objects for books, authors, and genres improved the overall structure and efficiency of the application. This modular approach made it easier to implement new features and changes.

## Code Overview

The refactored code is structured to enhance readability and maintainability. Below is a brief overview of the key components:

### Importing Data

```javascript
// Import necessary data and constants from data.js
import { books, authors, genres, BOOKS_PER_PAGE } from "./data.js";
```

### Initialization

```javascript
let page = 1;
let matches = books; // Initially, all books are considered matches
```

### Utility Functions

```javascript
const getElement = (selector) => document.querySelector(selector);
```

### Creating Book Previews

```javascript
const createBookPreviews = (books, container) => {
    const fragment = document.createDocumentFragment();
    books.forEach(({ author, id, image, title }) => {
        const element = document.createElement("button");
        element.classList = "preview";
        element.setAttribute("data-preview", id);
        element.innerHTML = `
      <img class="preview__image" src="${image}" />
      <div class="preview__info">
        <h3 class="preview__title">${title}</h3>
        <div class="preview__author">${authors[author]}</div>
      </div>
    `;
        fragment.appendChild(element);
    });
    container.appendChild(fragment);
};
```

### Creating Options

```javascript
const createOptions = (options, defaultOption, container) => {
    const fragment = document.createDocumentFragment();
    const firstOption = document.createElement("option");
    firstOption.value = "any";
    firstOption.innerText = defaultOption;
    fragment.appendChild(firstOption);
    Object.entries(options).forEach(([id, name]) => {
        const element = document.createElement("option");
        element.value = id;
        element.innerText = name;
        fragment.appendChild(element);
    });
    container.appendChild(fragment);
};
```

### Applying Themes

```javascript
const applyTheme = (theme) => {
    const isNight = theme === "night";
    document.documentElement.style.setProperty(
        "--color-dark",
        isNight ? "255, 255, 255" : "10, 10, 20"
    );
    document.documentElement.style.setProperty(
        "--color-light",
        isNight ? "10, 10, 20" : "255, 255, 255"
    );
};
```

### Updating "Show More" Button

```javascript
const updateShowMoreButton = () => {
    const remainingBooks = matches.length - page * BOOKS_PER_PAGE;
    const button = getElement("[data-list-button]");
    button.innerText = `Show more (${remainingBooks})`;
    button.disabled = remainingBooks <= 0;
    button.innerHTML = `
    <span>Show more</span>
    <span class="list__remaining">(${
        remainingBooks > 0 ? remainingBooks : 0
    })</span>
  `;
};
```

### Event Listeners

```javascript
const closeOverlay = (selector) => {
    getElement(selector).open = false;
};

const openOverlay = (selector, focusSelector = null) => {
    getElement(selector).open = true;
    if (focusSelector) getElement(focusSelector).focus();
};

// Other event listener functions go here...
```

### Initial Setup

```javascript
createOptions(genres, "All Genres", getElement("[data-search-genres]"));
createOptions(authors, "All Authors", getElement("[data-search-authors]"));
applyTheme(
    window.matchMedia("(prefers-color-scheme: dark)").matches ? "night" : "day"
);
createBookPreviews(
    matches.slice(0, BOOKS_PER_PAGE),
    getElement("[data-list-items]")
);
updateShowMoreButton();
```

## Conclusion

Refactoring the "Book Connect" project was a valuable learning experience. It underscored the importance of code abstraction, documentation, and adhering to coding standards. By transforming the codebase into a more modular and maintainable structure, future enhancements and modifications will be much more manageable. Happy coding, and happy reading!