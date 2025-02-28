## Hello humans! 👋🧿 I come in peace! 

# ABOUT
🧿Graduated in Systems Analysis and Development, postgraduate in Information Security and IT Governance, currently studying for a bachelor's degree in administration and working in the call center sector. [LINKEDIN](https://www.linkedin.com/in/samuelcavalcanticosta/) <br>

# MY DIGITAL HERITAGE
🧿Subscribe in my Youtube Channel [LINK](https://www.youtube.com/@SamuelCavalcantiCosta/videos?sub_confirmation=1) <BR>
🧿Check my produtc in Hotmart [LINK](https://hotmart.com/en/marketplace/products?q=SAMUEL%20CAVALCANTI%20COSTA) <br>
🧿Read my books at Amazon [LINK](https://www.amazon.com/stores/Samuel-Cavalcanti-Costa/author/B0DQ8SPJVW?ref=ap_rdr&isDramIntegrated=true&shoppingPortalEnabled=true) <br>

# SUPPORT MY WORK
🧿Send me a gift [LINK](https://www.mercadolivre.com.br/presentes/presentei-me-8u5sv) <br>
🧿Donate [LINK](https://link.mercadopago.com.br/samuelccosta1991)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/YourUser/YourUser/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/YourUser/YourUser/output/github-contribution-grid-snake.svg">
  <img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/YourUser/YourUser/output/github-contribution-grid-snake.svg">
</picture>
name: generate animation

on:
  # run automatically every 24 hours
  schedule:
    - cron: "0 */24 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
    
  

jobs:
  generate:
    permissions: 
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
          
          
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
