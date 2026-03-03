# Profile Maintenance Guide

Instructions for AI agents maintaining this GitHub profile.

## Design Philosophy

**Data-rich but intentional.** The profile showcases real GitHub activity through stats cards while maintaining a professional, non-generic appearance. It should look like a developer's dashboard, not a template.

## Structure

```
1. Header (# GitHub Stats)
2. Name + Title + 2-line tagline
3. Activity section (stats + streak cards side-by-side)
4. Contributions graph
5. Languages breakdown
6. Current Work table
7. Stack (code block format)
8. Links (simple text, centered)
```

## Stats Cards Configuration

All cards use consistent theming:
- Theme: `dark` or `github-dark`
- Background: `0d1117`
- Accent color: `58a6ff` (GitHub blue)
- Hide borders: `true`
- Include private contributions: `true`

### Cards Used
- `github-readme-stats` - Main stats + languages
- `github-readme-streak-stats` - Commit streaks
- `github-readme-activity-graph` - Contribution timeline

## Content Guidelines

### Tagline
Keep it to 2 lines maximum. Focus on what you do, not aspirational statements.
- Good: "I connect AI tools with real business problems"
- Bad: "Passionate about leveraging cutting-edge AI solutions"

### Current Work
Only list 2-3 active projects. Use a table format with brief descriptions.

### Stack
Use code block format for clean monospace display. Group by category.

## What NOT to Do

- No visitor counters or "profile views" badges
- No "Connect with me" badge walls
- No inspirational quotes
- No emoji overload (1-2 per section header is fine)
- No generic "I love coding" statements
- No technology badge walls

## When to Update

- New significant project → Add to Current Work table
- Stack changes → Update Stack section
- Role/title changes → Update header

## Testing

After changes, verify:
1. Stats cards render (may take 1-2 min to cache)
2. Activity graph shows data
3. All links work
4. Layout doesn't break on mobile
