# Portfolio Part 1: Component Brainstorming

- **Name**: Izza Ewana Ayob
- **Dot Number**: Ayob.6
- **Due Date**: 9/16/2024 3pm

## Assignment Overview


The overall goal of the portfolio project is to have you design and implement
your own OSU component. There are no limits to what you choose to design and
implement, but your component must fit within the constraints of our software
sequence discipline. In other words, the component must extend from Standard and
must include both a kernel and a secondary interface.

Because this is a daunting project, we will be providing you with a series of
activities to aid in your design decisions. For example, the point of this
assignment is to help you brainstorm a few possible components and get some
feedback. For each of these components, you will need to specify the high-level
design in terms of the software sequence discipline. In other words, you will
describe a component, select a few kernel methods for your component, and select
a few secondary methods to layer on top of your kernel methods.

You are not required to specify contracts at this time. However, you are welcome
to be as detailed as you'd like. More detail means you will be able to get more
detailed feedback, which may help you decide which component to ultimately
implement.

## Assignment Checklist


To be sure you have completed everything on this assignment, we have littered
this document with TODO comments. You can browse all of them in VSCode by
opening the TODOs window from the sidebar. The icon looks like a tree and will
likely have a large number next to it indicating the number of TODOS. You'll
chip away at that number over the course of the semester. However, if you'd
like to remove this number, you can disable it by removing the following
line from the `settings.json` file:

```json
"todo-tree.general.showActivityBarBadge": true,
```

Which is not to be confused with the following setting that adds the counts
to the tree diagram (you may remove this one as well):

```json
"todo-tree.tree.showCountsInTree": true,
```

## Assignment Learning Objectives


Without learning objectives, there really is no clear reason why a particular
assessment or activity exists. Therefore, to be completely transparent, here is
what we're hoping you will learn through this particular aspect of the portfolio
project. Specifically, students should be able to:

1. Integrate their areas of interest in their personal lives and/or careers with
   their knowledge of software design
2. Determine the achievablility of a software design given time constraints
3. Design high-level software components following the software sequence
   discipline

## Assignment Rubric: 10 Points


Again, to be completely transparent, most of the portfolio project, except the
final submission, is designed as a formative assessment. Formative assessments
are meant to provide ongoing feedback in the learning process. Therefore,
the rubric is designed to assess the learning objectives *directly* in a way
that is low stakes—meaning you shouldn't have to worry about the grade. Just
do good work.

1. (3 points) Each design must align with your personal values and long-term
   goals. Because the goal of this project is to help your build out a
   portfolio, you really ought to care about what you're designing. We'll give
   you a chance to share your personal values, interests, and long-term goals
   below.
2. (3 points) Each design must be achievable over the course of a single
   semester. Don't be afraid to design something very small. There is no shame
   in keeping it simple.
3. (4 points) Each design must fit within the software sequence discipline. In
   other words, your design should expect to inherit from Standard, and it
   should contain both kernel and secondary methods. Also, null and aliasing
   must be avoided, when possible. The methods themselves must also be in
   justifiable locations, such as kernel or secondary.

## Pre-Assignment

> Before you jump in, we want you to take a moment to share your interests
> below. Use this space to talk about your career goals as well as your personal
> hobbies. These will help you clarify your values before you start
> brainstorming. Plus it helps us get to know you better! Feel free to share
> images in this section.

I have multiple interests but I don't think they're related to my major (I kinda want this portfolio to be related to my major). But these are some of my passions:
1. Paint & do sketches.
2. Read (novels).
3. I really love listening & exploring new music/songs (my fav app is spotify).
4. I like watching anime too my current favourite is one peace.
5. Journaling.

## Assignment


As previously stated, you are tasked with brainstorming 3 possible components.
To aid you in this process, we have provided [some example components][example-components]
that may help you in your brainstorming. All of these components were made at
some point by one of your peers, so you should feel confident that you can
accomplish any of them.


