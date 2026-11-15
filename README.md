Team AnC: Lab 2 Website

**Live site:** https://caleb-lab-lang.github.io/team-website/

## Team
| Name | Registration no. | GitHub username |
|------|------------------|-----------------|
| Caleb | COM/3433/26 | caleb-lab-lang |
| Agnes | COM/8148/26 | carol6740 |

## Who drove each part
- Part 0, 2, 4: Caleb Wagura
- Part 1, 3, 5: Agnes Mwende

## Personalisation
- **Our colours:** Primary Indigo (`#4f46e5` for light mode and `#818cf8` for dark mode), exceeding the 4.5:1 WebAIM text contrast requirement.
- **Projects we added:** "Team Git Repository" (`git`) and "Interactive Portfolio" (`js`).
- **Extension challenge(s) completed:**
  - **E1:** Added a fourth page (`faq.html`) using semantic `<details>` and `<summary>` disclosure elements and linked it across the navigation bar.
  - **E6:** Added real passport-style team photos (`images/caleb.jpg` and `images/agnes.jpg`) with explicit `width`, `height`, and empty `alt=""` attributes to prevent duplicate screen reader announcements.

## Reflection

1. Using a `<div>` instead of a `<button>` means losing native keyboard accessibility (focusability via `Tab` and activation via `Enter` or `Space`) as well as semantic role announcements. This would directly affect keyboard-only users and screen-reader users who rely on native HTML controls to navigate menus.

2. Without `defer`, the browser pauses HTML parsing as soon as it hits the `<script>` tag in `<head>`, downloads the file, and executes it immediately. Because the `<body>` has not been parsed yet, DOM queries like `document.querySelector('#project-list')` or `document.getElementById('year')` would return `null` and throw TypeErrors, breaking the page interactivity.

3. Using `innerHTML` causes the browser to parse strings as live HTML markup. If a visitor entered malicious `<script>` tags or event handlers (such as `<img src=x onerror=alert(1)>`), it would trigger a Cross-Site Scripting (XSS) attack. `textContent` escapes the input and renders it strictly as safe, plain text.

4. Client-side JavaScript validation improves user experience, but it runs entirely in the user's browser where it can be bypassed using DevTools, disabled, or skipped by sending direct HTTP POST requests (e.g., via `curl`). The server must always re-validate incoming data to protect database integrity and prevent malicious payloads.

5. `localStorage` is isolated by browser **origin**, which is defined by the combination of protocol, host/domain, and port. Double-clicking a file opens it under the `file://` origin, whereas Live Server serves it over `http://`. Because the protocol and host differ, the browser treats them as separate origins with separate storage buckets.

6. The `<header>` navigation bar and `<footer>` are duplicated across `index.html`, `projects.html`, `faq.html`, and `contact.html`. Duplicating markup makes maintenance error-prone because every navigation change (like adding the FAQ link) must be manually repeated in every file. This can be avoided by using a templating engine, server-side includes, or a component-based frontend framework (such as React or Vue).