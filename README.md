## .*hyb

# HYB — Hybrid Template Engine and Runtime

**HYB** is a hybrid template language and runtime designed for building clean, declarative, and reactive web documents without embedded JavaScript or complex dependencies.  
It compiles `.hyb` files — combining HTML and logic — into pure static HTML plus a single hydration runtime (`hydrator.js`).

Developed as part of a Master’s degree research project at the Faculty of Fine Arts, University of Porto.

---

## 1. General Structure

`.hyb` templates are composed of standard HTML nodes mixed with declarative logic blocks and bindings.  
Everything compiles into static HTML plus a single hydration runtime.


Document ::= (MetaBlock | Node)*


---

## 2. Metadata Blocks

Define local state or schema context for the component or section.

```html
@state { count: 0, open: false }
@schema { title: "string", items: "array" }
````

---

## 3. Control Structures

Declarative flow using JavaScript expressions.

```html
@for item in items
  <li>{{ item }}</li>
@endfor

@if open
  <p>Panel is open</p>
@else
  <p>Panel is closed</p>
@endif
```

---

## 4. Attributes & Bindings

* `:attr="expr"` — dynamic attribute
* `!event="expr"` — inline JS event
* `^js="ref"` / `^js*="listRef"` — virtual refs (not rendered in HTML)

```html
<button :class="open ? 'active' : ''" !click="open = !open">Toggle</button>
```

---

## 5. Interpolation

Inline JavaScript expressions using double braces.

```html
<h1>{{ title }}</h1>
<p>{{ count + 1 }}</p>
```

---

## 6. Compiler Output

The compiler produces **pure HTML**, without `data-*` attributes or runtime markup.
It generates a single `hydrator.js` containing:

* Selector registry
* Event and binding logic
* Reactive state system

**Example**

**Input (.hyb)**

```html
@state { count: 0 }

<div class="counter">
  <button !click="count--">-</button>
  <span>{{ count }}</span>
  <button !click="count++">+</button>
</div>
```

**Output (HTML)**

```html
<div class="counter">
  <button>-</button>
  <span>0</span>
  <button>+</button>
</div>
<script src="/hydrator.js"></script>
```

The **hydrator** reattaches logic on load, maintaining full interactivity with zero inlined JavaScript or identifiers.

---

## 7. Project Context

This system is part of a research project titled
**“Desmaterialização da Página” (The Dematerialisation of the Page)** —
a study exploring the intersection between editorial design and web development.
The project aims to rethink the website as a modular document built through composition rather than frameworks,
bridging the logic of design and the logic of code.

Faculty of Fine Arts, University of Porto — Master’s in Graphic Design and Editorial Projects.
Institutional email: **[up201406900@up.pt](mailto:up201406900@up.pt)**

---

## 8. License and Attribution

© 2025 Julien Lima — Faculty of Fine Arts, University of Porto
Licensed under the **MIT License**
