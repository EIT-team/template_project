#Set up version control for a new project 

Follow this instructions to set up a new project (corresponding to one EIT component or subcomponent, i.e.: ForwardSolver, ScouseTom, etc.) and upload it to GitHub. 

1. __Clone template project from Github in a sensible folder__

 ```bash
cd ~/workspace
git clone https://github.com/EIT-team/template_project.git
```

2. __Create new project folder for the component based on the structure of the template_project:__

 ```bash
cp -r template_project my_project
```
 Perhaps this is a good time to rename the component, i.e.: "Kirill's CGAL" -> "RatMesher"

3. __Copy project files in appropriate folder, e.g.:__

 ```bash
cd my_project
cp ~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/*/*.m src/matlab/
cp ~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/input.txt config/
cp ~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/Manual.docx doc/
cp ~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/input.inr resources/data
```

 Note:

 * Files > 100MB can't be uploaded to GitHub. In general, large files should be put in the Research Data space. If they're needed e.g. to run a test, you can make the test scp them in the right places, like:

 ```bash
scp user@ssh.rd.ucl.ac.uk:/path/to/input/file.mat resources/data/file.mat
```

 * Avoid at all costs uploading things that can be created from the uploaded source. E.g.:

 ```bash
~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/System/*.dll
~/Dropbox/SoftwareTidyUp/1_Meshing/CGAL_Kirill/ver1.2/*.exe
```

 * Add .gitignore files where needed to prevent GitHub from pushing unnecessary files or files that shouldn't be shared. E.g.:
 
 ```
 echo "**/*.dll" >.gitignore
 ```

4. __Add, commit and push everything to GitHub once you are happy with it:__

 ```
	git add -A .
	git commit -m "First commit of Kirill's CGAL for rats." 
	git push
```

5. __Create a development branch, where all the work will happen until next release:__

 ```bash
 	git checkout -b development
 ```

6. __Once there is a significant change pushed, or a new release, make a pull request and name someone else in the team code review your changes.__ See instructions [here](https://help.github.com/articles/using-pull-requests/).


	
-------

#Some useful tips

 * To prevent git from always asking for your credentials when typing a command, you can follow [this instructions](https://help.github.com/articles/generating-ssh-keys/).

 * If you are using __GitBash in Windows__, it'd may come in handy to have this added to your _.bash_profile_ (create it in ~/.bash_profile if it doesn't exist already) to keep track of your commands history:
 
 ```
PROMPT_COMMAND='history -a'
```

 * Also, a ___.gitconfig___ file may come in handy for git aliases (i.e. typing ```git st``` instead of ```git status``` or ```git push``` instead of ```git push origin master```), preventing git from always asking for your username, opening notepad++ automatically when you commit something without a message, etc. Here is an example _.gitconfig_:
 
 ```
# set your user tokens as environment variables, such as ~/.secrets
# See the README for examples.
[color]
  ui = true
[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green
[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red
  new = green
[alias]
  # add
  a = add # add
  chunkyadd = add --patch # stage commits chunk by chunk

  # via http://blog.apiaxle.com/post/handy-git-tips-to-stop-you-getting-fired/
  snapshot = !git stash save snapshot: $(date) && git stash apply stash@{0}
  snapshots = !git stash list --grep snapshot

  #via http://stackoverflow.com/questions/5188320/how-can-i-get-a-list-of-git-branches-ordered-by-most-recent-commit
  recent-branches = !git for-each-ref --count=15 --sort=-committerdate refs/heads/ --format='%(refname:short)'

  # branch
  b = branch -v # branch (verbose)

  # commit
  c = commit -m # commit with message
  ca = commit -am # commit all with message
  ci = commit # commit
  amend = commit --amend # ammend your last commit
  ammend = commit --amend # ammend your last commit

  # checkout
  co = checkout # checkout
  nb = checkout -b # create and switch to a new branch (mnemonic: "git new branch branchname...")

  # cherry-pick
  cp = cherry-pick -x # grab a change from a branch

  # diff
  d = diff # diff unstaged changes
  dc = diff --cached # diff staged changes
  last = diff HEAD^ # diff last committed change

  # log
  l = log --graph --date=short
  changes = log --pretty=format:\"%h %cr %cn %Cgreen%s%Creset\" --name-status
  short = log --pretty=format:\"%h %cr %cn %Cgreen%s%Creset\"
  simple = log --pretty=format:\" * %s\"
  shortnocolor = log --pretty=format:\"%h %cr %cn %s\"

  # pull
  pl = pull # pull

  # push
  ps = push # push

  # rebase
  rc = rebase --continue # continue rebase
  rs = rebase --skip # skip rebase

  # remote
  r = remote -v # show remotes (verbose)

  # reset
  unstage = reset HEAD # remove files from index (tracking)
  uncommit = reset --soft HEAD^ # go back before last commit, with files in uncommitted state
  filelog = log -u # show changes to a file
  mt = mergetool # fire up the merge tool

  # stash
  ss = stash # stash changes
  sl = stash list # list stashes
  sa = stash apply # apply stash (restore changes)
  sd = stash drop # drop stashes (destory changes)

  # status
  s = status # status
  st = status # status
  stat = status # status

  # tag
  t = tag -n # show tags with <n> lines of each tag message

  # svn helpers
  svnr = svn rebase
  svnd = svn dcommit
  svnl = svn log --oneline --show-commit
[format]
  pretty = format:%C(blue)%ad%Creset %C(yellow)%h%C(green)%d%Creset %C(blue)%s %C(magenta) [%an]%Creset
[mergetool]
  prompt = false
[mergetool "mvimdiff"]
  cmd = mvim -c 'Gdiff' $MERGED # use fugitive.vim for 3-way merge
  keepbackup = false
[merge]
  summary = true
  verbosity = 1
  tool = mvimdiff
[apply]
  whitespace = nowarn
[branch]
  autosetupmerge = true
[push]
  # 'git push' will push the current branch to its tracking branch
  # the usual default is to push all branches
    default = current
[core]
  autocrlf = false
  editor = 'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin
[advice]
  statusHints = false
[diff]
  # Git diff will use (i)ndex, (w)ork tree, (c)ommit and (o)bject
  # instead of a/b/c/d as prefixes for patches
  mnemonicprefix = true
    algorithm = patience
[rerere]
  # Remember my merges
  # http://gitfu.wordpress.com/2008/04/20/git-rerere-rereremember-what-you-did-last-time/
  enabled = true
[include]
  path = .gitconfig.user
[filter "lfs"]
    clean = git lfs clean %f
    smudge = git lfs smudge %f
    required = true
[user]
    name = your_name_here
    email = your_GitHub_email_here
```

You can customise this to have your details (username, path to preferred text/merge editor, etc). Once it's done, you can save it in _~/.gitconfig_. 






