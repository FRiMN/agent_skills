---
name: ddgs
description: Web search and content extraction via Dux Distributed Global Search. Use for searching documentation, facts, or any web content. Lightweight, no browser required.
---

# DDGS

Web metasearch and content extraction using the [Dux Distributed Global Search](https://github.com/deedy5/ddgs/tree/main). No browser required.

## Setup

Need only installed [uv](https://docs.astral.sh/uv/). DDGS using through uvx - executes and installs command-line tools provided by Python packages in an ephemeral environment.

## Search

```bash
# Basic search (10 results, output to csv file)
uvx ddgs text --max_results=10 -q "query" -o /tmp/query.json 2>&1 && cat /tmp/query.json
# News search (10 results, output to csv file)
uvx ddgs news --max_results=10 --output=csv -q "query" -o /tmp/query.json 2>&1 && cat /tmp/query.json
```

## Options

```bash
uvx ddgs --help
Usage: ddgs [OPTIONS] COMMAND1 [ARGS]... [COMMAND2 [ARGS]...]...

  DDGS CLI tool.

Options:
  --help  Show this message and exit.

Commands:
  books    CLI function to perform a DDGS books metasearch.
  images   CLI function to perform a DDGS images metasearch.
  news     CLI function to perform a DDGS news metasearch.
  text     CLI function to perform a DDGS text metasearch.
  version  Print and return version.
  videos   CLI function to perform a DDGS videos metasearch.
```

```bash
uvx ddgs text --help
Usage: ddgs text [OPTIONS]

  CLI function to perform a DDGS text metasearch.

Options:
  -q, --query TEXT                text search query
  -k, --keywords TEXT             (Deprecated) text search query
  -r, --region TEXT               us-en, ru-ru, etc.
  -s, --safesearch [on|moderate|off]
  -t, --timelimit [d|w|m|y]       day, week, month, year
  -m, --max_results INTEGER       maximum number of results
  -p, --page INTEGER              page number of results
  -b, --backend [auto|all|bing|brave|duckduckgo|google|grokipedia|mojeek|yandex|yahoo|wikipedia]
  -o, --output TEXT               csv, json or filename.csv|json (save the
                                  results to a csv or json file)
  -d, --download                  download results. -dd to set custom
                                  directory
  -dd, --download-directory TEXT  Specify custom download directory
  -th, --threads INTEGER          download threads, default=10
  -pr, --proxy TEXT               the proxy to send requests, example:
                                  socks5h://127.0.0.1:9150
  -v, --verify BOOLEAN            verify SSL when making the request
  -nc, --no-color                 disable color output
  --help                          Show this message and exit.
```

ALWAYS USE `--output` option! ddgs cli uses interactive output without this option.
ALWAYS STORE output files in `/tmp` dir as temporary file.

## Output format

Body is truncated in output. It is snippet, not whole content.

### CSV

```csv
title,href,body
LLM,https://en.wikipedia.org/wiki/LLM,"A large language model (LLM) is a language model ..."
Large language model - Wikipedia,https://en.wikipedia.org/wiki/Large_language_model,"A large language model ( LLM ) is a language model  ..."
```

### JSON

```json
[
  {
    "title": "LLM",
    "href": "https://en.wikipedia.org/wiki/LLM",
    "body": "A large language model (LLM) is a language model ..."
  },
  {
    "title": "LLM : Language Is All We Need. Attention is all you need. | Medium",
    "href": "https://medium.com/@prasannasethuraman/llm-language-is-all-we-need-3dd2f2914e4c",
    "body": "If we run this LLM locally on a i7 CPU ..."
  }
]
```

## When to use

- Searching for documentation or API references
- Looking up facts or current information
- Any task requiring web search without interactive browsing
