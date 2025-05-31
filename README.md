# markdown-it-mathjax3

I'm using `hexo-renderer-markdown-it-plus` for blogging.

This is a fork of [markdown-it-mathjax3](https://github.com/tani/markdown-it-mathjax3) to support additional packages.

You can use plugin's options.tex.packages to control which packages to load.
- If it's not set, use the defaults (inherited from upstream)
- If it's an array, overwrite the defaults
- Otherwise, add elements of `packages["[+]"]`(a list, if it exists) to the defaults, then remove elements of `packages["[-]"]`

Usage scenarios:
- Enable the 'physics' and 'setoptions' packages. (Other packages are already included in defaults or not working properly, i.e. 'require' and 'autoload')
- Use 'colorv2' instead of 'color'.
- Disable some packages you don't need(?)

## An example with Hexo

Install 'hexo-renderer-markdown-it-plus'.

In hexo's `_config.yml`:
```yaml
markdown_it_plus:
   plugins:
      - plugin:
         name: @berrylium/markdown-it-mathjax3
         enable: true
         options:
           tags: 'ams' # see https://docs.mathjax.org/en/latest/input/tex/eqnumbers.html for more info.
           tex:
             packages:
               '[+]':
                  - physics
                  - setoptions
                  - colorv2
               '[-]':
                  - color
```

Test it by writing a post:
```md
colorv2:
$\color{ #0000ff}{blue}\ default$

physics:
$\eval{\sin x}_0^\pi=0$

setoptions: (the first gradient operator should have an arrow above it while the second one doesn't) 
$$
\setOptions[physics]{arrowdel=true}
\grad
\setOptions[physics]{arrowdel=false}
\grad
$$
```
