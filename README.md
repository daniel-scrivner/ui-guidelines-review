```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   ██╗   ██╗██╗    ██████╗ ██╗   ██╗██╗██████╗ ███████╗██╗     ██╗███╗   ██╗ │
│   ██║   ██║██║   ██╔════╝ ██║   ██║██║██╔══██╗██╔════╝██║     ██║████╗  ██║ │
│   ██║   ██║██║   ██║  ███╗██║   ██║██║██║  ██║█████╗  ██║     ██║██╔██╗ ██║ │
│   ██║   ██║██║   ██║   ██║██║   ██║██║██║  ██║██╔══╝  ██║     ██║██║╚██╗██║ │
│   ╚██████╔╝██║   ╚██████╔╝╚██████╔╝██║██████╔╝███████╗███████╗██║██║ ╚████║ │
│    ╚═════╝ ╚═╝    ╚═════╝  ╚═════╝ ╚═╝╚═════╝ ╚══════╝╚══════╝╚═╝╚═╝  ╚═══╝ │
│                                                                             │
│   ███████╗███████╗    ██████╗ ███████╗██╗   ██╗██╗███████╗██╗    ██╗        │
│   ██╔════╝██╔════╝    ██╔══██╗██╔════╝██║   ██║██║██╔════╝██║    ██║        │
│   █████╗  ███████╗    ██████╔╝█████╗  ██║   ██║██║█████╗  ██║ █╗ ██║        │
│   ██╔══╝  ╚════██║    ██╔══██╗██╔══╝  ╚██╗ ██╔╝██║██╔══╝  ██║███╗██║        │
│   ███████╗███████║    ██║  ██║███████╗ ╚████╔╝ ██║███████╗╚███╔███╔╝        │
│   ╚══════╝╚══════╝    ╚═╝  ╚═╝╚══════╝  ╚═══╝  ╚═╝╚══════╝ ╚══╝╚══╝         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

# UI Guidelines Review

A GitHub Action that automatically reviews your frontend code against [Vercel's Web Interface Guidelines](https://vercel.com/design/guidelines) using Claude AI.

---

## ✨ Features

```
┌────────────────────────────────────────────────────────────────────────────┐
│                                                                            │
│  🔄 LIVE GUIDELINES     Fetches latest guidelines at runtime - never      │
│                         outdated, always in sync with Vercel's repo       │
│                                                                            │
│  🤖 AI-POWERED          Uses Claude to intelligently review code          │
│                         against 9 UI/UX categories                        │
│                                                                            │
│  ✅ NON-BLOCKING        Advisory only - won't fail your builds            │
│                         Posts feedback as PR comments                     │
│                                                                            │
│  🎯 FOCUSED             Only triggers on frontend file changes            │
│                         (.tsx, .ts, .css in app/components/lib)           │
│                                                                            │
│  📝 DETAILED            Categorized feedback with file:line refs          │
│                         MUST fix vs SHOULD improve priorities             │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### 1. Add the Workflow

Copy `.github/workflows/ui-guidelines-review.yml` to your repository.

### 2. Add Your API Key

Add `ANTHROPIC_API_KEY` to your repository secrets:
- Go to **Settings** → **Secrets and variables** → **Actions**
- Click **New repository secret**
- Name: `ANTHROPIC_API_KEY`
- Value: Your Anthropic API key

### 3. Open a PR

The review runs automatically on PRs that modify frontend files.

---

## 📋 What It Reviews

The action checks your code against these categories from the [Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines):

| Category | What It Checks |
|----------|----------------|
| **Accessibility** | ARIA labels, keyboard support, focus management, semantic HTML |
| **Forms** | Input types, autocomplete, validation, error handling |
| **Animation** | `prefers-reduced-motion`, compositor-friendly properties |
| **Performance** | Virtualization, image optimization, CLS prevention |
| **Navigation** | URL state sync, proper link elements |
| **Touch** | Hit targets (44x44px), touch-action, overscroll behavior |
| **Typography** | Proper quotes, ellipsis, non-breaking spaces |
| **Dark Mode** | `color-scheme`, theme-color meta |
| **Hydration** | Controlled vs uncontrolled inputs |

---

## 🚫 Anti-Patterns Detected

```
┌────────────────────────────────────────────────────────────────────────────┐
│                                                                            │
│  ✗ user-scalable=no or maximum-scale=1     (breaks accessibility)         │
│  ✗ onPaste with preventDefault             (blocks user input)            │
│  ✗ transition: all                         (performance issue)            │
│  ✗ outline-none without focus-visible      (breaks keyboard nav)          │
│  ✗ <div onClick> for navigation            (not accessible)               │
│  ✗ Images without dimensions               (causes CLS)                   │
│  ✗ Form inputs without labels              (screen reader issue)          │
│  ✗ Icon buttons without aria-label         (not accessible)               │
│  ✗ Hardcoded date/number formats           (use Intl.* instead)           │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 📄 Example Output

```markdown
## 🎨 UI Guidelines Review

### Summary
Found 3 issues across 2 files. 1 accessibility concern (MUST fix), 2 improvements (SHOULD).

### Accessibility (MUST)
- `components/Button.tsx:42` - Icon button missing `aria-label`
  ```tsx
  // Add aria-label for screen readers
  <button aria-label="Close dialog">
  ```

### Animation (SHOULD)
- `components/Modal.tsx:18` - Missing `prefers-reduced-motion` check

### ✅ Passing
- Form accessibility
- Keyboard navigation
- Image optimization
```

---

## ⚙️ Configuration

### Customize File Patterns

Edit the workflow to match your project structure:

```yaml
paths:
  - "src/**"        # Your source directory
  - "components/**"
  - "app/**"
  - "*.tsx"
  - "*.ts"
  - "*.css"
```

### Adjust Review Depth

Modify `claude_args` to change the review depth:

```yaml
claude_args: "--max-turns 30"  # More turns = deeper analysis
```

---

## 🔗 References

- [Vercel Web Interface Guidelines](https://vercel.com/design/guidelines)
- [Guidelines GitHub Repository](https://github.com/vercel-labs/web-interface-guidelines)
- [AGENTS.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/AGENTS.md) - Full guidelines
- [command.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md) - Condensed checklist
- [Claude Code Action](https://github.com/anthropics/claude-code-action)

---

## 📜 License

MIT License - see [LICENSE](LICENSE) for details.

---

<p align="center">
  Built with ❤️ using <a href="https://github.com/anthropics/claude-code-action">Claude Code Action</a>
</p>
