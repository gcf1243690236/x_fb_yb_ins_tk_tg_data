name: Update README

on:
  schedule:
    - cron: "*/5 * * * *"   # 每5分钟运行
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Update README
        run: |
          echo "# Auto Update" > README.md
          echo "" >> README.md
          echo "Last update: $(date)" >> README.md

      - name: Commit changes
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add README.md
          git commit -m "update readme $(date)" || echo "no change"
          git push