# LaTeX Rendering & Interactive Graphing Reference

This file contains exact boilerplate and patterns for KaTeX math rendering and D3 knowledge graphs. **Copy these patterns exactly** — do not improvise alternatives.

## Table of Contents
1. KaTeX Setup (CDN & Initialization)
2. Inline and Display Math Patterns
3. Common LaTeX Pitfalls in HTML
4. KaTeX in Dynamic Content (Flashcards, Show/Hide)
5. Interactive Knowledge Graph (D3 Force-Directed)
6. Charting with Chart.js (Optional)

---

## 1. KaTeX Setup (CDN & Initialization)

Place these in the `<head>` of every study guide HTML file:

```html
<!-- KaTeX CSS -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.11/katex.min.css"
      integrity="sha512-nQo5wNRbSbMHNGMxcGEKlKSjpHFtG9BoSGPnkGzFMuBTiQaVOvFoMOGy5M/MFss1OHGc9oCEvPDpDR9Y9BJQQ=="
      crossorigin="anonymous" referrerpolicy="no-referrer" />

<!-- KaTeX JS -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.11/katex.min.js"
        integrity="sha512-xoEB1LoaLGZ0rMOjnIGRGU2CUg5Lxa/wPFnQXYELGOvEMB2Yj94QFNkRp5q9tFeQlfBNTKjsSahZ+CPmuVaOQ=="
        crossorigin="anonymous" referrerpolicy="no-referrer"></script>

<!-- KaTeX Auto-render extension -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.16.11/contrib/auto-render.min.js"
        integrity="sha512-cjMHOqHeAOdk5lLdpe8E5w0ANkMsMbVxCnFEEYhHyIG46SFUKNSIAOanMJq8RGVo7xCfuk5XSWAqEwOLLkCkQ=="
        crossorigin="anonymous" referrerpolicy="no-referrer"></script>
```

Then at the **end of `<body>`** (after all content), add the auto-render call:

```html
<script>
  document.addEventListener("DOMContentLoaded", function () {
    renderMathInElement(document.body, {
      delimiters: [
        { left: "$$", right: "$$", display: true },
        { left: "\\[", right: "\\]", display: true },
        { left: "\\(", right: "\\)", display: false },
        { left: "$", right: "$", display: false }
      ],
      throwOnError: false,
      trust: true
    });
  });
</script>
```

**IMPORTANT**: `throwOnError: false` prevents a single bad expression from breaking the entire page.

---

## 2. Inline and Display Math Patterns

### Inline math (within a sentence)
Use `\( ... \)` or `$ ... $`:

```html
<p>The quadratic formula is \( x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} \) where \( a \neq 0 \).</p>
```

### Display math (centered, standalone)
Use `\[ ... \]` or `$$ ... $$`:

```html
\[ \int_a^b f(x)\,dx = F(b) - F(a) \]
```

### Aligned multi-line equations

```html
\[
\begin{aligned}
  \nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\
  \nabla \cdot \mathbf{B} &= 0 \\
  \nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\
  \nabla \times \mathbf{B} &= \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}
\end{aligned}
\]
```

### Cases / piecewise functions

```html
\[
f(x) = \begin{cases}
  x^2 & \text{if } x \geq 0 \\
  -x  & \text{if } x < 0
\end{cases}
\]
```

### Matrices

```html
\[
A = \begin{pmatrix}
  a_{11} & a_{12} \\
  a_{21} & a_{22}
\end{pmatrix}
\]
```

---

## 3. Common LaTeX Pitfalls in HTML

| Mistake | Fix |
|---------|-----|
| Using `<` or `>` raw in math (HTML interprets as tags) | Use `\lt` and `\gt` instead |
| Using `&` raw in math (HTML entity) | Use `\&` or restructure |
| Backslash at end of line in JS string | Double-escape: `\\\\` for `\\` in template literals |
| Using `\text{}` with special chars | Keep `\text{}` content simple; no HTML inside |
| Forgetting `\,` thin space before `dx` | Always write `\int f(x)\,dx` |
| Using `\bold` | Use `\mathbf{}` for bold math, `\textbf{}` for bold text |

**HTML escaping rule**: In raw HTML between tags, single backslashes work fine. In JS strings/template literals, double-escape backslashes.

---

## 4. KaTeX in Dynamic Content (Flashcards, Show/Hide)

When content is hidden (flashcard backs, "Show Answer" sections), KaTeX auto-render processes them at load time as long as they're in the DOM — just hidden with CSS (`display:none`).