There is no requirement that you use any of the components listed above.
If you want to model something else, go for it! Very common early object
projects usually attempt to model real-world systems like banks, cars,
etc. Make of this whatever seems interesting to you, and keep in mind that
you're just brainstorming right now. You do not have to commit to anything.

### Example Component

To help you brainstorm a few components, we've provided an example below of a
component you already know well: NaturalNumber. We highly recommend that you
mirror the formatting as close as possible in your designs. By following this
format, we can be more confident that your designs will be possible.

- Example Component: `NaturalNumber`
  - **Description**:
    - The purpose of this component is to model a non-negative
      integer. Our intent with this design was to keep a simple kernel that
      provides the minimum functionality needed to represent a natural number.
      Then, we provide more complex mathematical operations in the secondary
      interface.
  - **Kernel Methods**:
    - `void multiplyBy10(int k)`: multiplies `this` by 10 and adds `k`
    - `int divideBy10()`: divides `this` by 10 and reports the remainder
    - `boolean isZero()`: reports whether `this` is zero
  - **Secondary Methods**:
    - `void add(NaturalNumber n)`: adds `n` to `this`
    - `void subtract(NaturalNumber n)`: subtracts `n` from `this`
    - `void multiply(NaturalNumber n)`: multiplies `this` by `n`
    - `NaturalNumber divide(NaturalNumber n)`: divides `this` by `n`, returning
      the remainder
    - ...
  - **Additional Considerations** (*note*: "I don't know" is an acceptable
    answer for each of the following questions):
    - Would this component be mutable? Answer and explain:
      - Yes, basically all OSU components have to be mutable as long as they
        inherit from Standard. `clear`, `newInstance`, and `transferFrom` all
        mutate `this`.
    - Would this component rely on any internal classes (e.g., `Map.Pair`)?
      Answer and explain:
        - No. All methods work with integers or other NaturalNumbers.
    - Would this component need any enums or constants (e.g.,
      `Program.Instruction`)? Answer and explain:
        - Yes. NaturalNumber is base 10, and we track that in a constant called
          `RADIX`.
    - Can you implement your secondary methods using your kernel methods?
      Answer, explain, and give at least one example:
      - Yes. The kernel methods `multiplyBy10` and `divideBy10` can be used to
        manipulate our natural number as needed. For example, to implement
        `increment`, we can trim the last digit off with `divideBy10`, add 1 to
        it, verify that the digit hasn't overflown, and multiply the digit back.
        If the digit overflows, we reset it to zero and recursively call
        `increment`.

Keep in mind that the general idea when putting together these layered designs
is to put the minimal implementation in the kernel. In this case, the kernel is
only responsible for manipulating a digit at a time in the number. The secondary
methods use these manipulations to perform more complex operations like
adding two numbers together.

Also, keep in mind that we don't know the underlying implementation. It would be
completely reasonable to create a `NaturalNumber1L` class which layers the
kernel on top of the existing `BigInteger` class in Java. It would also be
reasonable to implement `NaturalNumber2` on top of `String` as seen in
Project 2. Do not worry about your implementations at this time.

On top of everything above, there is no expectation that you have a perfect
design. Part of the goal of this project is to have you actually use your
component once it's implemented to do something interesting. At which point, you
will likely refine your design to make your implementation easier to use.

### Component Designs

> Please use this section to share your designs.

