BASIC! Operation
================

<!-- toc -->

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

#### Run {#menus-run}

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

- COLOR SCHEME

    Sets the color scheme of the screens. The schemes are identified by their appearance with the default colors. Choose Black text on a White background, White text on a Black background or White text on a Blue background.

- CUSTOM COLORS

    Check the box to override the Color Scheme setting, allowing you to set your own colors. You can set the Text (foreground) Color, the Background Color, the Line Color, and the Highlight Color. Each color is specified as a single number with 16 hexadecimal digits: four fields of four digits each for Alpha (opacity), Red, Green, and Blue components.

##### CONSOLE SETTINGS

Opens a sub-menu with options for settings of the Console and various others screens in BASIC!

- FONT SIZE

    Sets the font size (Small, Medium, or Large) to be used with the various screens in BASIC!.

- TYPEFACE

    Choose the typeface to be used on the Output Console and some other screens:
	Monospace, Sans Serif, or Serif.

- CONSOLE MENU

    Check the box if the Menu should be visible in the Output Console and TGet screen.

- CONSOLE LINES

    Check the box if the text lines in the Output Console should be underlined.

- EMPTY CONSOLE COLOR

    Choose the background color of the part of the Output Console that has not yet been written. It can match the background color of the text or the color of the lines separating text lines.
	
	This setting also applies to the `Select` (but not `Dialog.select`) command.

##### EDITOR SETTINGS

Opens a sub-menu with options for setting properties and features of the Program Editor.

- EDITOR LINES

    Check the box if the text lines in the Editor should be underlined.

- EDITOR LINE WRAP

    Check the box if long text lines in the Editor should wrap at the edge of the screen. If unchecked, long lines are not wrapped, and the Editor screen may be scrolled horizontally.

- EDITOR AUTOINDENT

    Check the box if you want the Editor to do auto indentation. Enabling auto indentation also enables the formatting of a line that ends with the "#" character.
	
	Some devices are not able to do auto indenting properly. In some of those devices the AutoIndent feature may cause the Editor to be unusable. If that happens, turn off AutoIndent.

##### MENU ITEMS ON ACTION BAR

Opens a sub-menu with options for moving some of the Editor menu items to the Action Bar, if there is room for them there. You can select as many as you like, but the number of items moved depends on the device and orientation. These options have no effect on Android devices before Honeycomb (3.0).

- RUN ON ACTION BAR

    If checked, Android will attempt to move the RUN item from the Editor Menu to the Action Bar.

- LOAD ON ACTION BAR

    If checked, Android will attempt to move the LOAD item from the Editor Menu to the Action Bar.

- SAVE ON ACTION BAR

    If checked, Android will attempt to move the SAVE item from the Editor Menu to the Action Bar.

- EXIT ON ACTION BAR

    If checked, Android will attempt to move the EXIT item from the Editor Menu to the Action Bar.

##### SCREEN ORIENTATION

Choose to allow the Sensors to determine the orientation of the screens or to set a fixed orientation without regard to the Sensors.

Note: The reverse orientations apply to Android 2.3 or newer.

##### GRAPHIC ACCELERATION

Check this box to enable GPU-assisted graphics acceleration on devices since 3.0 (Honeycomb) that support it. It is disabled by default. If you enable this option, test your program carefully. Hardware acceleration can make some of BASIC!’s graphical operations fail.

##### BASE DRIVE

Some Android devices have several external storage devices (and some have no physical external storage devices). BASIC! will use the system-suggested device as its base drive. The base drive is the device where the BASIC! "rfo-basic" directory (base directory) is located. The base directory is where BASIC!’s programs and data are stored. (See "Paths Explained", later in this manual.)

If your device does have more than one external storage device they will be listed here. If your device has no external storage devices, your one and only choice will be "No external storage". Tap the device you want to use as the base drive and press the BACK key. You will then be given the choice of either immediately restarting BASIC! with the new base drive or waiting and doing the restart yourself.

In this manual, <pref base drive> means the base drive you selected when you set the Base Drive here. In many devices, the system-suggested drive is "/sdcard".

Note: If you have created a Launcher Shortcut (see Appendix C) with files in one base directory but try to execute that shortcut while using a different base directory, the shortcut will fail to execute. You will get an error message.

#### Commands

The Commands command presents the list of the BASIC! commands and functions as copied from Appendix A of this document.

Tapping an alpha key will cause the command list to scroll to commands that start with that character. There will be no scrolling if there is no command that starts with that character.

Note: You can hide the virtual keyboard with the BACK key. If you do that, you will not be able to get it back until you invoke the `Commands` option again.

Tapping on a particular command causes that command to be copied to the clipboard (not including the page number) and returning to the Editor. You can then paste the command into your BASIC! program.

#### About

The `About` option displays the Bintray page for the release of BASIC! that corresponds to the release of the BASIC! that you are using. Make sure that you have a connection to the Internet before selecting `About`.

#### Exit

The only way to cleanly exit BASIC! is to use the `Exit` option.

Pressing the HOME key while in BASIC! leaves BASIC! in exactly the same state it was in when the HOME key was tapped. If a program was running, it will still be running when BASIC! is re-entered. If you were in the process of deleting, the Delete screen will be shown when BASIC! is re-entered.

## Run

Selecting `Run` from the Editor’s menu starts the program running. However, if the source in the Editor has been changed, then the Save dialog will be displayed. You may choose to save the changed source or continue without saving.

The BASIC! Output Console will be presented as soon as the program starts to run. You will not see anything on this screen unless one of the following situations occur:

- the program prints something
- the `END` statement is executed
- you are in Echo mode
- there is a run-time error

If the program does not print anything then the only indication you would get that the program has finished is if the program ends with an `End` statement.

If the program does not contain any executable statements then the message, "Nothing to execute" will be displayed.

Tapping the BACK key will stop a running program. Tapping the BACK key when the program run has ended will restart the Editor.

If the program ended with a run-time error, the line where the error occurred will be shown selected in the Editor. If the error occurred in an `INCLUDE` file then the `INCLUDE` statement will be shown selected.

The Editor cursor will remain where it was when the `Run` was started if no run-time error occurred.

### Menu

Pressing the MENU key or touching the Menu icon while a program is running or after the program is stopped will cause the Run Menu to be displayed. (Except when Graphics is running. See the Graphics section for details.)

#### Stop

If a program is running, the `Stop` menu item will be enabled. Tapping `Stop` will stop the running program. `Stop` will not be enabled if a program is not running.

#### Editor

`Editor` will not be enabled if a program is running. If the program has stopped and `Editor` is thus enabled then selecting `Editor` will cause the Editor to be re-entered. You could also use the BACK key to do this.

## Crashes

BASIC! is a very large and complex program that is constantly under development. From time to time, it will crash. Previous versions of BASIC! supported automatic crash reporting. This feature has been temporarily disabled while we work on an implementation that is more compatible with Android versions 4.2 and later. We apologize for the inconvenience.
