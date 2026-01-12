```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║   ██╗   ██╗██╗    ██████╗ ███████╗██╗   ██╗██╗███████╗██╗    ██╗             ║
║   ██║   ██║██║    ██╔══██╗██╔════╝██║   ██║██║██╔════╝██║    ██║             ║
║   ██║   ██║██║    ██████╔╝█████╗  ██║   ██║██║█████╗  ██║ █╗ ██║             ║
║   ██║   ██║██║    ██╔══██╗██╔══╝  ╚██╗ ██╔╝██║██╔══╝  ██║███╗██║             ║
║   ╚██████╔╝██║    ██║  ██║███████╗ ╚████╔╝ ██║███████╗╚███╔███╔╝             ║
║    ╚═════╝ ╚═╝    ╚═╝  ╚═╝╚══════╝  ╚═══╝  ╚═╝╚══════╝ ╚══╝╚══╝              ║
║                                                                              ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  AUTOMATED UI/UX CODE REVIEW USING VERCEL WEB INTERFACE GUIDELINES           ║
║  ──────────────────────────────────────────────────────────────────          ║
║  STATUS: OPERATIONAL │ VERSION: 1.0 │ LICENSE: MIT                           ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## SYSTEM OVERVIEW

```
┌────────────────────────────────────────────────────────────────────────────┐
│                                                                            │
│  A GitHub Action that automatically reviews frontend code against          │
│  Vercel's Web Interface Guidelines using Claude AI. Non-blocking.          │
│  Advisory. Always current with upstream guidelines.                        │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## OPERATIONAL CHARACTERISTICS

```
┌────────────────────────────────────────────────────────────────────────────┐
│  CAPABILITY                 DESCRIPTION                                    │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  LIVE GUIDELINES            Fetches latest guidelines at runtime from      │
│                             vercel-labs/web-interface-guidelines           │
│                             Never outdated. Always synchronized.           │
│                                                                            │
│  AI-POWERED REVIEW          Uses Claude to intelligently analyze code      │
│                             against 9 UI/UX categories                     │
│                                                                            │
│  NON-BLOCKING               Advisory only. Will not fail builds.           │
│                             Posts feedback as PR comments.                 │
│                                                                            │
│  SELECTIVE TRIGGER          Only executes on frontend file changes         │
│                             (.tsx, .ts, .css in configured paths)          │
│                                                                            │
│  DETAILED REPORTING         Categorized feedback with file:line refs       │
│                             MUST fix vs SHOULD improve priorities          │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## DEPLOYMENT INSTRUCTIONS

```
┌────────────────────────────────────────────────────────────────────────────┐
│  STEP 1: ADD WORKFLOW                                                      │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Copy .github/workflows/ui-guidelines-review.yml to your repository.       │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────┐
│  STEP 2: CONFIGURE API KEY                                                 │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Add ANTHROPIC_API_KEY to repository secrets:                              │
│                                                                            │
│  Settings > Secrets and variables > Actions > New repository secret        │
│                                                                            │
│  Name:   ANTHROPIC_API_KEY                                                 │
│  Value:  [Your Anthropic API key]                                          │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────┐
│  STEP 3: EXECUTE                                                           │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Open a pull request modifying frontend files.                             │
│  Review runs automatically. Results posted as PR comments.                 │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## REVIEW CATEGORIES

```
┌────────────────────────────────────────────────────────────────────────────┐
│  CATEGORY                   SCOPE                                          │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  ACCESSIBILITY              ARIA labels, keyboard support, focus           │
│                             management, semantic HTML                      │
│                                                                            │
│  FORMS                      Input types, autocomplete, validation,         │
│                             error handling                                 │
│                                                                            │
│  ANIMATION                  prefers-reduced-motion, compositor-friendly    │
│                             properties                                     │
│                                                                            │
│  PERFORMANCE                Virtualization, image optimization,            │
│                             CLS prevention                                 │
│                                                                            │
│  NAVIGATION                 URL state sync, proper link elements           │
│                                                                            │
│  TOUCH                      Hit targets (44x44px), touch-action,           │
│                             overscroll behavior                            │
│                                                                            │
│  TYPOGRAPHY                 Proper quotes, ellipsis, non-breaking spaces   │
│                                                                            │
│  DARK MODE                  color-scheme, theme-color meta                 │
│                                                                            │
│  HYDRATION                  Controlled vs uncontrolled inputs              │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## ANTI-PATTERN DETECTION

```
┌────────────────────────────────────────────────────────────────────────────┐
│  PATTERN                              ISSUE                                │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  user-scalable=no                     Breaks accessibility                 │
│  maximum-scale=1                      Breaks accessibility                 │
│  onPaste with preventDefault          Blocks user input                    │
│  transition: all                      Performance degradation              │
│  outline-none without focus-visible   Breaks keyboard navigation           │
│  <div onClick> for navigation         Not accessible                       │
│  Images without dimensions            Causes CLS                           │
│  Form inputs without labels           Screen reader issue                  │
│  Icon buttons without aria-label      Not accessible                       │
│  Hardcoded date/number formats        Use Intl.* instead                   │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## OUTPUT FORMAT

