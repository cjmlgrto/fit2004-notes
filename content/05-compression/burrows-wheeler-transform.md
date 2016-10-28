[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Burrows-Wheeler Transform

### Compressing Text

1. Given an input string `S`, generate |`S`| cyclic rotations.
2. Sort these strings into alphabetical order by first character
3. Collate all the last characters of every string
4. These characters combined form the `BWT`— the encoded version
5. Then, compress repeated characters by placing a number in front of a character (this represents the number of repeats)
6. The final string is the compressed, encoded text

#### Example

`CAR$` generates the following (`$` represents the end of the text):

```
CAR$
$CAR
R$CA
AR$C
```

Sorted alphabetically, we get

```
$CAR
AR$C
CAR$
R$CA
```

Collating the last characters then labelling the number of characters, we get: `1R1C1$1A`.

### Decompressing Text

1. Let `bwt` be the input string.
- Create a list, `F`, that contains the sorted version of `bwt`.
- Create a list, `N`, that numbers each occurence of every character in `bwt`.
- Create a list, `R`, that ‘ranks’ each unique character in `F`.
- Create a list, `L`, that is essentially `bwt`.
- Set a counter called `row` to `0`, and create an empty string called `output`.
- Repeat n-1 times, where n is the length of the string, `bwt`:
	- Set the current character, `c` to the `row`-th item of `L`.
	- Insert this character at the beginning of `output`.
	- Let $r$ be the unicode number of the character, `c`. Add together the $r$-th item of `R` and `row`-th item of N. This should give a new integer. Set this as the new `row` number.
- Return the `output` string.

#### Example

Given `1R1C1$1A`, we de-encode to get RC$A. Then, we create our lists:

- `F`irst: $ACR
- `N`umerals: R<sub>1</sub> C<sub>1</sub> $<sub>1</sub> A<sub>1</sub>
- `R`ank: 

| | $ | A | C | R |
|---|---|---|---|---|
| First appears in `F` at position | 1 | 2 | 3 | 4

- `L`ast: RC$A

Then we repeat our algorithm, building up the word each time:

```
$
R$
AR$
CAR$
```

### Substring Searching

1. Let `bwt` be the input string, and `S` be the query
- Create a list, `F`, that contains the sorted version of `bwt`.
- Create a list, `L`, that is essentially `bwt`.
- Let `range` be the boundaries of a substring in `L` in the form `(start, end)`
- For every character `c` in `S`:
	- Find the first occurence of `c` in `L` (say, position `i`)
	- Once found, find where this `i`-th character of `L` occurs in `F`
	- Set the index of this found character to be the `start` of the `range`
	- Do the above steps for finding the _last_ occurence of `c` in `L` (by traversing backwards)
	- Set `end` accordingly
- If every character in `S` has been iterated, it has been found
- But if any character can't be found during the loop above, it is not found



