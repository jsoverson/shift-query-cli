# Shift query CLI

Command line tool to query AST nodes in JavaScript source files. Outputs JSON

## Install

```bash
$ npm install -g shift-query-cli
```

## Usage

Usage: shift-query [-j] file.js query-pattern

```bash
$ shift-query test.js IdentifierExpression
[ IdentifierExpression { type: 'IdentifierExpression', name: 'require' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'puppeteer' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'browser' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'page' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'page' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'page' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'page' } ]
```

If a script is piped to shift-query then the second argument is treated as the query pattern.


```bash
$ tail +2 shift-query | shift-query IdentifierExpression
[ IdentifierExpression { type: 'IdentifierExpression', name: 'require' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'require' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'require' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'console' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'code' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'file' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'pattern' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'printUsage' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'require' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'file' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'console' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'getStdin' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'fileContents' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'pattern' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'printUsage' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'parseScript' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'fileContents' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'console' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'e' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'process' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'query' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'ast' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'pattern' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'console' },
  IdentifierExpression { type: 'IdentifierExpression', name: 'result' } ]
```

## Outputting JSON

Output JSON with the `-j` flag.

```bash
$ shift-query -j test.js "[params.items.length=0]"
```

```bash
$ shift-query -j test.js LiteralStringExpression | jq .[].value
"puppeteer"
"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.131 Safari/537.36"
"en-US,en;q=0.9"
"1"
"https://www.google.com/"
"ss.png"
```

## Query syntax

Sytax is from shift-query which is, in turn, from esquery. It follows CSS syntax very closely and if you are familiar
writing CSS selectors you should pick this up quickly.

See [shift-query](https://github.com/jsoverson/shift-query)