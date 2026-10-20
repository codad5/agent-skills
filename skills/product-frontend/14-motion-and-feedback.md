# Reference — Motion and feedback

Goal: the UI answers every action at once, keeps people oriented while the network catches up, and feels alive without being busy. This is product motion, not showpiece animation: every movement explains something (where a thing came from, what changed, that the click registered) or it's cut.

Use it when designing components (Phase 4), in the per-screen loop (every state), and in the craft pass.

## 1. Answer every action, whatever the network is doing

People judge speed by how fast something responds, not by how fast the server is. Match the feedback to how long the wait is:

| Wait | What the person should see |
|---|---|
| **Under ~100ms** | The result, or an instant pressed state. Nothing else needed. |
| **~100ms to 1s** | Immediate acknowledgement: the button shows it's working (spinner inside it, label changes to "Saving…"), the row dims, the toggle flips. |
| **1 to ~10s** | Progress in place: a skeleton for content, a progress bar for known lengths, a short status line ("Generating the report…"). |
| **Over ~10s** | Make it a background job: let them leave, show progress somewhere persistent, notify when done. |

Rules that make this work:
- **Every interactive element has hover, pressed, focus, disabled and busy states.** The pressed state shows on pointer down, before any network.
- **Never block the whole page for one action.** The spinner lives in the button or the row that triggered it.
- **Stop double submits:** disable the control while it's busy, and keep its width steady so the layout doesn't jump.
- **Delay loaders slightly** (~300ms) so fast responses don't flash a skeleton, and once one shows, keep it at least ~300ms so it doesn't flicker.
- **Keep what's on screen while refetching.** Show the previous data, dimmed or with a small "Updating…" note, instead of swapping back to a skeleton on every filter change.

## 2. Optimistic updates: show the result before the server confirms

For actions that almost always succeed (toggle, rename, like, reorder, mark as read, archive):
1. Update the UI immediately.
2. Send the request.
3. On failure, roll back and say so in place, with a retry ("Couldn't archive. Try again").

Pair destructive optimistic actions with **undo** instead of a confirm dialog ("Archived · Undo" for ~5 seconds). Keep confirm dialogs for wide-impact or irreversible actions (deleting an account, a switch that affects every user).

Don't be optimistic about money, permissions or anything where a wrong "done" misleads: show the pending state and wait.

Stack hints: React `useOptimistic`, `useTransition` and `useFormStatus` with server actions; TanStack Query's `onMutate` with rollback; SWR's `optimisticData`.

## 3. Loading that looks like the content

- **Skeletons match the real layout** (same rows, columns, heights), so nothing shifts when data arrives. Each independent section loads on its own; a slow chart never blocks a table.
- **Spinners only inside small things** (a button, an inline cell), never alone on an empty page.
- **Stream long answers** (AI replies, reports) as they arrive, with a stop control.
- **Images reserve their space** (width and height or aspect ratio) and fade in, never pop and push text.
- **Prefetch likely next steps** (on hover or when a link scrolls into view) so navigation feels instant.

## 4. When the network is slow or gone

- **Slow:** after a few seconds with no answer, say so ("Still working, your connection seems slow") instead of a spinner that never changes.
- **Offline:** a clear but calm banner; keep showing what's already loaded; disable or queue actions that need the network, and say which.
- **Failed:** say what happened and what to do, with a retry right there. Keep what the person typed; never clear a form on error.
- **Reconnected:** refresh quietly and say so briefly if anything changed.

## 5. Motion that explains

Use motion for:
- **Orientation:** a panel slides from the edge it's anchored to; a dialog scales in slightly from where it was opened; a new page keeps shared elements in place (the View Transitions API helps).
- **Feedback:** a toggle slides, a checkbox ticks, "Copy" becomes "Copied ✓" for a moment.
- **Change:** a new or updated row highlights briefly; a changed number ticks over or flashes its colour once.
- **Liveness, only for live data:** a small pulsing dot means "this updates in real time". Never pulse static things.

How it moves:
- **Durations are tokens:** ~100–150ms for hover and press, ~200ms for menus and panels, ~250–300ms for large surfaces entering. Exits faster than entrances.
- **Easing:** ease-out for entering (fast start, gentle stop), ease-in for leaving. No bounce in work tools.
- **Animate `transform` and `opacity` only**; animating width, height or position causes jank and layout shift.
- **Respect reduced motion:** with `prefers-reduced-motion`, replace movement with a fade or nothing.
- **Content that animates in must be visible without JavaScript.** If the script fails, the content shows; it doesn't stay invisible waiting for a reveal.
- **One motion library at most**, behind the design system's wrapper, or plain CSS transitions; often CSS is enough.

## 6. Making it feel alive without making it busy

- Hover states on everything clickable (a tone change, not a jump).
- Empty states that teach, with the action right there.
- Small, specific confirmations in place ("Saved 2s ago") instead of a toast for everything.
- Toasts only for results that happen elsewhere or later (export ready, background job failed).
- A signature moment or two (a satisfying completion, a gentle count-up on a headline number on first load), not motion on every element.

## Check it

- Throttle the network in browser dev tools (slow 3G, offline) and run the main flows: every action acknowledges within ~100ms, nothing blocks the page, failures keep input and offer retry.
- Turn on reduced motion and check nothing important depends on movement.
- Watch for layout shift as data arrives.

## What NOT to do

- Don't put a full-page spinner in front of one action.
- Don't animate for decoration (bouncing icons, looping shimmer on loaded content, parallax in an app).
- Don't swap the whole screen back to skeletons on every refetch.
- Don't be optimistic about payments, permissions or irreversible actions.
- Don't let a failed request silently undo what the person did, or clear what they typed.
