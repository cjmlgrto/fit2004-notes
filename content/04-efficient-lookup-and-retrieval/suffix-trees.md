[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Suffix Trees

### Properties

- Are like Prefix Trees / Tries, but every suffix of an input string is inserted into the tree
	- Note that this then takes O(M<sup>2</sup>) to construct
- Allows for O(M) searching of substrings, where M is the length of the substring
- Space complexity however is at O(M<sup>2</sup>), where M is the size of the string for suffix tree
	- Save space by compressing branches with only 1 child (e.g. a trail like `p -> p -> l -> e` can be combined into a single key, `pple` and just compared letter by letter
	- Or, save space using a tuple `(x,y)`, that represents the boundary indices substring in the original string— and comparisons directly occur through the original string— thus, total number of nodes reduces to O(M)

### Substring Search

- Similar to prefix matching: traverse every node for corresponding letters until full substring is matched

### Counting occurences of a substring

- First, substring search
- Then count the number of leaf nodes under the trailing node's subtree

### Finding longest repeated substring

- Find the deepest node in the tree with at least two children
- The trail of that deepest node with the _most_ children is the longest repeated substring