**Pattern for flashcard flip:**
```html
<div class="flashcard" onclick="this.classList.toggle('flipped')">
  <div class="card-front">
    <p>What is the derivative of \( e^{x^2} \)?</p>
  </div>
  <div class="card-back">
    <p>Using chain rule: \( \frac{d}{dx} e^{x^2} = 2x \cdot e^{x^2} \)</p>
  </div>
</div>
```

**Pattern for "Show Answer" toggle:**
```html
<div class="exercise">
  <p class="question">Evaluate \( \int_0^1 x^2\,dx \)</p>
  <button onclick="this.nextElementSibling.style.display='block'; this.style.display='none';">Show Answer</button>
  <div class="answer" style="display:none;">
    \[
    \begin{aligned}
      \int_0^1 x^2\,dx &= \left[\frac{x^3}{3}\right]_0^1 \\
      &= \frac{1}{3} - 0 = \frac{1}{3}
    \end{aligned}
    \]
  </div>
</div>
```

**If you dynamically inject LaTeX via JavaScript**, re-render after injection:

```javascript
function rerenderMath(element) {
  renderMathInElement(element, {
    delimiters: [
      { left: "$$", right: "$$", display: true },
      { left: "\\[", right: "\\]", display: true },
      { left: "\\(", right: "\\)", display: false },
      { left: "$", right: "$", display: false }
    ],
    throwOnError: false
  });
}

// After injecting new content:
const container = document.getElementById('flashcard-container');
container.innerHTML = newCardHTML;
rerenderMath(container);
```

---

## 5. Interactive Knowledge Graph (D3 Force-Directed)

Use D3.js v7 from CDN. This gives draggable nodes, zoomable canvas, and labeled edges.

