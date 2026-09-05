# ICU Services

## String, Properties and CharacterIterator

- **Unicode string** includes type definitions of UTF-16 strings and code points. It also contains many C `u_string` functions and the C++ `UnicodeString` class with many additional string functions.

- **Unicode properties** includes the C definitions and functions found in `uchar.h` as well as some macros found in `utf.h`. It also includes the C++ Unicode class.

- **Unicode string iteration** uses the macros in `utf.h` for the iteration of strings. In C++, ICU uses the characterIterator and its subclass.

## Conversion Basics

ICU transforms text from one encoding codepage to Unicode and back.

## Locale and Resources

- **Locale ID** specifies language and region information. C++ use the `Locale` class, while C APIs use null-terminated C strings `char const*` for Locale IDs.

- **Locale Object** represents a specific geographical, political, or cultural region.

- **Resource Bundle** stores locale-specific data. C++ use the `ResourceBundle` class. C use `ures_` interface.

## Locale and Services

Transliteration has pre-built transformations for case conversions, normalization conversions, the removal of given characters, and also for a variety of language and script transliterations.

Transliterations can be chained together to perform a series of operations and each step of the process can use a UnicodeSet to restrict the characters that are affected. There are two basic types of transliterators:
- Most natural language transliterators are written a rule-based transliterators.
- Transliterators can be written as text files using a simple language that is similar to regular expression syntax.
