---
name: curl
description: Web content extraction via curl. Use for extract documentation, facts, or any web content. Lightweight, no browser required.
---

# Curl

Web content extraction using the curl. No browser required.

## Extract content

Span and div tags are dropped from the HTML https://pandoc.org/MANUAL.html#raw-htmltex and sed removes any inline SVG images in image tags from the Markdown content.

```bash
curl -fsSL "URL" | \
    pandoc -f html-native_divs-native_spans -t gfm-raw_html --wrap=none | \
    sed -E 's/!\[[^]]*\]\([^)]*\)//g'
```

## When to use

- Fetching content from specific URLs
- Looking up facts or current information
- Any task requiring get web page content without interactive browsing