- Component Design #1: `MusicPlaylist`
  - **Description**:
    - The purpose of this component is to model a collection of songs in a playlist. The kernel provides minimal functionality to handle the basic structure of a playlist, such as adding or removing songs. The secondary methods will enable more complex interactions, such as shuffling, filtering by genre, or getting a recommended next song (am considering a blend between two people favourites or counting percentage of smiliarity in music taste).

  - **Kernel Methods**:
    - `void addSong(Song s)`: Adds the song s to the playlist.
    - `Song removeSong(int index)`: Removes and returns the song at the specified index.
    - `boolean isEmpty()`: Reports whether the playlist is empty.
    - `int size()`: Returns the number of songs in the playlist.

  - **Secondary Methods**:
    - `void shuffle()`: Randomly rearranges the order of songs in the playlist.
    - `List<Song> filterByGenre(String genre)`: Returns a list of songs in the playlist that belong to the specified genre.
    - `Song getNextRecommendedSong()`: Recommends the next song based on the user's listening history or playlist order.
    - `void play()`: Starts playing the songs in the playlist from the first track.
    - `Song getCurrentSong()`: Returns the currently playing song
    - `void skip()`: Skips to the next song in the playlist.
  - **Additional Considerations** (*note*: "I don't know" is an acceptable
    answer for each of the following questions):
    - Would this component be mutable? Answer and explain:
      - Yes, playlists are mutable as songs are frequently added, removed, and reordered. The kernel methods inherently modify the playlist by adding and removing songs.

    - Would this component rely on any internal classes (e.g., `Map.Pair`)?
      Answer and explain:
      - list? queue?
    - Would this component need any enums or constants (e.g.,
      `Program.Instruction`)? Answer and explain:
      - Yes, possibly an enum for Genre to categorize songs more easily, or constants for specifying the default playback order.
    - Can you implement your secondary methods using your kernel methods?
      Answer, explain, and give at least one example:
      - Yes. For example, shuffle() can be implemented by iterating over the list of songs and swapping them randomly. filterByGenre() would iterate through the playlist and collect songs where the genre matches the input. Another example is play(), which can use a loop to sequentially retrieve songs and start playing them from the first track.


- Component Design #2: `EmotionBookHighlighter`
  - **Description**:
    - The purpose of this component is to model a system that highlights passages from books, categorizes them based on associated emotions, and allows for easy retrieval of quotes and their corresponding page numbers. The kernel provides basic functionality for storing and retrieving highlighted passages and emotions. Secondary methods will enable more complex operations, such as sorting by emotion or retrieving quotes for specific emotions.
  - **Kernel Methods**:
    - `void highlightPassage(String quote, int page, String emotion)`: Highlights a passage from the book, associates it with a specific emotion, and stores the page number.
    - `String getQuote(int index)`: Retrieves the highlighted quote at the given index.
    - `String getEmotion(int index)`: Retrieves the emotion associated with the quote at the given index.
    - `int getPage(int index)`: Retrieves the page number of the quote at the given index.
  - **Secondary Methods**:
    - `List<String> getQuotesByEmotion(String emotion)`: Returns a list of all quotes that are associated with a particular emotion.
    - `void sortQuotesByEmotion()`: Sorts the highlighted quotes by their associated emotions in alphabetical order or by predefined emotional categories (e.g., happy, sad, angry).
    - `List<String> getAllQuotes()`: Retrieves all the highlighted quotes from the book.
    - `Map<String, Integer> getQuoteWithPage(int index)`: Returns a quote along with its associated page number as a key-value pair.
    - `List<String> getSortedEmotions()`: Returns a sorted list of all emotions that have been associated with highlighted quotes.
    - `void removeHighlight(int index)`: Removes a highlighted passage from the system.
    - `int getNumberOfHighlights()`: Returns the total number of highlighted passages.
  - **Additional Considerations** (*note*: "I don't know" is an acceptable
    answer for each of the following questions):
    - Would this component be mutable? Answer and explain:
      - Yes, this component is mutable. The highlighted passages, emotions, and page numbers will be constantly added, removed, or updated, making it inherently mutable.
    - Would this component rely on any internal classes (e.g., `Map.Pair`)?
      Answer and explain:
      - Yes, the component would likely rely on internal classes such as Pair<String, Integer> or a similar structure to store quotes along with their page numbers. A Map<String, List<Pair<String, Integer>>> could be used to associate each emotion with a list of quotes and their respective pages.
    - Would this component need any enums or constants (e.g.,
      `Program.Instruction`)? Answer and explain:
      - Yes, an enum could be useful to define a set of standard emotions, such as Emotion.HAPPY, Emotion.SAD, Emotion.ANGRY, etc., for consistency across the system. You might also have a constant like DEFAULT_SORT_ORDER for sorting emotions in a particular order.
    - Can you implement your secondary methods using your kernel methods?
      Answer, explain, and give at least one example:
      - Yes. For example, getQuotesByEmotion() can iterate over the list of highlighted quotes and return those associated with the specified emotion. Similarly, sortQuotesByEmotion() can use a basic sorting algorithm, leveraging the emotional categories stored with each quote.


