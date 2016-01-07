Game Dev Curriculum
=======================
### Editing
Just edit `Introduction to Game Development.md`, which has everything. If spaces don't work, try `Introduction\ to\ Game\ Development.md`.

### Viewing in Browser
Run `make` to generate output.html, a compiled HTML version of `Introduction to Game Development.md`, and then open it in your browser. This lets you see on your computer your changes to `Introduction to Game Development.md`.

`output.html` is local to your computer. If you want to change what `http://yuxshao.github.io/learn-gamedev/` shows, run `make pub` (not `make`) instead, commit your changes, and then push the changes to GitHub.

### Deploying
(below is some ADI-related stuff; shouldn't matter to us)

_Note: In order to deploy these projects, you need to have SSH access to `adi-website`.  Ask Dan, Nate, Eunice, or Raymond for help setting this up._

Run `make deploy` to deploy your curriculum.  The first time, it will ask for a path slug.  Give something **unique**!
