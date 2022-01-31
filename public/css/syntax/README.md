# pygments-css


[Pygments](http://pygments.org), a Python-based code highlighting tool, comes with a set of builtin styles (not css files) for code highlighting. You have to generate a CSS file using the command line.

You can generate these yourself, but this git repository has already generated them for you.


build
-----

These css files were generated using pygmentize on the command line like so::

    pygmentize -S default -f html -a .highlight > default.css

You can remove or change the top-level class by removing or modifying `-a .highlight` in the `makefile`.

To regenerate them all with whichever ``pygments`` version you are using, run

    git clone <this repo>
    cd pygments-css
    make cssfiles

> Code block will look like this.
```yml
highlighter-theme: monokai //you can change your syntax color scheme.
date_format: "%Y-%M-%D" //and date format.
```

### Screenshots
#### Page
![alt text](/public/img/screenshot-1.png)
#### Articles
![alt text](/public/img/screenshot-2.png)
#### Page - Mobile
![alt text](/public/img/screenshot-m1.png)
#### Page - Articles
![alt text](/public/img/screenshot-m2.png)
