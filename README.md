## Events & Event Listeners

**What an event is**

An event is something that happens in the browser — a click, a key press, a form submit, the page finishing loading. JavaScript can "listen" for these events and run code in response. This is what makes a page interactive instead of static.

**Adding an event listener — the standard way**

```jsx
const button = document.querySelector("#myButton");

button.addEventListener("click", function () {
  console.log("Button clicked!");
});
```

`addEventListener` takes two main things: the event name (as a string) and a function to run when it happens (called a **callback function**).

**Using a named function instead of an inline one**

```jsx
function handleClick() {
``````jsx
  console.log("Button clicked!");
}

button.addEventListener("click", handleClick);
```

Note: no `()` after `handleClick` here — you're passing the function itself to run later, not calling it immediately.

**Arrow function version**

```jsx
button.addEventListener("click", () => {
  console.log("Button clicked!");
});
```

---

**Common event types**

```jsx
// Mouse events
button.addEventListener("click", () => {});
button.addEventListener("dblclick", () => {});
button.addEventListener("mouseenter", () => {});
button.addEventListener("mouseleave", () => {});

// Keyboard events
document.addEventListener("keydown", () => {});
document.addEventListener("keyup", () => {});
``````jsx
// Form events
input.addEventListener("input", () => {});    // fires on every keystroke
input.addEventListener("change", () => {});   // fires when value changes AND loses focus
form.addEventListener("submit", () => {});

// Window/page events
window.addEventListener("load", () => {});
window.addEventListener("resize", () => {});
window.addEventListener("scroll", () => {});
```

---

**The event object**

The callback function automatically receives an "event object" with details about what happened — pass a parameter to access it (commonly named `e` or `event`).

```jsx
button.addEventListener("click", function (e) {
  console.log(e);          // the whole event object
  console.log(e.target);   // the exact element that was clicked
});
```

**Using the event object with keyboard input**

```jsx
document.addEventListener("keydown", function (e) {
  console.log(e.key);   // which key was pressed, e.g. "Enter", "a", "Shift"
});
```

**Getting input values**

```html
<input type="text" id="nameInput">
<button id="submitBtn">Submit</button>
```

```jsx
const input = document.querySelector("#nameInput");
const btn = document.querySelector("#submitBtn");

btn.addEventListener("click", function () {
  console.log(input.value);   // reads whatever the user typed
});
```

---

**Preventing default behavior**

Some elements have built-in default behavior — a form reloads the page on submit, a link navigates away. `e.preventDefault()` stops that default action so you```jsx
// Form events
input.addEventListener("input", () => {});    // fires on every keystroke
input.addEventListener("change", () => {});   // fires when value changes AND loses focus
form.addEventListener("submit", () => {});

// Window/page events
window.addEventListener("load", () => {});
window.addEventListener("resize", () => {});
window.addEventListener("scroll", () => {});
```

---

**The event object**

The callback function automatically receives an "event object" with details about what happened — pass a parameter to access it (commonly named `e` or `event`).

```jsx
button.addEventListener("click", function (e) {
  console.log(e);          // the whole event object
  console.log(e.target);   // the exact element that was clicked
});
```

**Using the event object with keyboard input**

```jsx
document.addEventListener("keydown", function (e) {
  console.log(e.key);   // which key was pressed, e.g. "Enter", "a", "Shift"
});
```

**Getting input values**

```html
<input type="text" id="nameInput">
<button id="submitBtn">Submit</button>
```

```jsx
const input = document.querySelector("#nameInput");
const btn = document.querySelector("#submitBtn");

btn.addEventListener("click", function () {
  console.log(input.value);   // reads whatever the user typed
});
```

---

**Preventing default behavior**

Some elements have built-in default behavior — a form reloads the page on submit, a link navigates away. `e.preventDefault()` stops that default action so youcan handle it with your own JS instead.

