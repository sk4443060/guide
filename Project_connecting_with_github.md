<!-- CONNECTING PROJECT WITH GIT HUB -->
[01] Step> Login into GIT Account
[02] Step> Create a Repo with project name.
[03] Step> Select Private and Keep README unchecked
[04] Step> Initialize your project with:
     $ git init
[05] Step> Copy your Repo link something like:
     $ git remote add origin https://github.com/your-username/project.git
     (If you find origin already exist run $ git remote remove origin)
     (If you run the wrong remote ---/your-username/wrong.git stil you can remove it with the remove command and move with normal to continue)
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

     NOTE
     $ git reset (It will undo $ git add .)
     
[07] Verify on GitHub
     Go to GitHub → Your Repo (my-laravel-project).

<!-- WORKING WITH BRANCHING WITH REMOTE GIT -->
As you already in main branch. If you want to check run this command
     $ git branch

     This will show as:
     * main [Star shows you are in this branch, means * indicating current branch]
     development

     If you are not in main
     $ git checkout main

     Then pull the latest changes (just in case):
     $ git reset --hard origin/main
     $ git pull origin main
     Or
     $ git clone https://<username>:<token>@github.com/<username>/<repo>.git temp
     
Create a New Branch Called development
     $ git checkout -b development

     This:
          - Creates a new branch named development
          - Automatically switches you to that branch
     
Push development Branch to GitHub
     $ git push -u origin development

     Now GitHub also has your development branch.

Pull Code from main to development
     Once you're in development branch and want to pull new updates from main, do this:
     $ git checkout development
     $ git reset --hard origin development
     $ git pull origin main

If you want to mearge from all branch follow:
     $ git checkout [BRANCH NAME]
     $ git reset --hard origin/[SAME BRANCH NAME IN WHICH YOU ARE]
     $ git pull origin [SAME BRANCH NAME IN WHICH YOU ARE]
     $ git pull origin [OTHER BRANCH]

     Here you have successfully merged the two branches code.
