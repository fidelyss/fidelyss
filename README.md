<h1 align="center">Hey 👋What's Up?</h1>

###

<div align="center">
  <img src="https://skillicons.dev/icons?i=html" height="60" alt="html5 logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=css" height="60" alt="css3 logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=js" height="60" alt="javascript logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=nodejs" height="60" alt="nodejs logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=ts" height="60" alt="typescript logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=react" height="60" alt="react logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=tailwind" height="60" alt="tailwindcss logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=nextjs" height="60" alt="nextjs logo"  />
  <img width="12" />
  <img src="https://cdn.simpleicons.org/sass/CC6699" height="60" alt="sass logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=threejs" height="60" alt="threejs logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=mongodb" height="60" alt="mongodb logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=postgres" height="60" alt="postgresql logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=py" height="60" alt="python logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=aws" height="60" alt="amazonwebservices logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=kubernetes" height="60" alt="kubernetes logo"  />
  <img width="12" />
  <img src="https://skillicons.dev/icons?i=docker" height="60" alt="docker logo"  />
</div>

###

<div align="center">
 <a href="https://www.linkedin.com/in/alisson-fidelis-426a58236/" target="_blank">
  <img src="https://img.shields.io/static/v1?message=LinkedIn&logo=linkedin&label=&color=0077B5&logoColor=white&labelColor=&style=for-the-badge" 
       height="25" 
       alt="linkedin logo" />
</a>
</div>

###

<div align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=fidelyss&theme=dracula" height="150" alt="trophy graph"  />
</div>

###

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
