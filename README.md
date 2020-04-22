# Reason Compiler Benchmark Tool

This repository offers a simple setup for benchmarking your Reason project
compilation metrics.

It's very simple for now:

The script `benchmark-test.js` will automatically pick up your bsconfig.sources
configuration to find all Reason file occurrences and puts it in relation to
the bucklescript build times by running a clean build.

It will not measure complete builds (no -clean-world | -make-world) to keep
dependencies out of the equation.

The script outputs pure json on `stdout`, and some human readable information
on `stderr`:

```
node scripts/benchmark-test.js
Capturing LOC / file numbers...
Cleaning the project first...
Measuring build performance...
{
  "fileMetrics": {
    "numberOfFiles": 37,
    "blankLines": 483,
    "commentLines": 177,
    "codeLines": 4510,
    "totalLines": 5170
  },
  "buildTime": {
    "real": 3.12,
    "user": 4.18,
    "sys": 1.77
  },
  "results": {
    "locPerSec": 1237
  }
}
```

## Installation

It's a standalone NodeJS script, it only needs a project with a common Reason
project with a `bsconfig.json` in the project root and `cloc` as a dev
dependency.

```
# Install line counting tool
npm install cloc --save-dev

# Create some subdir if wanted
mkdir scripts
```

**Add a npm script for easy access & automation:**

```js
//package.json
{
  "scripts": {
    "re:bench": "node scripts/benchmark-test.js"
  }
}
```
