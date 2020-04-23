# Reason Compiler Benchmark Tool

This repository offers a simple setup for benchmarking your Reason project
compilation metrics.

## How it works

It's very simple for now:

The script `benchmark-test.js` will automatically pick up your bsconfig.sources
configuration to find all Reason file occurrences and puts it in relation to
the bucklescript build times by running a clean build.

It will not measure complete builds (no -clean-world | -make-world) to keep
dependencies out of the equation.

## Usage

`node benchmark-test.js > result.json`

The script outputs pure json on `stdout`, and some human readable information
on `stderr`. Example output:

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

It's a standalone NodeJS script, it only needs a typical Reason project with a
`bsconfig.json` in its project root and `cloc` as a dev dependency:

```
# Install line counting tool
npm install cloc --save-dev

# Create some subdir if wanted
mkdir scripts

# Curl the test script into the scripts folder
curl -o scripts/benchmark-test.js https://raw.githubusercontent.com/ryyppy/re-compiler-benchmark-tool/master/benchmark-test.js

# Make sure to make world before running the tool, otherwise it will fail
npx bsb -make-world

# To run it
node scripts/benchmark-test.js
```

## Why not a package.json?

It's a simple script
