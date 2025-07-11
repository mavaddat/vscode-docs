---
ContentId: DE4EAE2F-4542-4363-BB74-BE47D64141E6
DateApproved: 07/09/2025
MetaDescription: Learn about the basic editing features of Visual Studio Code. Search, multiple selection, code formatting.
MetaSocialImage: images/codebasics/code-basics-social.png
---
# Basic editing

Visual Studio Code is an editor first and foremost, and includes the features you need for highly productive source code editing. This topic takes you through the basics of the editor and helps you get moving with your code.

## Keyboard shortcuts

Being able to keep your hands on the keyboard when writing code is crucial for high productivity. VS Code has a rich set of default keyboard shortcuts as well as allowing you to customize them.

* [Keyboard Shortcuts Reference](/docs/configure/keybindings.md#keyboard-shortcuts-reference) - Learn the most commonly used and popular keyboard shortcuts by downloading the reference sheet.
* [Install a Keymap extension](/docs/configure/keybindings.md#keymap-extensions) - Use the keyboard shortcuts of your old editor (such as Sublime Text, Atom, and Vim) in VS Code by installing a Keymap extension.
* [Customize Keyboard Shortcuts](/docs/configure/keybindings.md#keyboard-shortcuts-editor) - Change the default keyboard shortcuts to fit your style.

## Multiple selections (multi-cursor)

VS Code supports multiple cursors for fast simultaneous edits. You can add secondary cursors (rendered thinner) with `kbstyle(Alt+Click)`. Each cursor operates independently based on the context it sits in. A common way to add more cursors is with `kb(editor.action.insertCursorBelow)` or `kb(editor.action.insertCursorAbove)` that insert cursors below or above.

> [!NOTE]
> Your graphics card driver (for example NVIDIA) might overwrite these default shortcuts.

![Multi-cursor](images/codebasics/multicursor.gif)

`kb(editor.action.addSelectionToNextFindMatch)` selects the word at the cursor, or the next occurrence of the current selection.

![Multi-cursor-next-word](images/codebasics/multicursor-word.gif)

> [!TIP]
> You can also add more cursors with `kb(editor.action.selectHighlights)`, which will add a selection at each occurrence of the current selected text.

### Multi-cursor modifier

If you'd like to change the modifier key for applying multiple cursors to `kbstyle(Cmd+Click)` on macOS and `kbstyle(Ctrl+Click)` on Windows and Linux, you can do so with the `setting(editor.multiCursorModifier)` [setting](/docs/configure/settings.md). This lets users coming from other editors such as Sublime Text or Atom continue to use the keyboard modifier they are familiar with.

The setting can be set to:

* `ctrlCmd` - Maps to `kbstyle(Ctrl)` on Windows and `kbstyle(Cmd)` on macOS.
* `alt` - The existing default `kbstyle(Alt)`.

There's also a menu item **Selection** > **Switch to Ctrl+Click for Multi-Cursor** or **Selection** > **Switch to Alt+Click for Multi-Cursor** to quickly toggle this setting.

The **Go to Definition** and **Open Link** gestures will also respect this setting and adapt such that they do not conflict. For example, when the setting is `ctrlCmd`, multiple cursors can be added with `kbstyle(Ctrl/Cmd+Click)`, and opening links or going to definition can be invoked with `kbstyle(Alt+Click)`.

### Shrink/expand selection

Quickly shrink or expand the current selection. Trigger it with `kb(editor.action.smartSelect.shrink)` and `kb(editor.action.smartSelect.expand)`.

Here's an example of expanding the selection with `kb(editor.action.smartSelect.expand)`:

![Expand selection](images/codebasics/expandselection.gif)

## Column (box) selection

Place the cursor in one corner and then hold `kbstyle(Shift+Alt)` while dragging to the opposite corner:

![Column text selection](images/codebasics/column-select.gif)

> [!NOTE]
> This changes to `kbstyle(Shift+Ctrl/Cmd)` when using `kbstyle(Ctrl/Cmd)` as [multi-cursor modifier](#multi-cursor-modifier).

There are also default keyboard shortcuts for column selection on macOS and Windows, but not on Linux.

Key|Command|Command ID
---|-------|----------
`kb(cursorColumnSelectDown)`|Column Select Down|`cursorColumnSelectDown`
`kb(cursorColumnSelectUp)`|Column Select Up|`cursorColumnSelectUp`
`kb(cursorColumnSelectLeft)`|Column Select Left|`cursorColumnSelectLeft`
`kb(cursorColumnSelectRight)`|Column Select Right|`cursorColumnSelectRight`
`kb(cursorColumnSelectPageDown)`|Column Select Page Down|`cursorColumnSelectPageDown`
`kb(cursorColumnSelectPageUp)`|Column Select Page Up|`cursorColumnSelectPageUp`

You can [edit](/docs/configure/keybindings.md) your `keybindings.json` to bind them to something more familiar if you want.

### Column Selection mode

The user setting **Editor: Column Selection** controls this feature. Once this mode is entered, as indicated in the Status bar, the mouse gestures and the arrow keys will create a column selection by default. This global toggle is also accessible via the **Selection** > **Column Selection Mode** menu item. In addition, one can also disable Column Selection mode from the Status bar.

## Save / Auto Save

By default, VS Code requires an explicit action to save your changes to disk, `kb(workbench.action.files.save)`.

However, it's easy to turn on `Auto Save`, which will save your changes after a configured delay or when focus leaves the editor. With this option turned on, there is no need to explicitly save the file. The easiest way to turn on `Auto Save` is with the **File** > **Auto Save** toggle that turns on and off save after a delay.

For more control over `Auto Save`, open User or Workspace [settings](/docs/configure/settings.md) and find the associated settings:

* `setting(files.autoSave)`: Can have the values:
  * `off` - to disable auto save.
  * `afterDelay` - to save files after a configured delay (default 1000 ms).
  * `onFocusChange` - to save files when focus moves out of the editor of the dirty file.
  * `onWindowChange` - to save files when the focus moves out of the VS Code window.
* `setting(files.autoSaveDelay)`: Configures the delay in milliseconds when `setting(files.autoSave)` is configured to `afterDelay`. The default is 1000 ms.

If you want to customize the `Auto Save` functionality for specific languages or file types, you can do so from the `settings.json` file by adding language-specific rules.

For example, to disable `Auto Save` for LaTeX files:

```json
    "[latex]": {
        "files.autoSave": "off",
    },
```

## Hot Exit

By default, VS Code remembers unsaved changes to files when you exit. Hot exit is triggered when the application is closed via **File** > **Exit** (**Code** > **Quit** on macOS) or when the last window is closed.

You can configure hot exit by setting `setting(files.hotExit)` to the following values:

* `"off"`: Disable hot exit.
* `"onExit"`: Hot exit will be triggered when the application is closed, that is when the last window is closed on Windows/Linux or when the `workbench.action.quit` command is triggered (from the **Command Palette**, keyboard shortcut or menu). All windows without folders opened will be restored upon next launch.
* `"onExitAndWindowClose"`: Hot exit will be triggered when the application is closed, that is when the last window is closed on Windows/Linux or when the `workbench.action.quit` command is triggered (from the **Command Palette**, keyboard shortcut or menu), and also for any window with a folder opened regardless of whether it is the last window. All windows without folders opened will be restored upon next launch. To restore folder windows as they were before shutdown, set `setting(window.restoreWindows)` to `all`.

If something goes wrong with hot exit, all backups are stored in the following folders for standard install locations:

* **Windows** `%APPDATA%\Code\Backups`
* **macOS** `$HOME/Library/Application Support/Code/Backups`
* **Linux** `$HOME/.config/Code/Backups`

## Find and replace

VS Code allows you to quickly find and replace text in the currently opened file. Press `kb(actions.find)` to open the Find control in the editor and type the search string. The search results are highlighted in the editor, overview ruler, and minimap.

VS Code immediately starts searching as you type. To only start searching when you press `kbstyle(Enter)`, clear the `setting(editor.find.findOnType)` setting.

If there are multiple matches in the current file, press `kb(editor.action.nextMatchFindAction)` to go to the next result or `kb(editor.action.previousMatchFindAction)` to go to the previous result while the find input box has focus.

By default, VS Code saves the history of your find and replace queries for a workspace and restores it across restarts. You can configure this behavior with the `setting(editor.find.history)` and `setting(editor.find.replaceHistory)` settings. Set the value to `never` to disable saving the history.

### Seed search string from selection

When the Find control is opened, it will automatically populate the selected text in the editor into the find input box. If the selection is empty, the word under the cursor will be inserted into the input box instead.

![Seed Search String From Selection](images/codebasics/seed-search-string-from-selection.gif)

This feature can be turned off by setting `setting(editor.find.seedSearchStringFromSelection)` to `"never"`.

### Find in selection

By default, the find operations are run on the entire file in the editor. To limit the search to the text selection, select the **Find in Selection** icon on the Find control or press `kb(toggleFindInSelection)`.

![Find In Selection](images/codebasics/find-in-selection.gif)

If you want it to be the default behavior of the Find control, you can set `setting(editor.find.autoFindInSelection)` to `always`, or to `multiline`, if you want it to be run on selected text only when multiple lines of content are selected.

### Advanced find and replace options

For more advanced scenarios, the Find and Replace control has the following options:

* Find control:

  * Match Case
  * Match Whole Word
  * Regular Expression

* Replace control:

  * Preserve case

![Advanced Find and Replace Options](images/codebasics/search-replace-advanced-options.png)

### Multiline support and Find control resizing

You can search multiple line text by pasting the text into the Find input box and Replace input box. Pressing `kbstyle(Ctrl+Enter)` inserts a new line in the input box.

![Multiple Line Support](images/codebasics/multiple-line-support.gif)

While searching long text, the default size of Find control might be too small. You can drag the left sash to enlarge the Find control or double click the left sash to maximize it or shrink it to its default size.

![Resize Find control](images/codebasics/resize-find-widget.gif)

## Search across files

VS Code allows you to quickly search over all files in the currently opened folder.  Press `kb(workbench.view.search)` and enter your search term. Search results are grouped into files containing the search term, with an indication of the hits in each file and its location. Expand a file to see a preview of all of the hits within that file. Then single-click on one of the hits to view it in the editor.

![A simple text search across files](images/codebasics/search.png)

> [!TIP]
> VS Code also supports regular expression searching in the search box.

You can configure advanced search options by selecting the ellipsis (**Toggle Search Details**) below the search box on the right (or press `kb(workbench.action.search.toggleQueryDetails)`). This shows additional fields to configure the search.

> [!TIP]
> You can use Quick Search to quickly find text across all files in the currently opened folder. Open the Command Palette (`kb(workbench.action.showCommands)`) and enter the **Search: Quick Search** command.

### Advanced search options

![Advanced search options](images/codebasics/searchadvanced.png)

In the two input boxes below the search box, you can enter patterns to include or exclude from the search. If you enter `example`, that will match every folder and file named `example` in the workspace. If you enter `./example`, that will match the folder `example/` at the top level of your workspace. Use `,` to separate multiple patterns. Paths must use forward slashes. You can also use [glob pattern](/docs/editor/glob-patterns.md) syntax, for example:

* `*` to match zero or more characters in a path segment
* `?` to match on one character in a path segment
* `**` to match any number of path segments, including none
* `{}` to group conditions (for example `{**/*.html,**/*.txt}` matches all HTML and text files)
* `[]` to **declare** a range of characters to match (`example.[0-9]` to match on `example.0`, `example.1`, …)
* `[!...]` to negate a range of characters to match (`example.[!0-9]` to match on `example.a`, `example.b`, but not `example.0`)

VS Code excludes some folders by default to reduce the number of search results that you are not interested in (for example: `node_modules`). Open [settings](/docs/configure/settings.md) to change these rules under the `setting(files.exclude)` and `setting(search.exclude)` section.

Note that glob patterns in the Search view work differently than in settings such as `setting(files.exclude)` and `setting(search.exclude)`. In the settings, you must use `**/example` to match a folder named `example` in subfolder `folder1/example` in your workspace. In the Search view, the `**` prefix is assumed. The glob patterns in these settings are always evaluated relative to the path of the workspace folder.

Also note the **Use Exclude Settings and Ignore Files** toggle button in the **files to exclude** box. The toggle determines whether to exclude files that are ignored by your `.gitignore` files and/or matched by your `setting(files.exclude)` and `setting(search.exclude)` settings.

> [!TIP]
> From the Explorer, you can right-click on a folder and select **Find in Folder** to search inside a folder only.

### Search and replace

You can also Search and Replace across files. Expand the Search widget to display the Replace text box.

![search and replace](images/codebasics/global-search-replace.png)

When you type text into the Replace text box, you will see a diff display of the pending changes. You can replace across all files from the Replace text box, replace all in one file or replace a single change.

![search and replace diff view](images/codebasics/search-replace-example.png)

> [!TIP]
> You can quickly reuse a previous search term by using `kb(history.showNext)` and `kb(history.showPrevious)` to navigate through your search term history.

### Case changing in regex replace

VS Code supports changing the case of regex matching groups while doing Search and Replace in the editor or globally. This is done with the modifiers `\u\U\l\L`, where `\u` and `\l` will upper/lowercase a single character, and `\U` and `\L` will upper/lowercase the rest of the matching group.

Example:

![Changing case while doing find and replace](images/codebasics/case-change-replace.gif)

The modifiers can also be stacked - for example, `\u\u\u$1` will uppercase the first three characters of the group, or `\l\U$1` will lowercase the first character, and uppercase the rest. The capture group is referenced by `$n` in the replacement string, where `n` is the order of the capture group.

## Search Editor

Search Editors let you view workspace search results in a full-sized editor, complete with syntax highlighting and optional lines of surrounding context.

Below is a search for the word 'SearchEditor' with two lines of text before and after the match for context:

![Search Editor overview](images/codebasics/search-editor-overview.png)

The **Open Search Editor** command opens an existing Search Editor if one exists, or to otherwise create a new one. The **New Search Editor** command will always create a new Search Editor.

In the Search Editor, results can be navigated to using **Go to Definition** actions, such as `kb(editor.action.revealDefinition)` to open the source location in the current editor group, or `kb(editor.action.revealDefinitionAside)` to open the location in an editor to the side. Additionally, you can configure the behavior for single-clicking or double-clicking a search result with the `setting(search.searchEditor.singleClickBehaviour)` and `setting(search.searchEditor.doubleClickBehaviour)` settings. For example, to open a peek definition window or to open the source location.

You can also use the **Open New Search Editor** button at the top of the Search view, and can copy your existing results from a Search view over to a Search Editor with the **Open in editor** link at the top of the results tree, or the **Search Editor: Open Results in Editor** command.

![Search Editor Button](images/codebasics/search-editor-button.png)

The Search Editor above was opened by selecting the **Open New Search Editor** button (third button) on the top of the Search view.

### Search Editor commands and arguments

* `search.action.openNewEditor` - Opens the Search Editor in a new tab.
* `search.action.openInEditor` - Copy the current Search results into a new Search Editor.
* `search.action.openNewEditorToSide` - Opens the Search Editor in a new window next to the window you currently have opened.

There are two arguments that you can pass to the Search Editor commands (`search.action.openNewEditor`, `search.action.openNewEditorToSide`) to allow keyboard shortcuts to configure how a new Search Editor should behave:

* `triggerSearch` - Whether a search be automatically run when a Search Editor is opened. Default is true.
* `focusResults` - Whether to put focus in the results of a search or the query input. Default is true.

For example, the following keyboard shortcut runs the search when the Search Editor is opened but leaves the focus in the search query control.

```json
{
    "key": "ctrl+o",
    "command": "search.action.openNewEditor",
    "args": { "query": "VS Code", "triggerSearch":true, "focusResults": false }
}
```

### Search Editor context default

The `setting(search.searchEditor.defaultNumberOfContextLines)` setting has a default value of 1, meaning one context line will be shown before and after each result line in the Search Editor.

### Reuse last Search Editor configuration

The `setting(search.searchEditor.reusePriorSearchConfiguration)` setting (default is `false`) lets you reuse the last active Search Editor's configuration when creating a new Search Editor.

## IntelliSense

We'll always offer word completion, but for the rich [languages](/docs/languages/overview.md), such as JavaScript, JSON, HTML, CSS, SCSS, Less, C# and TypeScript, we offer a true IntelliSense experience. If a language service knows possible completions, the IntelliSense suggestions will pop up as you type. You can always manually trigger it with `kb(editor.action.triggerSuggest)`.  By default, `kbstyle(Tab)` or `kbstyle(Enter)` are the accept keyboard triggers but you can also [customize these keyboard shortcuts](/docs/configure/keybindings.md).

> [!TIP]
>  The suggestions filtering supports CamelCase, so you can type the letters which are upper cased in a method name to limit the suggestions. For example, "cra" will quickly bring up "createApplication".

> [!TIP]
> IntelliSense suggestions can be configured via the `setting(editor.quickSuggestions)` and `setting(editor.suggestOnTriggerCharacters)` [settings](/docs/configure/settings.md).

JavaScript and TypeScript developers can take advantage of the [npmjs](https://www.npmjs.com) type declaration (typings) file repository to get IntelliSense for common JavaScript libraries (Node.js, React, Angular). You can find a good explanation on using type declaration files in the [JavaScript language](/docs/languages/javascript.md#intellisense) topic and the [Node.js](/docs/nodejs/nodejs-tutorial.md) tutorial.

Learn more in the [IntelliSense document](/docs/editing/intellisense.md).

## Formatting

VS Code has great support for source code formatting. The editor has two explicit format actions:

* **Format Document** (`kb(editor.action.formatDocument)`) - Format the entire active file.
* **Format Selection** (`kb(editor.action.formatSelection)`) - Format the selected text.

You can invoke these from the **Command Palette** (`kb(workbench.action.showCommands)`) or the editor context menu.

VS Code has default formatters for JavaScript, TypeScript, JSON, HTML, and CSS. Each language has specific formatting options (for example, `setting(html.format.indentInnerHtml)`) which you can tune to your preference in your user or workspace [settings](/docs/configure/settings.md). You can also disable the default language formatter if you have another extension installed that provides formatting for the same language.

```json
"html.format.enable": false
```

Along with manually invoking code formatting, you can also trigger formatting based on user gestures such as typing, saving or pasting. These are off by default but you can enable these behaviors through the following [settings](/docs/configure/settings.md):

* `setting(editor.formatOnType)` - Format the line after typing.
* `setting(editor.formatOnSave)` - Format a file on save.
* `setting(editor.formatOnPaste)` - Format the pasted content.

> [!NOTE]
> Not all formatters support format on paste as to do so they must support formatting a selection or range of text.

In addition to the default formatters, you can find extensions on the Marketplace to support other languages or formatting tools. There is a `Formatters` category so you can easily search and find [formatting extensions](https://marketplace.visualstudio.com/search?target=VSCode&category=Formatters&sortBy=Installs). In the **Extensions** view search box, type 'formatters' or 'category:formatters' to see a filtered list of extensions within VS Code.

## Folding

You can fold regions of source code using the folding icons on the gutter between line numbers and line start. Move the mouse over the gutter and click to fold and unfold regions. Use `kbstyle(Shift + Click)` on the folding icon to fold or unfold the region and all regions inside.

![Folding](images/codebasics/folding.png)

You can also use the following actions:

* Fold (`kb(editor.fold)`) folds the innermost uncollapsed region at the cursor.
* Unfold (`kb(editor.unfold)`) unfolds the collapsed region at the cursor.
* Toggle Fold (`kb(editor.toggleFold)`) folds or unfolds the region at the cursor.
* Fold Recursively (`kb(editor.foldRecursively)`) folds the innermost uncollapsed region at the cursor and all regions inside that region.
* Unfold Recursively (`kb(editor.unfoldRecursively)`) unfolds the region at the cursor and all regions inside that region.
* Fold All (`kb(editor.foldAll)`) folds all regions in the editor.
* Unfold All (`kb(editor.unfoldAll)`) unfolds all regions in the editor.
* Fold Level X (`kb(editor.foldLevel2)` for level 2) folds all regions of level X, except the region at the current cursor position.
* Fold All Block Comments (`kb(editor.foldAllBlockComments)`) folds all regions that start with a block comment token.

Folding regions are by default evaluated based on the indentation of lines. A folding region starts when a line has a smaller indent than one or more following lines, and ends when there is a line with the same or smaller indent.

Folding regions can also be computed based on syntax tokens of the editor's configured language. The following languages already provide syntax aware folding: Markdown, HTML, CSS, LESS, SCSS, and JSON.

If you prefer to switch back to indentation-based folding for one (or all) of the languages above, use:

```json
  "[html]": {
    "editor.foldingStrategy": "indentation"
  },
```

Regions can also be defined by markers defined by each language. The following languages currently have markers defined:

Language|Start region|End region
--------|------------|----------
Bat|`::#region` or `REM #region`|`::#endregion` or `REM #endregion`
C#|`#region`|`#endregion`
C/C++|`#pragma region`|`#pragma endregion`
CSS/Less/SCSS|`/*#region*/`|`/*#endregion*/`
Coffeescript|`#region`|`#endregion`
F#|`//#region` or `(#region)`|`//#endregion` or `(#endregion)`
Java|`//#region` or `//<editor-fold>`|`//#endregion` or `//</editor-fold>`
Markdown|`<!-- #region -->`|`<!-- #endregion -->`
Perl5|`#region` or `=pod`|`#endregion` or `=cut`
PHP|`#region`|`#endregion`
PowerShell|`#region`|`#endregion`
Python|`#region` or `# region`|`#endregion` or `# endregion`
TypeScript/JavaScript|`//#region` |`//#endregion`
Visual Basic|`#Region`|`#End Region`

To fold and unfold only the regions defined by markers use:

* Fold Marker Regions (`kb(editor.foldAllMarkerRegions)`) folds all marker regions.
* Unfold Marker Regions (`kb(editor.unfoldAllMarkerRegions)`) unfolds all marker regions.

### Fold selection

The command **Create Manual Folding Ranges from Selection** (`kb(editor.createFoldingRangeFromSelection)`) creates a folding range from the currently selected lines and collapses it. That range is called a **manual** folding range that goes on top of the ranges computed by folding providers.

Manual folding ranges can be removed with the command **Remove Manual Folding Ranges** (`kb(editor.removeManualFoldingRanges)`).

Manual folding ranges are especially useful for cases when there isn't programming language support for folding.

## Indentation

VS Code lets you control text indentation and whether you'd like to use spaces or tab stops. By default, VS Code inserts spaces and uses 4 spaces per `kbstyle(Tab)` key. If you'd like to use another default, you can modify the `setting(editor.insertSpaces)` and `setting(editor.tabSize)` [settings](/docs/configure/settings.md).

```json
    "editor.insertSpaces": true,
    "editor.tabSize": 4,
```

### Auto-detection

VS Code analyzes your open file and determines the indentation used in the document. The auto-detected indentation overrides your default indentation settings. The detected setting is displayed on the right side of the Status Bar:

![auto detect indentation](images/codebasics/indentation-detection.png)

You can click on the Status Bar indentation display to bring up a dropdown with indentation commands allowing you to change the default settings for the open file or convert between tab stops and spaces.

![indentation commands](images/codebasics/indentation-commands.png)

> [!NOTE]
> VS Code auto-detection checks for indentations of 2, 4, 6 or 8 spaces. If your file uses a different number of spaces, the indentation may not be correctly detected. For example, if your convention is to indent with 3 spaces, you may want to turn off `setting(editor.detectIndentation)` and explicitly set the tab size to 3.

```json
    "editor.detectIndentation": false,
    "editor.tabSize": 3,
```

## File encoding support

Set the file encoding globally or per workspace by using the `setting(files.encoding)` setting in **User Settings** or **Workspace Settings**.

![files.encoding setting](images/codebasics/filesencodingsetting.png)

You can view the file encoding in the status bar.

![Encoding in status bar](images/codebasics/fileencoding.png)

Click on the encoding button in the status bar to reopen or save the active file with a different encoding.

![Reopen or save with a different encoding](images/codebasics/encodingclicked.png)

Then choose an encoding.

![Select an encoding](images/codebasics/encodingselection.png)

## Overtype mode

Prior to release 1.96, VS Code only supported *insert* mode, where characters are inserted at the cursor position, unless you installed the Vim [keymap extension](/docs/configure/keybindings.md#keymap-extensions).

As of release 1.96, VS Code supports *overtype* mode, which lets you overwrite existing characters instead of inserting characters at the cursor position. By default, overtype mode is off.

To switch between insert and overtype mode, run the **Toggle Overtype/Insert Mode** command in the Command Palette or press (`kb(editor.action.toggleOvertypeInsertMode)`). When you're in overtype mode, a Status Bar indicator shows `OVR`.

You can change the cursor style for overtype mode by configuring the `setting(editor.overtypeCursorStyle)` setting.

Use the `setting(editor.overtypeOnPaste)` setting to overwrite text when pasting. You need to be in overtype mode for this setting to take effect.

## Compare files

VS Code supports several ways to compare the content of the current file or of any two files.

When you have an active file open in the editor, you have the following compare options:

* **Compare with a workspace file**: in the Command Palette, select **File: Compare Active File With...**, and then choose another file to compare with.
* **Compare with clipboard**: in the Command Palette, select **File: Compare Active File with Clipboard** (`kb(workbench.files.action.compareWithClipboard)`) to compare the current file with the clipboard content.
* **Compare with saved**: in the Command Palette, select **File: Compare Active File with Saved** (`kb(workbench.files.action.compareWithSaved)`) to compare the current file with the last saved version.

To compare any two files:

* Right-click on a file in the Explorer view and select **Select for Compare**. Then, right-click on a second file and select **Compare with Selected**.
* To start a comparison between two empty editor windows, select **File: Compare New Untitled Text Files** from the Command Palette.

> [!TIP]
> You can start VS Code from the command line with the `--diff` option to compare two files. Learn more about the [VS Code command line interface](/docs/configure/command-line.md#core-cli-options).

## Next steps

You've covered the basic user interface - there is a lot more to VS Code.  Read on to find out about:

* [Intro Video - Setup and Basics](/docs/introvideos/basics.md) - Watch a tutorial on the basics of VS Code.
* [User/Workspace Settings](/docs/configure/settings.md) - Learn how to configure VS Code to your preferences through user and workspace settings.
* [Code Navigation](/docs/editing/editingevolved.md) - Peek and Goto Definition, and more.
* [Integrated Terminal](/docs/terminal/basics.md) - Learn about the integrated terminal for quickly performing command-line tasks from within VS Code.
* [IntelliSense](/docs/editing/intellisense.md) - VS Code brings smart code completions.
* [Debugging](/docs/debugtest/debugging.md) - This is where VS Code really shines.

## Common questions

### Is it possible to globally search and replace?

Yes, expand the Search view text box to include a replace text field. You can search and replace across all the files in your workspace. Note that if you did not open VS Code on a folder, the search will only run on the currently open files.

![global search and replace](images/codebasics/global-search-replace.png)

### How do I turn on word wrap?

You can control word wrap through the `setting(editor.wordWrap)` [setting](/docs/configure/settings.md). By default, `setting(editor.wordWrap)` is `off` but if you set to it to `on`, text will wrap on the editor's viewport width.

```json
    "editor.wordWrap": "on"
```

You can toggle word wrap for the VS Code session with `kb(editor.action.toggleWordWrap)`.

You can also add vertical column rulers to the editor with the `setting(editor.rulers)` setting, which takes an array of column character positions where you'd like vertical rulers.

As in other editors, commands such as **Cut** and **Copy** apply to the whole wrapped line. Triple-click selects the whole wrapped line. Pressing `kbstyle(Home)` twice moves the cursor to the very beginning of the line. Pressing `kbstyle(End)` twice moves the cursor to the very end of the line.

### How can I avoid placing extra cursors in word wrapped lines?

If you'd like to ignore line wraps when adding cursors above or below your current selection, you can pass in `{ "logicalLine": true }` to `args` on the keyboard shortcut like this:

```json
{
  "key": "shift+alt+down",
  "command": "editor.action.insertCursorBelow",
  "when": "textInputFocus",
  "args": { "logicalLine": true },
},
{
  "key": "shift+alt+up",
  "command": "editor.action.insertCursorAbove",
  "when": "textInputFocus",
  "args": { "logicalLine": true },
},
```