- Component Design #3: `Emotion-Based-Journal`
  - **Description**:
    - This component models a journaling system where users can write journal entries and associate each entry with an emotion or topic. The kernel focuses on basic functionality like adding, removing, and retrieving entries, while secondary methods enable more complex operations such as searching, sorting by emotions, and extracting key insights.
  - **Kernel Methods**:
    - `void addEntry(String entry, String emotion)`: Adds a journal entry associated with a specific emotion (e.g., happy, sad, anxious).
    - `String getEntry(int index)`: Retrieves the journal entry at the specified index.
    - `String getEmotion(int index)`: Returns the emotion associated with the journal entry at the specified index.
    - `void removeEntry(int index)`: Removes the journal entry at the given index.
    - `int getTotalEntries()`: Returns the total number of journal entries.
  - **Secondary Methods**:
    - `List<String> searchByEmotion(String emotion)`: Returns a list of all journal entries associated with the specified emotion.
    - `void sortByEmotion()`: Sorts all journal entries by emotion for easier retrieval and reflection.
    - `Map<String, Integer>` getEntriesByEmotionCount(): Returns a count of how many entries have been categorized under each emotion.
    - `String getMostFrequentEmotion()`: Retrieves the emotion that appears most frequently across all journal entries.
    - `List<String> getEntriesByKeyword(String keyword)`: Searches for and returns entries that contain a specific keyword or phrase.
    - `void addQuote(String quote, int page)`: Adds a favorite quote from a book along with the page number it appears on, which could be useful for reflecting on inspiring ideas during journaling.
    - `Map<String, Integer> getQuotes()`: Returns all stored quotes along with their page numbers.
    - `String generateSummary()`: Generates a brief summary of the user's recent entries, including the most frequent emotions, recurring themes, or significant quotes.
  - **Additional Considerations** (*note*: "I don't know" is an acceptable
    answer for each of the following questions):
    - Would this component be mutable? Answer and explain:
      - Yes, it would be mutable as journal entries are constantly being added, removed, or modified.

    - Would this component rely on any internal classes (e.g., `Map.Pair`)?
      Answer and explain:
      - Yes, it could rely on internal classes such as Map<String, List<String>> to store emotions as keys and associated journal entries as values, or use a Pair<String, Integer> structure to store quotes and their corresponding page numbers.
    - Would this component need any enums or constants (e.g.,
      `Program.Instruction`)? Answer and explain:
      - Yes, an enum could be useful for predefined emotions such as Emotion.HAPPY, Emotion.SAD, or Emotion.ANXIOUS, ensuring consistency when categorizing entries.

    - Can you implement your secondary methods using your kernel methods?
      Answer, explain, and give at least one example:
      - Yes. For example, searchByEmotion() can iterate over the journal entries, using the getEmotion() method to find matching emotions. Similarly, getEntriesByKeyword() would search through the entries using a basic string-matching algorithm.

## Post-Assignment

The following sections detail everything that you should do once you've
completed the assignment.

### Changelog


At the end of every assignment, you should update the
[CHANGELOG.md](../../CHANGELOG.md) file found in the root of the project folder.
Since this is likely the first time you've done this, we would recommend
browsing the existing file. It includes all of the changes made to the portfolio
project template. When you're ready, you should delete this file and start your
own. Here's what I would expect to see at the minimum:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Calendar Versioning](https://calver.org/) of
the following form: YYYY.0M.0D.

