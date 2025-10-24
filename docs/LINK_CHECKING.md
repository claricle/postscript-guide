# Link Checking

This project uses [Lychee](https://github.com/lycheeverse/lychee) to automatically check all links in the documentation for validity.

## Automatic Checks

Link checking runs automatically via GitHub Actions:

- **On every push to `main`**
- **On every pull request**
- **Weekly** (Sundays at midnight UTC) to catch external link rot
- **Manually** via workflow_dispatch

## What Gets Checked

### Built Site (Primary)
- All HTML files in `_site/` after Jekyll build
- Rendered internal navigation links
- Cross-references between pages
- External URLs in documentation
- Fragment identifiers (anchors)

### Source Files (Secondary)
- AsciiDoc files in `docs/**/*.adoc`
- xref cross-references
- External URLs in source
- Navigation structure integrity

## Running Locally

### Prerequisites

Install lychee:

```bash
# macOS
brew install lychee

# Linux (Cargo)
cargo install lychee

# Or download from releases
# https://github.com/lycheeverse/lychee/releases
```

### Check Built Site

```bash
# Build the Jekyll site first
bundle exec jekyll build

# Check all links in built site
lychee --config lychee.toml '_site/**/*.html'
```

### Check Source Files

```bash
# Check AsciiDoc source files
lychee --config lychee.toml 'docs/**/*.adoc'
```

### Quick Check

```bash
# Check both in one command
lychee --config lychee.toml '_site/**/*.html' 'docs/**/*.adoc'
```

## Configuration

### lychee.toml

Main configuration file controlling:
- File patterns to check
- Timeout and retry settings
- Accepted HTTP status codes
- Caching behavior
- URL remapping for local development

### .lycheeignore

Patterns to exclude from checking:
- Example URLs (example.com, test.com)
- Local development URLs (localhost)
- PostScript-specific pseudo-URLs (%stdin, %stdout)
- Temporarily unavailable but known-good URLs
- False positives

## Common Issues

### Internal xref Links

AsciiDoc `xref:` links are checked in two ways:

1. **Source files**: Validates `.adoc` file exists
2. **Built site**: Validates rendered HTML anchor exists

If you get errors about missing xrefs:
- Check the target file exists
- Verify the path is relative and correct
- Ensure front matter `title` matches xref target

### External URLs

If external URLs fail:
- Check if site is temporarily down
- Verify URL is correct
- Add to `.lycheeignore` if it's a false positive
- Consider if URL should be updated

### Navigation Hierarchy

The checker validates that parent/grand_parent references are valid:
- Parent page must exist
- Title must match exactly
- Category index files must have `has_children: true`

## Fixing Broken Links

### Internal Links

```adoc
# Wrong
xref:nonexistent.adoc[Link]

# Right
xref:existing-file.adoc[Link]
```

### Cross-Category Links

```adoc
# Same category
xref:other-command.adoc[`other`]

# Different category (go up then down)
xref:../other-category/command.adoc[`command`]

# From command to index
xref:index.adoc[Category Index]
```

### External Links

```adoc
# Use https where available
https://www.example.com/path

# Not http (unless required)
http://www.example.com/path
```

## CI Pipeline Integration

The link checker is integrated into CI:

- **Pull Requests**: Checks only changed files and their dependencies
- **Main Branch**: Full site check
- **Scheduled**: Weekly full check for link rot

### Failure Behavior

If links are broken:
- ❌ CI pipeline fails
- 📝 Results posted as PR comment
- 📊 Artifact uploaded with full report
- 🔍 Developers must fix before merge

### Success Criteria

All checks must pass:
- ✅ All internal links resolve
- ✅ All external URLs return 2xx/3xx status
- ✅ All fragments (anchors) exist
- ✅ Navigation hierarchy valid

## Maintenance

### Weekly Checks

Review weekly automated runs for:
- External link rot (sites going down)
- Moved content (redirects)
- Broken anchors

### After Major Changes

Run locally after:
- Reorganizing documentation structure
- Renaming files
- Updating navigation hierarchy
- Adding new categories

### Updating Exclusions

Add to `.lycheeignore`:
- Known problematic external sites
- Example/placeholder URLs
- Temporary development URLs
- False positives that can't be fixed

## Troubleshooting

### "Too Many Requests" (429)

External sites may rate-limit:
- Wait and retry
- Check less frequently
- Add to ignore if persistent

### "Connection Timeout"

Network issues:
- Retry the workflow
- Check if site is permanently down
- Increase timeout in `lychee.toml`

### "Fragment Not Found"

Anchor doesn't exist:
- Check target page has the anchor
- Verify Jekyll generated correct IDs
- Check for case sensitivity

### False Positives

Legitimate links failing:
- Add pattern to `.lycheeignore`
- Document why in ignore file
- Consider if link should be updated

## Best Practices

1. **Check locally before commit**: Run lychee on changed files
2. **Use relative paths**: For internal links
3. **Verify anchors**: When linking to specific sections
4. **Keep URLs current**: Regular maintenance of external links
5. **Document exclusions**: Comment why in `.lycheeignore`

## Resources

- [Lychee Documentation](https://lychee.cli.rs/)
- [GitHub Action](https://github.com/lycheeverse/lychee-action)
- [Configuration Reference](https://github.com/lycheeverse/lychee/blob/master/lychee.example.toml)