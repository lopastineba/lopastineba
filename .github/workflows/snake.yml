name: Snake generator

on:
  schedule:
    - cron: "0 6 * * *"   # ежедневно 06:00 UTC
  workflow_dispatch:
  push:
    branches: [ "main" ]

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Generate snake (SVG + GIF)
        uses: Platane/snk@v3
        with:
          # GitHub user to read the contribution graph from
          github_user_name: ${{ github.repository_owner }}

          # List of files to generate (one per line). Options via query string.
          # - palette: [github, github-dark, github-light]
          # - color_snake: snake color
          # - color_dots: 5 comma-separated colors from 0 to max contributions
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/github-snake.gif?color_snake=orange&color_dots=#ebedf0,#c6e48b,#7bc96f,#239a3b,#196127

      - name: Publish to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