## YYYY.MM.DD

### Added

- Designed a <!-- insert name of component 1 here --> component
- Designed a <!-- insert name of component 2 here --> component
- Designed a <!-- insert name of component 3 here --> component
```

Here `YYYY.MM.DD` would be the date of your submission, such as 2024.04.21.

You may notice that things are nicely linked in the root CHANGELOG. If you'd
like to accomplish that, you will need to make GitHub releases after each pull
request merge (or at least tag your commits). This is not required.

In the future, the CHANGELOG will be used to document changes in your
designs, so we can gauge your progress. Please keep it updated at each stage
of development.

### Submission


If you have completed the assignment using this template, we recommend that
you convert it to a PDF before submission. If you're not sure how, check out
this [Markdown to PDF guide][markdown-to-pdf-guide]. However, PDFs should be
created for you automatically every time you save, so just double check that
all your work is there before submitting. For future assignments, you will
just be submitting a link to a pull request. This will be the only time
you have to submit any PDFs.


### Peer Review

<!-- TODO: review the peer review guidelines then delete this comment -->

Following the completion of this assignment, you will be assigned three
students' component brainstorming assignments for review. Your job during the
peer review process is to help your peers flesh out their designs. Specifically,
you should be helping them determine which of their designs would be most
practical to complete this semester. When reviewing your peers' assignments,
please treat them with respect. Note also that we can see your comments, which
could help your case if you're looking to become a grader. Ultimately, we
recommend using the following feedback rubric to ensure that your feedback is
both helpful and respectful (you may want to render the markdown as HTML or a
PDF to read this rubric as a table).

| Criteria of Constructive Feedback | Missing                                                                                                                           | Developing                                                                                                                                                                                                                                | Meeting                                                                                                                                                               |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Specific                          | All feedback is general (not specific)                                                                                            | Some (but not all) feedback is specific and some examples may be provided.                                                                                                                                                                | All feedback is specific, with examples provided where possible                                                                                                       |
| Actionable                        | None of the feedback provides actionable items or suggestions for improvement                                                     | Some feedback provides suggestions for improvement, while some do not                                                                                                                                                                     | All (or nearly all) feedback is actionable; most criticisms are followed by suggestions for improvement                                                               |
| Prioritized                       | Feedback provides only major or minor concerns, but not both. Major and minar concerns are not labeled or feedback is unorganized | Feedback provides both major and minor concerns, but it is not clear which is which and/or the feedback is not as well organized as it could be                                                                                           | Feedback clearly labels major and minor concerns. Feedback is organized in a way that allows the reader to easily understand which points to prioritize in a revision |
| Balanced                          | Feedback describes either strengths or areas of improvement, but not both                                                         | Feedback describes both strengths and areas for improvement, but it is more heavily weighted towards one or the other, and/or descusses both but does not clearly identify which part of the feedback is a strength/area for improvement  | Feedback provides balanced discussion of the document's strengths and areas for improvement. It is clear which piece of feedback is which                             |
| Tactful                           | Overall tone and language are not appropriate (e.g., not considerate, could be interpreted as personal criticism or attack)       | Overall feedback tone and language are general positive, tactul, and non-threatening, but one or more feedback comments could be interpretted as not tactful and/or feedback leans toward personal criticism, not focused on the document | Feedback tone and language are positive, tactful, and non-threatening. Feedback addesses the document, not the writer                                                 |

### Assignment Feedback

If you'd like to give feedback for this assignment (or any assignment, really),
make use of [this survey][survey]. Your feedback helps make assignments
better for future students.

<!-- TODO: follow the link to share your feedback then delete this comment -->

[example-components]: https://therenegadecoder.com/code/the-never-ending-list-of-small-programming-project-ideas/
[markdown-to-pdf-guide]: https://therenegadecoder.com/blog/how-to-convert-markdown-to-a-pdf-3-quick-solutions/
[survey]: https://forms.gle/dumXHo6A4Enucdkq9
