Learning ICU usage, for getting a better job!

# Ability of ICU
* Code Page Conversion
* Collation
* Formatting
* Time Calculation
* Unicode Support
* Regular Expression
* Bidi
* Text Boundaries

# What's the Unicode
* coded character set
* character encoding scheme

ASCII is both a coded character set and a character encoding scheme.
Because it assigns 128 characters and control codes to consecutive numbers from 0 to 127.

## Glyphs versus Characters
- **Character** is the smallest semantic unit in a writing system.
- **Glyph** is the visual presentation of one or more characters.

For example:

1 character -> 2 glyphs
```
é -> e + ´
```
A font may represent the character `é` using two glyphs: the `e` and the acute-accent glyph.

2 characters -> 1 glyph
```
fi -> ﬁ (ligature)
```
The two characters `f` and `i` can be represent by a single glyph ligature glyph `ﬁ`.

## Character Encoding Forms and Schemes

- **Encoding Forms** include `UTF-8`, `UTF-16`, and `UTF-32`, which define how code points are represented as code units.
- **Encoding Schemes** have `UTF-16BE`, `UTF-16LE`, `UTF-32BE`, and `UTF-32LE`, define how code units are represented as bytes and their byte ordering.