### CDN

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/7.9.0/d3.min.js"></script>
```

### Data Structure

```javascript
const graphData = {
  nodes: [
    { id: "concept1", label: "Gradient Descent", group: "optimization", importance: 3,
      definition: "An iterative algorithm that moves toward a function's minimum by following the negative gradient." },
    { id: "concept2", label: "Learning Rate", group: "optimization", importance: 2,
      definition: "Step size hyperparameter controlling how far gradient descent moves each iteration." },
    { id: "concept3", label: "Loss Function", group: "fundamentals", importance: 3,
      definition: "Measures how far the model's predictions are from the true values." },
  ],
  links: [
    { source: "concept1", target: "concept3", relation: "requires", label: "minimizes" },
    { source: "concept2", target: "concept1", relation: "extends", label: "controls step size" },
  ]
};
```

- `group`: color clustering
- `importance`: 1-3, controls node radius
- `relation`: controls line style — "requires"=dashed, "extends"=solid, "contrasts"=red dotted, "example"=dash-dot, "applies"=green solid

### Rendering Pattern

```javascript
function renderKnowledgeGraph(containerId, data) {
  const container = document.getElementById(containerId);
  const width = container.clientWidth || 800;
  const height = 500;

  const svg = d3.select(`#${containerId}`)
    .append("svg")
    .attr("viewBox", `0 0 ${width} ${height}`)
    .attr("width", "100%")
    .attr("height", height);

  const g = svg.append("g");
  svg.call(d3.zoom().scaleExtent([0.3, 3]).on("zoom", (event) => {
    g.attr("transform", event.transform);
  }));

  const groups = [...new Set(data.nodes.map(n => n.group))];
  const color = d3.scaleOrdinal(d3.schemeTableau10).domain(groups);

  svg.append("defs").selectAll("marker")
    .data(["arrow"]).enter().append("marker")
    .attr("id", d => d)
    .attr("viewBox", "0 -5 10 10")
    .attr("refX", 20).attr("refY", 0)
    .attr("markerWidth", 6).attr("markerHeight", 6)
    .attr("orient", "auto")
    .append("path").attr("d", "M0,-5L10,0L0,5").attr("fill", "#999");

  function linkStyle(rel) {
    switch (rel) {
      case "requires":  return "6,4";
      case "contrasts": return "2,2";
      case "example":   return "4,2,1,2";
      default:          return "none";
    }
  }
  function linkColor(rel) {
    switch (rel) {
      case "contrasts": return "#e74c3c";
      case "applies":   return "#27ae60";
      default:          return "#888";
    }
  }

  const simulation = d3.forceSimulation(data.nodes)
    .force("link", d3.forceLink(data.links).id(d => d.id).distance(120))
    .force("charge", d3.forceManyBody().strength(-300))
    .force("center", d3.forceCenter(width / 2, height / 2))
    .force("collision", d3.forceCollide().radius(d => 20 + d.importance * 8));

  const link = g.append("g").selectAll("line")
    .data(data.links).enter().append("line")
    .attr("stroke", d => linkColor(d.relation))
    .attr("stroke-width", 1.5)
    .attr("stroke-dasharray", d => linkStyle(d.relation))
    .attr("marker-end", "url(#arrow)");

  const linkLabel = g.append("g").selectAll("text")
    .data(data.links).enter().append("text")
    .text(d => d.label)
    .attr("font-size", "10px")
    .attr("fill", "#666")
    .attr("text-anchor", "middle");

  const node = g.append("g").selectAll("g")
    .data(data.nodes).enter().append("g")
    .call(d3.drag()
      .on("start", (event, d) => { if (!event.active) simulation.alphaTarget(0.3).restart(); d.fx = d.x; d.fy = d.y; })
      .on("drag", (event, d) => { d.fx = event.x; d.fy = event.y; })
      .on("end", (event, d) => { if (!event.active) simulation.alphaTarget(0); d.fx = null; d.fy = null; })
    );

  node.append("circle")
    .attr("r", d => 10 + d.importance * 5)
    .attr("fill", d => color(d.group))
    .attr("stroke", "#fff").attr("stroke-width", 2)
    .style("cursor", "grab");

  node.append("text")
    .text(d => d.label)
    .attr("dx", d => 14 + d.importance * 5)
    .attr("dy", 4)
    .attr("font-size", "12px")
    .attr("fill", "currentColor");

  // Tooltip
  const tooltip = d3.select(`#${containerId}`)
    .append("div")
    .style("position", "absolute")
    .style("background", "var(--bg-secondary, #f9f9f9)")
    .style("border", "1px solid var(--border, #ddd)")
    .style("border-radius", "8px")
    .style("padding", "12px 16px")
    .style("max-width", "260px")
    .style("font-size", "13px")
    .style("box-shadow", "0 4px 12px rgba(0,0,0,0.15)")
    .style("pointer-events", "none")
    .style("opacity", 0)
    .style("transition", "opacity 0.2s");

  node.on("mouseover", (event, d) => {
    tooltip.html(`<strong>${d.label}</strong><br>${d.definition}`)
      .style("left", (event.offsetX + 15) + "px")
      .style("top", (event.offsetY - 10) + "px")
      .style("opacity", 1);
  }).on("mouseout", () => {
    tooltip.style("opacity", 0);
  });

  simulation.on("tick", () => {
    link.attr("x1", d => d.source.x).attr("y1", d => d.source.y)
        .attr("x2", d => d.target.x).attr("y2", d => d.target.y);
    linkLabel.attr("x", d => (d.source.x + d.target.x) / 2)
             .attr("y", d => (d.source.y + d.target.y) / 2);
    node.attr("transform", d => `translate(${d.x},${d.y})`);
  });
}
```

### Container HTML

```html
<div id="knowledge-graph" style="position:relative; width:100%; border:1px solid var(--border,#ddd); border-radius:8px; overflow:hidden;"></div>
<script>renderKnowledgeGraph("knowledge-graph", graphData);</script>
```

### Graph Legend

```html
<div class="graph-legend" style="display:flex; gap:20px; flex-wrap:wrap; padding:12px; font-size:13px;">
  <span>── solid = extends</span>
  <span>╌╌ dashed = requires</span>
  <span style="color:#e74c3c;">∙∙ dotted red = contrasts</span>
  <span style="color:#27ae60;">── green = applies to</span>
  <span>╌∙╌ dash-dot = example of</span>
</div>
```

---

## 6. Charting with Chart.js (Optional)

For statistics, economics, or science courses needing bar/line/pie charts:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.7/chart.umd.min.js"></script>
```

Use when a rendered chart is clearer than a table.

---

## Quick Checklist Before Finishing

- [ ] KaTeX CSS in `<head>`
- [ ] KaTeX JS + auto-render JS loaded (katex.min.js before auto-render.min.js)
- [ ] `renderMathInElement(document.body, {...})` called at end of body
- [ ] All math uses `\( \)` or `\[ \]` delimiters
- [ ] No raw `<` or `>` inside math (use `\lt` `\gt`)
- [ ] D3 loaded from CDN before knowledge graph script
- [ ] Knowledge graph container has `position:relative`
- [ ] Hidden content (flashcard backs, answers) is in the DOM at load time
