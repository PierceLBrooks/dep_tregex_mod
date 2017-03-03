# dep\_tregex\_mod

This is a fork of [dep_tregex](https://github.com/yandex/dep_tregex), a Python 2 module that implements Stanford Tregex-inspired language for rule-based dependency tree manipulation. This fork extends the original functionality to allow for optional matchings using ``?``, as outlined in [Introduction to Tregex.ppt](http://nlp.stanford.edu/software/tregex/The_Wonderful_World_of_Tregex.ppt).

Documentation: https://szymciolop.github.io/dep_tregex_mod/.


# usage notes

Trees are represented internally as lists corresponding to [CoNNL-U format](http://universaldependencies.org/format.html).

```python
from dep_tregex import Tree
tree = Tree(forms, lemmas, cpostags, postags, feats, heads, deprels)
# where feats is of the form ['case=Nom', 'number=Plur', ...]
```

To get all nodes matching your tregex:

```python
from dep_tregex import parse_pattern
pattern = parse_pattern("x lemma 'be' and > y deprel 'NSUBJ'")
matchings, backrefs_map = [], {}
for node in range(1, len(tree) + 1):
    if pattern.match(tree, node, backrefs_map):
        matchings.append(node)
        # backrefs_map contains matchings for variables x, y
        # in this case x == node
```

To output you tree to a file:

```python
import dep_tregex

# for HTML:
html_file = open('tree.html', 'w')
dep_tregex.write_prologue_html(html_file)
dep_tregex.write_tree_html(file, html_file)
dep_tregex.write_epilogue_html(html_file)

# for CoNLL-U:
conll_file = open('tree.conll', 'w')
dep_tregex.write_tree_conll(conll_file, tree)
```
