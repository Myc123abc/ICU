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

## Date and Time

- **Calendar** is a base class for extracting calendar-related attributes from a `Date` value.
- **GregorianCalendar** is a class for represeting a Gregorian calendar.
- **TimeZero** is a base class for represeting a time zone.
- **SimpleTimeZero** is a class for represeting a time zone for use with a Gregorian calendar.

## Format and Parse

A formatter takes a value and produces a user-readable string that represents that value or takes a string and parses it to produce a value. The formatting services include general formatting, formatting numbers, formatting dates and times, and formatting messages.

- **Gneral formatting**
  - `Format`
  - `FieldPosition`
  - `ParsePosition`
  - `Formattable`

- **Formatting numbers**
  - `NumberFormatter` supports decimal values, currencies, measurement units, percentages, scientific notation, compact notation.
  - `NumberFormat` provides the basic fields and methods to format number objects and number primitives into localized strings and parse localized strings to number objects.
  - `DecimalFormat` provides the methods used to format number objects and number primitives into localized string and parse localized strings into number objects in base 10.
  - `DecimalFormatSymbols` is used by DecimalFormat to access localized number strings such as the grouping separators, the decimal separator, and the percent sign.

- **Formatting Dates and Times**
  - `DateFormat` provides the basic fields and methods for formatting date objects to localized strings and parsing date and time strings to date objects.
  - `SimpleDateFormat` is used to format date objects to localized strings and to parse date and time strings to date objects using a `GregorianCalendar`.
  - `DateFormatSymbols` is used to access localized date and time formatting strings, such as names of the months, days of the week, and the time zone.

- **Formatting Messages**
  - `MessageFormat` is used to produce a language-specific user message that contains numbers, currency, percentages, date, time, and string variables.
  - `ChoiceFormat` is used to map strings to ranges of numbers and to handle plural words and name series in user messages.

## Searching and Sorting

- **Collator** is the abstract base class of all classes that compare strings.
- **CollationElementIterator** provides an iterator for stepping through each character of a locale-specific string according to the rules of a specific collator object.
- **RuleBasedCollator** provides a sophisticated mechanism for comparing strings in a language-specific manner, and an interface that allows the user to specifically customize the sorting order.
- **CollationKey** enables the fast sorting of strings by representing a string as a sort key under the rules of a specific collator object.

## Text Analysis

The BreakIterator services can be used for formatting and handling text; locating the beggining and ending points of a word; counting words, sentences, and paragraphs; and listing unique words.
Specifically, text operations can be done to locate the following linguistic boundaries:
- Display text on the screen and locate places in the text where the BreakIterator can perform word-wrapping to fit the text within the margins.
- Located the begining and end of a word that the user has selected.
- Count graphemes (or characters), words, sentences, or paragraphs.
- Determine how far to move in the text store when the user hits an arrow key to move forward or backward one grapheme.
- Make a list of all the unique words in a document.
- Figure out whether or not a range of text contains only whole words.
- Capitalize the first letter of each word.
- Extract a particular unit from the text.

ICU provides the following classes for iteratoring over locale-specific text:

- **BreakIterator** is the abstract base class that defines the operations for finding and getting the positions of logical breaks in a string of text: character, words, sentences, and potential line breaks.
- **CharacterIterator** is the abstract base class for forward and backward iteration over a string of Unicode characters.
- **StringCharacterIterator** is used for forward and backward iteration over a string of Unicode characters.

