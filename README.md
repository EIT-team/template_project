#Set up version control for a new project in GitHub

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


    

