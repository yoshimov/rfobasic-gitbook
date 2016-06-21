BASIC! Operation
================

## Permissions

This application requests many permissions, permissions such as sending and receiving SMS messages, making phone calls, record audio, etc. BASIC! does not exercise any of these permissions (except writing to the SD card) on its own. These permissions get exercised by the BASIC! programmer, you. You and only you. You exercise these permissions by means of the programs that you write.

If you write a program that uses the sms.send command then BASIC! will attempt to send an SMS message. BASIC! must have permission to send SMS messages for this command to work. If you never use the sms.send command then BASIC! will never send an SMS message. You are in control.

The source code for BASIC! is available from the BASIC! web site (http://laughton.com/basic/) and the BASIC! GitHub repository (https://github.com/RFO-BASIC/Basic). Please feel free to examine this source code if you have any doubt about the use of these permissions.

## Editor

### Editing the Program

The Editor is where BASIC! programs are written and edited. The operation of the Editor is fairly simple. Tap the screen at the point where you want to edit the program. A cursor will appear. Use the keyboard to edit at the cursor location.

When the Enter key is tapped, the new line will automatically indent to the indent level of the previous line. This feature will not work if the Preference, "Editor AutoIndent," is not checked. This feature also may not work if you are using a software keyboard.

If the program that you are editing has been given a name via Save or Load then that program name will be shown in the title bar.

Some Android devices are shipped with "Settings/Developer Option/Destroy Activities" checked and/or "Settings/Energy/Quick Restart" checked. Both of these setting create problems with loading files into the Editor. It appears as if you have gone through the process of loading the file but nothing appears in the editor. The solution to the problem is to uncheck both of these options. Even better, completely turn off Developer Options unless you know that you have a legitimate development need.

If your Android device does not have a physical keyboard, you will see a virtual keyboard. If you see the virtual keyboard, then you will see different things depending upon the way you are holding the device. If the device is in landscape mode then you will see a dialog box with a chunk of the program in a small text input area. You can scroll the small chunk of text up and down in this area but you will not be able to see very much of the program at any one time. It is probably best not to try to edit a program in landscape mode; hold your device in portrait mode while editing.

On some devices, if you do a long touch on the screen, a dialog box will appear. You can use the selections in the box for selecting, copying, cutting and pasting of text, among other things. Other devices have different procedures for invoking the cut and paste functions.

### Multiple Commands on a Line

More than one BASIC! source code statement may be written on one physical line. Separate commands with a colon character ":".

For example, the following line uses three separate commands to initialize some variables:

```
name$="BASIC!" : ver=1.86 : array.load reviews$[], "Great!", "Wow!", "Fantastic!"
```

Note: two commands, `Sensors.open` and `SQL.update`, use the colon as a sub-parameter separator. If you use multiple-command lines, be careful when using these two commands.

### Line Continuation

A BASIC! source code statement may be written on more than one physical line using the line continuation character "~". If "~" is the last thing on a line, except for optional spaces, tabs, or a '%' comment, the line will be merged with the next line. This behavior is slightly different in the `Array.load` and `List.add` commands; see the descriptions of those commands for details.

Note: this operation is implemented by a pre-processor that merges the source code lines with continuation characters before the source code is executed. If you have a syntax error in the merged line, it will show as one line in the error message, but it will still be multiple lines in the editor. Only the first physical line will be highlighted, regardless of which line the error is in.

For example, the code line:

```
s$ = "The quick brown fox " + verb$ + " over " + count$ + " lazy dogs"
```

could be written as:

```
s$ = "The quick brown fox " +~
	verb$ +     ~       % what the fox did
	" over " +  ~
	count$ +    ~       % how many lazy dogs
	" lazy dogs"
```

### # - Format Line

If a line has the # character at the end of the line, the keywords in that line will be capitalized and the # will be removed.

This feature may not work if you are using a virtual keyboard.

This feature will not work if the Preference option "Editor AutoIndent" is not checked.

### Menus

#### Run

Run the current program.

If the program has been changed since it was last saved, you will be given an opportunity to save the program before the run is started.

If a run-time error occurs then the offending line will be shown as selected in the editor.

#### Load

Load a program file into the editor. The first time you open BASIC! after installing it, if you select `Load` it displays the sample programs in the directory `rfo-basic/source/Sample_Programs`. (See `Paths Explained`, later in this manual.) Otherwise, when you open BASIC! and select `Load` it starts in the default source directory `rfo-basic/source`. Program files must have the extension `.bas`.

BASIC! checks to see if the current program in the Editor has been changed when Load is tapped. You will be offered the opportunity to save the program if it has been changed. If you choose to save the program, `Load` will restart after the save is done.

The "BASIC! Load File" screen shows the path to your current directory followed by sorted lists of the subdirectories and program files in it. Directories are denoted by the `(d)` appended to the name. BASIC! programs are shown with the `.bas` extension. If there are files in the directory that do not have the `.bas` extension, they do not appear in the list.

Tap on a `.bas` file to load it into the Editor.

You can navigate to any directory on your device for which you have read permission.

- Tap on a directory to display its contents.
- Tap on the ".." at the top of list to move up one directory level. The tap has no effect if the current directory is the device root directory "/".

You can exit the `Load` option without loading a program by tapping the BACK key.

BASIC! remembers the path to the directory you are in when you load a program. Next time you select `Load`, it starts in that directory. If you select `Save` or `Save and Run`, the file is saved in the remembered directory (unless it is Sample_Programs).

#### Save

Saves the program currently in the editor.

A dialog box displays the path to the directory where you will save the file and an input area where you can enter the file name. If the current program has a name because it was previously loaded or saved then that name will be in the text input area. Type in the name you want the file saved as and tap `OK`. The extension `.bas` will be added to file name if is not already there.

If you do not enter a file name, BASIC! uses a default filename, `default.bas`.

BASIC! remembers the path to the directory you were in when you last loaded or saved a program. When you `Save`, the file name you type is saved in the remembered directory. If the name you type includes subdirectories, BASIC! remembers the new path. The name you type can include "../". Be careful if you are using a soft keyboard, as it may automatically insert spaces that you don’t want.

You cannot save programs in the sample program directory `source/Sample_Programs`. If you load a program from `source/Sample_Programs`, change it, and `Save` it, the program is saved in source.

You can exit `Save` without saving a file by tapping the BACK key.

#### Clear

Clear the current program in the Editor. You will be offered the opportunity to save the current program if it has been changed.

#### Search

Search for strings in the program being edited. Found strings may be replaced with a different string.

The Search view shows a Text Window with the text from the Editor, a `Search For` field and a `Replace With` field.

If there is a block of text currently selected in the Editor, then that text will be placed into the `Search For` field.

The initial location of the search cursor will be at the start of the text regardless of where the cursor was in the Editor text.

Note: The search ignores case. For example, searching for "basic" will find "BASIC" This is because BASIC! converts the whole program to lower case (except characters within quotes) when the program is run.

##### NEXT BUTTON

Start the search for the string in the `Search For` field. The search is started at the current cursor location. If the string is found then it will be selected in `Text Window`.

If the `Done` button is tapped at this point then the Editor will returned to with the found text selected.

If the `Replace` button is tapped then the selected text will be replaced.

Pressing the `Next` button again will start a new search starting at the end of the selected or replaced text.

If no matching text is found then a "string not found" message is shown. Tapping the `Done` button returns to the Editor with the cursor at the end of the program. Alternatively, you could change the `Search For` text and start a new search.

##### REPLACE BUTTON

If `Next` has found and selected some text then that text is replaced by the contents of the `Replace With` field.

If no text has been found then the message, "Nothing found to replace" will be shown.

##### REPLACE ALL BUTTON

All occurrences of the `Search For` text are replaced with the `Replace With` text. `Replace All` always starts at the start of the text. The last replaced item will be shown selected in the `Text Window`. The number of items replaced will be shown in a message.

##### DONE BUTTON

Returns to the Editor with the changed text. If there is selected text in the `Text Window` then that text will be shown selected in the Editor.

#### BACK KEY

Returns to the Editor with the original text unchanged. All changes made during the Search will be undone. Think of the BACK key as UNDO ALL.

#### Load and Run

Selecting this option is exactly the same as first selecting `Load` and then selecting `Run`. The selected program is loaded into the Editor and is run immediately.

#### Save and Run

Selecting this option is a fast way to save and then run. Any changes you have made are saved, overwriting your file, and your program is run immediately. A brief popup notifies you that your file has been changed. If the program you are editing has no name (not previously loaded or saved), the Editor will ask you what name to use.

#### Format

Format the program currently in the Editor. The keywords are capitalized. Program lines are indented as appropriate for the program structure. Left- and right-double quotation marks (“ and ”) are replaced by simple ASCII quotation marks (").

When copying program text from the Forum or another web site, "non-breaking space" characters, designated `&nbsp` in HTML, may be inserted into the program text. Except when they are enclosed in quoted strings, `Format` converts these characters to simple ASCII spaces.

#### Delete

Delete files and directories. The command should be used for maintaining files and directories that are used in BASIC! but it can also be used to delete any file or directory on the SD card for which you have the required permissions. `Delete` starts in the `rfo-basic` directory.

Tapping `Delete` presents the "BASIC! Delete File" screen. The screen shows the path to your current directory followed by sorted lists of the directories and files in it. Directories are marked with `(d)` appended to the name and appear at the top of the list.

Tapping a file name displays the "Confirm Delete" dialog box. Tap the `Delete` button to delete the file. Tap the `No` button to dismiss the dialog box and not delete the file.

Tapping a directory name displays the contents of the directory. If the directory is empty the "Confirm Delete" dialog box is shown. Tap the `Delete` button to delete the directory. Tap the No button to dismiss the dialog box and not delete the directory.

Tap the ".." at the top of the screen to move up one directory level. Tapping the ".." has no effect if you are in the root directory "/".

Exit `Delete` by tapping the BACK key.

#### Preferences

##### SCREEN COLORS

Opens a sub-menu with options for setting the colors of the various screens in BASIC!

