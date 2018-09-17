
---
layout: post
title: "Python src Import"
date: 2018-09-17
---
When I was trying to organize my python modules with src structure, it brings me a lot of confusion. Here are some tips I learned along the way, hope it helps to you.

Assume we have a src under the /home/code/
```
- src/
  - __init__.py
  - src_1/
    - __init__.py
    - module_1.py
  - src_2/
    - __init__.py
    - module_2.py
```
Assume you want to run the `module_2.py` (main entrance of your code, or a test cases), in `module_2.py` you want to use some function in `module_1.py`. 

Basically, you have two choices, 1) absolute path; 2) relative path. I will elaborate them individually as follows:

1. absoluate path:
    -  `import src_1.module_1`
    using this import way, you should `cd Pakcage` folder and run the script like this: `python -m src_2.module_2`, the reason is current location path `/home/code/src` would be your src search path

    - `import src.src_1.module_1`
    using this import way, you should `cd /home/code` folder and run `python -m src.src_2.module_2`, the reason is `src` is as the main package, and `import src_1.module_1` would cause `src_1` not recognized. (not clear about this, need more explanation)

2. relative path:
    - `import ..src_1.module_1`
    relative path is for package, not for the code location. when you are under `/home/code/src/`, and run the `python -m src_2.module_2`, you will see the error `attempted relative import beyond top-level package`, because the top-level package is `src_2`, `..` doesn't know where to go. So you need `cd /home/code/`, and run `python -m src.src_2.module_2`, to use this relative path. 

In conclusion, when designing the package, you need to know where you want to start the main script, in order to import your local packages. If it is an independent package, so all the other modules using this package will import the module outside this module, so you better use second method of abosluate path to call modules under different sibling pakcages/folders of parent pakcage. 
  