```
┌────────────────────────────────────────────────────────────────────────────┐
│  EXAMPLE REVIEW OUTPUT                                                     │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  ## UI Guidelines Review                                                   │
│                                                                            │
│  ### Summary                                                               │
│  Found 3 issues across 2 files.                                            │
│  1 accessibility concern (MUST fix), 2 improvements (SHOULD).              │
│                                                                            │
│  ### Accessibility (MUST)                                                  │
│  - `components/Button.tsx:42` - Icon button missing `aria-label`           │
│    ```tsx                                                                  │
│    // Add aria-label for screen readers                                    │
│    <button aria-label="Close dialog">                                      │
│    ```                                                                     │
│                                                                            │
│  ### Animation (SHOULD)                                                    │
│  - `components/Modal.tsx:18` - Missing `prefers-reduced-motion` check      │
│                                                                            │
│  ### Passing                                                               │
│  - Form accessibility                                                      │
│  - Keyboard navigation                                                     │
│  - Image optimization                                                      │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## CONFIGURATION

```
┌────────────────────────────────────────────────────────────────────────────┐
│  CUSTOMIZE FILE PATTERNS                                                   │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Edit workflow to match project structure:                                 │
│                                                                            │
│  paths:                                                                    │
│    - "src/**"                                                              │
│    - "components/**"                                                       │
│    - "app/**"                                                              │
│    - "*.tsx"                                                               │
│    - "*.ts"                                                                │
│    - "*.css"                                                               │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘

┌────────────────────────────────────────────────────────────────────────────┐
│  ADJUST REVIEW DEPTH                                                       │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Modify claude_args to change review depth:                                │
│                                                                            │
│  claude_args: "--max-turns 30"                                             │
│                                                                            │
│  Higher values enable deeper analysis.                                     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## REFERENCES

```
┌────────────────────────────────────────────────────────────────────────────┐
│  RESOURCE                           URL                                    │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│  Web Interface Guidelines           https://vercel.com/design/guidelines   │
│  Guidelines Repository              https://github.com/vercel-labs/        │
│                                       web-interface-guidelines             │
│  AGENTS.md (Full Guidelines)        https://github.com/vercel-labs/        │
│                                       web-interface-guidelines/blob/       │
│                                       main/AGENTS.md                       │
│  command.md (Checklist)             https://github.com/vercel-labs/        │
│                                       web-interface-guidelines/blob/       │
│                                       main/command.md                      │
│  Claude Code Action                 https://github.com/anthropics/         │
│                                       claude-code-action                   │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## LICENSE

```
╔════════════════════════════════════════════════════════════════════════════╗
║                                                                            ║
║  MIT LICENSE                                                               ║
║  ───────────                                                               ║
║                                                                            ║
║  Permission is hereby granted, free of charge, to any person obtaining a   ║
║  copy of this software and associated documentation files, to deal in the  ║
║  Software without restriction, including without limitation the rights to  ║
║  use, copy, modify, merge, publish, distribute, sublicense, and/or sell    ║
║  copies of the Software.                                                   ║
║                                                                            ║
╚════════════════════════════════════════════════════════════════════════════╝
```

---

```
┌────────────────────────────────────────────────────────────────────────────┐
│                                                                            │
│                          [END OF TRANSMISSION]                             │
│                                                                            │
│                               ◇  ◇  ◇                                      │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```
