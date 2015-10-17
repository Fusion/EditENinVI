# EditENinVI

This is a very silly little util that lets you edit Evernote notes directly from your heavy client in vim.

## Warning

The first time you save an existing note with this tool, it will write what it believes is the note's true content in a hidden field. This means that, from now on, if you edit this note in Evernote then in this tool, you will lose edits made in Evernote itself.

## Prerequisites

The prerequisites are:

- AppleScript (therefore, OS X)
- Ruby
- multimarkdown (`brew install multimarkdown`)
- Evernote heavy client
- vim
- iTerm

- and more if you wish to use the plugins described below

Some of these dependencies can be replaced by your favorite tool. For instance, you could use macvim or terminal.

# PLUGINS

Currently, if you have the proper binaries installed, you can go further than just using markdown.

## graphviz

Make sure that you have 'dot' installed in /usr/local/bin and you will be able to add entries such as:

    ''''diagram
    digraph G {

    subgraph cluster_1 {
    b2 -> a3;
    a3 -> a0;

    start [shape=Mdiamond];
    end
    ''''

## plantuml

Two requirements: java must be available, and you need, for now to put 'plantuml.jar' in ~/bin/

You will then be able to type:

    ''''plantuml
    @startuml
    Alice -> Bob: Authentication Request
    Bob --> Alice: Authentication Response
    Alice -> Bob: Another authentication Request
    Alice <-- Bob: another authentication Response
    @enduml
    ''''

Note that, due to plantuml being Java-based, there is a time penalty for starting the JVM, etc.

## LaTeX

You really need motivation to use this one. Not just because TeX is complex, but because getting it working on OS X is challenging. Here is my easiest-and-not-all-that-satisfying setup:

1. Install imagemagick (from http://cactuslab.com/imagemagick/)
2. Install MacTeX (from https://tug.org/mactex/mactex-download.html)
3. Install PanDoc

I would rather use dvipng but brew and libpng are currently at odds. Note that editeninvi makes some path assumptions and you may have to fix them: 'convert' is /opt/ImageMagick/bin/convert and latex is /usr/local/texlive/2015/bin/x86_64-darwin/pdflatex.

Then, try, for instance:

    ''''latex
    \documentclass[preview]{standalone}
    \begin{document}
    Hello. This is a test.
    \begin{equation}
    L = 2
    \end{equation}
    \end{document}
    '''

Again, due to how I trim page numbers from the PDF document, you will very likely have to make some adjustments.

# Roff

(really, we are using groff under the hood)

Very old yes still very useful. You can use it to write manpages, whole books, scientific papers, diagrams...

Example -- an equation:

    '''roff
    .EQ
    F(X) ˜=˜ left {
    matrix{
      lcol{ {4 X} above
        {1}above
        {4 ( 1 - X )}
      }
      lcol{
        { roman{"if "}
          0 <= X <= 1 smallover 4
        } above
        { roman{"if "}
          1 smallover 4 <= X <=
          3 smallover 4
        } above
        { roman{"if "}
          3 smallover 4 <= X <= 1
        }
      }
    }
    .EN
    '''

Example -- a diagram:

    '''roff
    .PS
    box invis \"Start\" \"Here\"; arrow
    box \"Step 1\"; arrow
    circle \"Step 2\"; arrow
    ellipse \"Step 3\"; arrow
    box \"Step 4\"; arrow
    box invis \"End\"
    .PE
    '''

Example -- a table:

    '''roff
    .TS
    center, box, tab(:);
    c s s
    c | c | c
    l | l | l.
    Mergers and Acquisitions Team
    =
    Employee:Title:Location
    =_
    Jones, James:Marketing Manager:New York Office
    Smith, Charles:Sales Manager:Los Angeles Office
    Taylor, Sarah:R&amp;D Manager:New York Office
    Walters, Mark:Information Systems Manager:Salt Lake City Office
    Zur, Mike:Distribution Manager:Portland Office
    .TE
    '''

Example -- some nicely formatted text:

    '''roff
    .TL
    Our Important Report
    .AU
    Dean Provins
    .AI
    Noted Author and Hacker
    Student of Life and the University of Calgary
    .AB
    Noted author and hacker, Dean Provins reveals all in the much heralded
    HOWTO for &#92;fIgroff&#92;fP. In this classic document, Provins describes the
    inner workings of one of the earliest machine document processing systems
    available.
    Readers are encouraged to try any or all the examples provided.
    .AE
    .NH
    Machine Document Processing
    .LP
    In this chapter, we see that computers have finally come into their own.
    No more must workers labour over Gutenberg presses, as they have for
    generations.
    .NH
    Macros
    .LP
    There are many macro packages available for &#92;fIgroff&#92;fP and friends. There
    are even more available for its predecessor &#92;fItroff&#92;fP.
    .ds MS &#92;fIms&#92;fP
    .NH 2
    The &#92;*[MS] Macro Package
    .LP
    The &#92;*[MS] macros provide a much needed lift for those toiling with the
    basic &#92;fItroff&#92;fP commands. They (the &#92;*[MS] macros) are now used
    extensively by writers the world over.
    '''

(source: http://www.zen89632.zen.co.uk/Groff/Eqn/eqnguide.pdf)

# HOTKEYS

To automate the use of this script, I have used Automator to create a service that runs it in a shell. I then used the System Preferences to configure a hotkey (in my case <opt><cmd>E) that will invoke the service.

The script will take the currently opened note and open a vim terminal tab. Every time you save your file, Evernote will be updated. When you exit this vim session, the script will stop listening.

I lifted a couple stylesheets to style your note. Setting '$style' to ':unstyled' will write lighter notes.

Use this script at your own risk, although the most serious risk I can think of is that you will get really ugly notes. I hope to fix most of the quirks down the road...

-Chris.
