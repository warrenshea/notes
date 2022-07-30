# Warren Shea's Notes for Regex
**Version**: 20220729

## Find everything between `class="` and `"`
Find: `(?s)class="*\K.*?(?=")`

Replace:

Results: `class=""`

## Replace property/attribute, e.g. ` [attribute]="`
Find: `([a-zA-Z\d\- ]+)=""`

## Lowercase [attribute]s in code
Search: `[attribute]="([a-zA-Z\d ]+)"` or `[attribute]="(.+)"`

Replace: `[attribute]="\L$1"`

## Find string with dash (-) in it
`[attribute]="([a-zA-Z\d\&\- ]+)"`

## Find string with |mobile at the end
`[attribute]="([a-zA-Z\d ]+)\|mobile"`

## Find any word, digit, or space
`([\w\d\s]+)`

## Find everything between `<svg` and `</svg>`
Find: `(?s)<svg*\K.*?(?=</svg>)`
Replace: `>`
Results: `<svg></svg>`

## RegReplace
* This is a useful sublime extension for running multiple regex expressions on a single file through a keybind
* RegReplace rules (for Mac),
/Users/<user>/Library/Application Support/Sublime Text/Packages/User/reg_replace_rules.sublime-settings
```json
{
    "replacements": {
        "rule1": {
            "find":"",
            "replace":"",
            "greedy": true
        },
        "rule2": {
            "find":"",
            "replace":"",
            "greedy": true
        }
    }
}
```
where
```json
"[\\n\\s]*" = any newline or space
"(string1|string2)" = looking for "string1" or "string2"
"[\\n\\s]*\"(property1|property2)\":[\\n\\s]*{[\\n\\w\"\\:\\,. ]*}," = replace entire json of "property1 = { stuff: stuff, },"

```
* RegReplace keybind (for Mac),
/Users/<user>/Library/Application Support/Sublime Text/Packages/User/Defeault (OSX).sublime-keymap
```json
[
    {
        "keys": ["option+ctrl+r"],
        "command": "reg_replace",
        "args": {"replacements": ["rule1","rule2"]}
    }
]
```