<!-- CONNECTING PROJECT WITH GIT HUB -->
[01] Step> Login into GIT Account
[02] Step> Create a Repo with project name.
[03] Step> Select Private and Keep README unchecked
[04] Step> Initialize your project with:
     $ git init
[05] Step> Copy your Repo link something like:
     $ git remote add origin https://github.com/your-username/project.git
     [NOTE] Verify Remote connection with command:
     $ git remote -v
     [It_should_output:]
     origin  https://github.com/your-username/my-laravel-project.git (fetch)
     origin  https://github.com/your-username/my-laravel-project.git (push)
[06] Commit and Push Your Project
     git status
     git add .
     git commit -m "Initial commit"
     git branch -M main
     git push -u origin main
[07] Verify on GitHub
     Go to GitHub → Your Repo (my-laravel-project).