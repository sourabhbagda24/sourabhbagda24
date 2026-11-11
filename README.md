name: Generate Snake & Pac-Man Animations

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Generate Snake and Pac-Man
        uses: Platane/snk@v3
        with:
          github_user_name: sourabhbagda24
          outputs: |
            dist/github-snake.svg?color_snake=#8b5cf6&color_dots=#ebedf0,#a7f3d0,#34d399,#10b981,#00f5a0
            dist/github-snake-dark.svg?palette=github-dark&color_snake=#00f5a0&color_dots=#161b22,#0e4429,#1e7e5e,#22d3ee,#00f5a0
            dist/pacman.svg?color_snake=#ffd60a&color_dots=#ebedf0,#c4b5fd,#a78bfa,#8b5cf6,#00f5a0
            dist/pacman-dark.svg?palette=github-dark&color_snake=#ffd60a&color_dots=#161b22,#2e1065,#6d28d9,#8b5cf6,#00f5a0

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
