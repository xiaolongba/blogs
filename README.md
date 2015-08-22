blogs
=====

Blogs writing by markdown by using static site generator [Pelican][1]. Served by gh-pages on github by using [ghp-import][2]

## Install

    :::shell
    sudo pip install -r requirements.txt

## Usage

Make sure we are woring in `master` branch before post any blogs. `gh-pages` branch is generated by [ghp-import][2] and any edit on it will lost.

1. Post new blogs in `content` directory
2. Commit blogs to github by using `git add`, `git commit` and `git push`
3. Publish blogs by using `make github`

[1]: https://github.com/getpelican/pelican
[2]: https://github.com/davisp/ghp-import
