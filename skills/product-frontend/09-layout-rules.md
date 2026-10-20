# Reference — The box layout rules

A small set of styling rules that keeps layouts predictable, components reusable and AI-written CSS from drifting. They are this skill's recommended standard.

**Offer them, don't impose them.** In Phase 1, tell the person about these rules, recommend them for what they're building, and let them accept, adapt or decline. Recommend them for almost every product UI (dashboards, tools, apps, forms, marketing pages). Say they fit less well for motion-heavy or graphics-heavy work (scroll-driven animation, canvas, games, illustration), where elements are positioned by animation rather than flow. If the project already has its own deliberate rules, follow those and only point out conflicts.

How to pitch it, in one line: "Every element is a box; parents space their children with `gap`; nothing pushes itself around with margins. Components then drop into any layout without fixes, and spacing lives in one place."

## 1. Every element is a box

- The parent is a box, and its children are smaller boxes arranged inside it with **flexbox or grid**. All layout and spacing comes from that.
- Break the UI into reusable components (buttons, cards, headers, rows). A component never decides its own outer spacing; whoever places it does.

## 2. Spacing between elements: `gap`, never margins

```jsx
// Wrong
<div className="mt-2 mb-4 ml-6">Content</div>

// Right: the parent spaces its children
<div className="flex flex-col gap-4">
  <div>Content 1</div>
  <div>Content 2</div>
</div>

<div className="flex gap-4">            {/* horizontal */}
  <Button>Save</Button>
  <Button variant="ghost">Cancel</Button>
</div>

<div className="grid grid-cols-3 gap-8"> {/* grid */}
  <Card /> <Card /> <Card />
</div>
```

- No `m-*`, `mx-auto`, `space-x-*` or `space-y-*`.
- Vary the rhythm on purpose: tight inside a group (`gap-1.5`/`gap-2`), wider between groups (`gap-6`), widest between sections (`gap-10`).
- Need extra space before one child? Wrap the group in its own box with its own gap, rather than giving the child a margin.

## 3. Padding: internal and symmetric

Padding only keeps content away from its container's walls.

```jsx
<div className="p-6">Equal distance from every wall</div>
<div className="px-8 py-4">Horizontal and vertical pairs</div>

// Avoid: one-sided padding
<div className="pr-4">…</div>
```

One-sided padding only when the design truly needs it (optical alignment, an icon inset), with a comment saying why.

## 4. Floating and overlapping: `absolute` only inside `relative`

```jsx
// Badge on a card
<div className="relative rounded-lg border border-border p-6">
  <span className="absolute top-2 right-2 rounded bg-danger-subtle px-2 py-1 text-danger">New</span>
  <h3>Card title</h3>
</div>

// Dropdown: the trigger's wrapper is the box; offset with a token, not a margin
<div className="relative">
  <Button>Menu</Button>
  <div className="absolute top-full left-0 translate-y-2 bg-surface-raised shadow-overlay">…</div>
</div>

// Wrong: absolute with no relative parent escapes the box
<div><div className="absolute top-0">…</div></div>
```

Better still, use the design system's popover/menu primitive, which handles positioning and collisions.

## 5. Common layouts

```jsx
// Centre both ways
<div className="flex min-h-screen items-center justify-center">…</div>

// Header: logo and nav pushed apart
<header className="flex items-center justify-between px-8 py-4">
  <Logo />
  <nav className="flex gap-6">…</nav>
</header>

// Page width without mx-auto: symmetric padding computed from the max width
// .px-page { padding-inline: max(var(--gutter), (100% - var(--page-max)) / 2); }
<main className="flex flex-col gap-10 px-page py-8">…</main>

// Full page
<div className="flex min-h-screen flex-col">
  <header className="flex items-center justify-between px-8 py-6">…</header>
  <main className="flex flex-1 flex-col gap-8 p-8">
    <div className="grid grid-cols-2 gap-8">
      <div className="relative flex flex-col gap-6 rounded-lg border border-border p-6">
        <span className="absolute top-4 right-4 …">Featured</span>
        <div className="flex flex-col gap-2"><h2>Title</h2><p>Body</p></div>
        <div className="flex gap-4"><Button>One</Button><Button>Two</Button></div>
      </div>
    </div>
  </main>
  <footer className="px-8 py-6">…</footer>
</div>
```

Notice the card's buttons get space from the card's `gap-6`, not from a `mt-6`.

## 6. Utilities first, CSS variables always

- Use the utility system (e.g. Tailwind) mapped to **design tokens**: `bg-surface`, `text-fg-muted`, `border-border`, `bg-accent`, not `bg-white`, `text-gray-500` or `bg-blue-500`. Switch the framework's default palette off so the raw classes don't exist.
- No raw colours (hex, rgb, oklch) and no arbitrary values (`text-[13px]`, `p-[7px]`) in components.
- When the utility system can't express it, use an inline style that reads a variable:

```jsx
<div style={{ background: "var(--gradient-hero)", boxShadow: "var(--shadow-elevated)" }}>…</div>
```

```css
/* tokens file — the only place raw values live */
:root {
  --gradient-hero: linear-gradient(135deg, var(--brand-500), var(--brand-700));
  --shadow-elevated: 0 20px 25px -5px oklch(0 0 0 / 0.1);
}
```

- New need → new token, named for its job, with its purpose written beside it.

## 7. Enforce it

Rules nobody checks drift within a week, and AI completions default to margins and raw colours. If the person accepts the rules, add lint errors for margins/`space-*`, arbitrary values and raw colours (an ESLint rule on class strings, or stylelint for CSS), and a grep check in handoffs. A deliberate exception gets a disable comment with the reason.

## Quick reference

| Don't | Do |
|---|---|
| `mt-4 mb-6 ml-2` | parent `flex flex-col gap-6` |
| `pr-4` alone | `p-4` / `px-4 py-2` |
| `absolute` with no positioned parent | `relative` parent, `absolute` child |
| `mx-auto max-w-6xl` | `px-page` |
| `bg-blue-500`, `#667eea`, `text-[13px]` | `bg-accent`, a token, a type-role utility |
