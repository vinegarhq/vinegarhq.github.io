# Translating Vinegar

## Prerequisites

To translate Vinegar, one must already have an environment setup capable of compiling Vinegar as detailed in [Installing from source](../../Installation/guides/source.md).

## Translating a new language

### Generating base POT file

In order to translate Vinegar, you must first generate a template file with all of Vinegar's strings dumped onto it with the following commands (inside the source directory):

```console
find . -name '*.go' | xargs xgettext --language=Go --keyword=_ --keyword=i18n.Local --keyword=Local --keyword=L --keyword=i18n.LocalDomain:2 --keyword=LocalDomain:2 --omit-header -o default.pot
find . -name '*.ui' | xargs xgettext --language=Glade --omit-header --join-existing -o default.pot 
```

This will generate most of the strings necessary for translation in a file called `default.pot`, however due to how Vinegar's settings are internally structured, some strings will need to manually be included, these strings are located in [config.go](https://github.com/vinegarhq/vinegar/blob/master/internal/config/config.go) in the `Studio` and `Config` structs, you will need to manually create `msgid` and `msgstr` field for them like so:

```pot
msgid "Studio's Graphics Mode"
msgstr ""
```

### Defining the language

Move the `default.pot` file inside the `data\po` directory and rename it to `{LOCALE}.po`, replacing `{LOCALE}` with the system locale for your desired language, after that all that remains is to manually translate every `msgid`'s respective `msgstr` field with your translation.

## Updating an existing translation

Translations are located in the `data\po` directory, updating an existing translation is as simple as editing your desired language's .po file in any text editor. The `msgid` field is the original string inside Vinegar's source code and the `msgstr` field is the translated version.

## Testing

To test a translation, you must build Vinegar with the changes you made as detailed in [Installing from source](../../Installation/guides/source.md), set the system language to your desired language and launch Vinegar.

## Contributing

After your translation is complete, open a pull request in Vinegar's repository with your new `.po` file, preferably detailing what you did on the translation, and continue on from there.