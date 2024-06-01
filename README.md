# Explorer Hider

I have, for years, a snippet named `Folder Hider` that does, basically, that:
```css
.nav-file-title[data-path="path/to/file.md"],
.nav-folder-title[data-path="path/to/folder"] {
    display: none;
}
```

Hiding some files I doesn't want to see.

But, managing a snippet have some caveat:
- Renaming the file or the folder will break the snippet, and same for moving
- I need to know the entire path of the file or folder, including insensitive case
- I need to always edit the snippets if I want to hide a new file or folder
- Can't unhide individually (unless using a snippets for each files...)

So, I decided to create a plugin that will manage that for me!

## ⚙️ Usage
### Configuration

The settings allow:
- Choosing between to save the CSS in a snippets (in your `.obsidian/snippets` folder) or directly inject the CSS in the page. Use this if, for example, you want to keep the folder hidden without using the plugin (for example with disabling or uninstalling it).
- Creating new rules, based on a string. Using attribute selector, you can hide multiple file or folder at once. For example, to hide all the files in a folder, you can set `[startswith] <path>`. See [CSS attribute selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors) for more information.

Each attributes correspond to:

| Attribute               | CSS   | Description                                                                                          |
| ----------------------- | ----- | ---------------------------------------------------------------------------------------------------- |
| Exact                   | `=`   | Exact match with the string                                                                          |
| Contains                | `*=`  | Contains the string                                                                                  |
| Ends with               | `$=`  | Ends with the string (suffixe)                                                                       |
| Starts with             | `^=`  | Starts with (prefix)                                                                                 |
| List                    | `~=`  | String is a whitespace separated list of words, one of which match exactly                           |
| Text followed by hiphen | `\|=` | The match can be on exactly the value or can begin with value immediately followed by a hyphen (`-`) |

The setting also display the list of all rules where you can:
- Hide or display individually the files/folders from the explorer or in the bookmarks
- Delete the rules
- For "string" rules, you can edit the attributes and the path. It's not possible for rules added using the file-menu, as they are followed by the path for changes (deleted/renamed/moved).

### Hiding files/folders

To hide a file or a folder, you can right-click on the file/folder in the explorer and select `Hide << name >>`. 

> [!IMPORTANT]
> The menu of bookmarks doesn't allow (yet) to add items. To hide a file from bookmarks, you can use:
> - The setting tab
> - The context menu from the file, if opened in the editor

If `Always hide in bookmark` is enabled, the file/folder will be hidden in the bookmarks too when the command is used from the explorer.

> [!TIP]
> For folder, the rules will be `^=` (starts with) and for files `=` (exact match).
> Also, in the needs to hide the content of a folder, the rules for folders includes `.nav-file-title[^="path"]` and `.nav-folder-title[^="path"]`

### Display all or hide all

Using the "eye" ribbon button you can enable or disable all the rules. 
- Show all will display all the hidden files/folders (ignoring the rules)
- Hide all will restore the older state (based on the hidden parameters).

## 📥 Installation

- [ ] From Obsidian's community plugins
- [x] Using BRAT with `https://github.com/Mara-Li/obsidian-explorer-hider`  
	→ Or use the protocole by pasting it in your web browser: @`obsidian://brat?plugin=https://github.com/Mara-Li/obsidian-explorer-hider`
- [x] From the release page: 
    - Download the latest release
    - Unzip `explorer-hider.zip` in `.obsidian/plugins/` path
    - In Obsidian settings, reload the plugin
    - Enable the plugin


### 🎼 Languages

- [x] English
- [x] French

To add a translation:
1. Fork the repository
2. Add the translation in the `src/i18n/locales` folder with the name of the language (ex: `fr.json`). 
    - You can get your locale language from Obsidian using [obsidian translation](https://github.com/obsidianmd/obsidian-translations) or using the commands (in templater for example) : `<% tp.obsidian.moment.locale() %>`
    - Copy the content of the [`en.json`](./src/i18n/locales/en.json) file in the new file
    - Translate the content
3. Edit `i18n/i18next.ts` :
    - Add `import * as <lang> from "./locales/<lang>.json";`
    - Edit the `ressource` part with adding : `<lang> : {translation: <lang>}`

