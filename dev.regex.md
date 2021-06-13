# Warren Shea's Notes for Regex
**Version**: 20210612

## Find everything between `class="` and `"`

Find: `(?s)class="*\K.*?(?=")`
Replace:
Results: `class=""`

## Find everything between  ` (text)=""`

Find: `([a-zA-Z\d\- ]+)=""`
Find: `([a-zA-Z\d\- ]+)="`
REPLACE: `$1="`

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