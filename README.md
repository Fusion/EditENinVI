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

Some of these can be replaced by your favorite tool. For instance, you could use macvim or terminal.

To automate the use of this script, I have used Automator to create a service that runs it in a shell. I then used the System Preferences to configure a hotkey (in my case <opt><cmd>E) that will invoke the service.

The script will take the currently opened note and open a vim terminal tab. Every time you save your file, Evernote will be updated. When you exit this vim session, the script will stop listening.

I lifted a couple stylesheets to style your note. Setting '$style' to ':unstyled' will write lighter notes.

Use this script at your own risk, although the most serious risk I can think of is that you will get really ugly notes. I hope to fix most of the quirks down the road and add support for more advanced things such as images and diagrams.

-Chris.