```jsx
const form = document.querySelector("#myForm");

form.addEventListener("submit", function (e) {
  e.preventDefault();   // stops the page from reloading
  console.log("Form submitted without reload");
});
```

This is essential for forms in JS-driven pages — without it, every submit reloads the page and any JS logic effectively "resets."

---

**Event delegation — a useful pattern**

Instead of adding a listener to every individual item (especially ones created dynamically), add one listener to a shared parent and check what was actually clicked.

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```jsx
const list = document.querySelector("#list");

list.addEventListener("click", function (e) {
  if (e.target.tagName === "LI") {
    console.log("You clicked:", e.target.textContent);
  }
});
```

This one listener works for all current `<li>`s *and* any new ones added later dynamically — adding individual listeners to each wouldn't cover future items.

---

**Removing an event listener**

```jsx
function handleClick() {
  console.log("Clicked");
}

button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);
```

Only works if the same named function reference is used in both calls — an inline/anonymous function can't be removed this way, since there's no reference to point back to.

---

**A practical mini example — toggle a class on click**

```html
<button id="toggleBtn">Toggle</button>
<div id="box">Hello</div>
```

```jsx
const btn = document.querySelector("#toggleBtn");
const box = document.querySelector("#box");

btn.addEventListener("click", function () {
  box.classList.toggle("active");
});
```

**Common mistakes**

- Writing `button.addEventListener("click", handleClick())` — the `()` calls it immediately instead of passing it as a reference
- Forgetting `e.preventDefault()` on form submissions, so the page reloads unexpectedlycan handle it with your own JS instead.

```jsx
const form = document.querySelector("#myForm");

form.addEventListener("submit", function (e) {
  e.preventDefault();   // stops the page from reloading
  console.log("Form submitted without reload");
});
```

This is essential for forms in JS-driven pages — without it, every submit reloads the page and any JS logic effectively "resets."

---

**Event delegation — a useful pattern**

Instead of adding a listener to every individual item (especially ones created dynamically), add one listener to a shared parent and check what was actually clicked.

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

```jsx
const list = document.querySelector("#list");

list.addEventListener("click", function (e) {
  if (e.target.tagName === "LI") {
    console.log("You clicked:", e.target.textContent);
  }
});
```

This one listener works for all current `<li>`s *and* any new ones added later dynamically — adding individual listeners to each wouldn't cover future items.

---

**Removing an event listener**

```jsx
function handleClick() {
  console.log("Clicked");
}

button.addEventListener("click", handleClick);
button.removeEventListener("click", handleClick);
```

Only works if the same named function reference is used in both calls — an inline/anonymous function can't be removed this way, since there's no reference to point back to.

---

**A practical mini example — toggle a class on click**

```html
<button id="toggleBtn">Toggle</button>
<div id="box">Hello</div>
```

```jsx
const btn = document.querySelector("#toggleBtn");
const box = document.querySelector("#box");

btn.addEventListener("click", function () {
  box.classList.toggle("active");
});
```

**Common mistakes**

- Writing `button.addEventListener("click", handleClick())` — the `()` calls it immediately instead of passing it as a reference
- Forgetting `e.preventDefault()` on form submissions, so the page reloads unexpectedly
- Adding individual listeners to elements that don't exist yet (created dynamically later) — use event delegation instead
- Confusing `input` event (fires on every keystroke) with `change` event (fires only after losing focus)- Trying to `removeEventListener` an anonymous inline function — it silently fails since there's no matching reference

**Small practice task**# Day-31
dom 2 Events &amp; Event Listeners```html
<!-- Setup: a button, a text input, a form with one input + submit button,
     and a <ul> with 3 <li> items -->
```

```jsx
// 1. Add a click listener to the button that logs a message
// 2. Log the input's value every time the user types (input event)
// 3. Prevent the form from reloading the page on submit, log the submitted value instead
// 4. Use event delegation on the <ul> to log which <li> was clicked
// 5. Add a "keydown" listener on the document that logs which key was pressed
```
