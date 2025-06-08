# GitHub Actions Workflow

Below is an example of a workflow that uses octo-linter docker to check files in `.github`.

````yaml
---
name: GitHub Actions YAML linter

on:
  pull_request:
    paths:
      - '.github/**.yml'
      - '.github/**.yaml'

jobs:
  main:
    name: Lint
    runs-on: ubuntu-24.04
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run octo-linter
        run: |
          docker run --rm --name octo-linter \
            -v $(pwd)/.github:/dot-github -v $(pwd):/config \
            keenbytes/octo-linter:v1.2.3 \
            lint -p /dot-github -l WARN -c /config/config.yml
````
