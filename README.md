## po4gitbook

### NOTE

* This project is just working state.
* I didn't yet implement file copy action and LANGS.md file generation process.

### Overview

This tool is translation tool to make translation catalog into the Portable Object Template(pot) format,
and compile po format into the separate markdown(text) file. each work can be done automatically.

### Create catalog by extracting message from markdown files

po4gitbook message extraction works in the following step.

1. Aggregate a list of markdown documentation by recursively traversal sub-directory, and save a list into the po/POTFILES.in
2. Create pot files per-directory. Message ID catalog for root is saved as doc-root.pot, and another Message ID catalog is named as each directory's own.

Every user can translate using pot file. for the convenience, I recommend to use po editor such as [PoEdit](http://www.poedit.net), [GTranslator](https://wiki.gnome.org/Apps/Gtranslator), [Lokalize](https://userbase.kde.org/Lokalize), and so on as you want to use.

Run following command if you want to prepare to translate

```
$ ./update.sh
```

This command automatically updates pot plus all of po file.

### Translate

Please note that,

* First of all, You need to copy pot to po(like overview.po → overview.ja.po)
* You should write your credit(# FULL NAME &lt;YOU@COMPANY.COM&gt;, YEAR1, YEAR2-YEAR3, YEAR4.) onto the header description
* You don't need to leave Copyright (C) ... line.
* You may leave a license notice as "# This file is distributed under the same license as the gitbook package."
* You should write Language-team URL. if it doesn't exist, write your name and e-mail alternatively.

### Preparate to compile

Before you generate translation result, you need to create po/LINGUAS onto the gitbook(if it doesn't exist).

```
$ touch po/LINGUAS
```

and insert your ISO language code, such as 

```
ar az ca de es fi fr it ja ko nl ru zh_CN
```

and many one as you want to create.

If there is no specified language code related on your language, po4gitbook will not generate result into your language. so, please double check before you try to "Compile".

### Compile po

After you complete to translate to your language per one catalog(directory) unit, you can generate translation result into your language by running compile.sh command

```
$ ./compile.sh
```

Translation will be generated by compiling po file into the locale/LANG/blabla.md.

