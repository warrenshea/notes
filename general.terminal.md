# Warren Shea's Notes for Command Prompt / Terminal/iTerm2

## List all files and directories
dir /b /s

## List all files and directories into a file (listing.txt)
dir /b /s > listing.txt

## List all files with directories
find . -name \* -print

## Delete all empty folders
find . -type d -empty -execdir rmdir {} +

## Delete all these filetypes:
del /S /Q *.EXE *.TMP *.PDF *.GIF *.FLV *.MP4 *.MP3 *.JPEG *.JPG *.TTF *.PNG *.ZIP *.ICO *.txt *.GZ *.SWF *.CSS *.webm *.xlsm *.eot *.woff *.psd *.TTF *.xls *.flv *.ogg *.xlsx *.docx *.webp *.lnk *.log *.pptx *.woff2 *.dwt *.htm *.bak *.as *.asx *.eps *.jar *.svg *.fla *.ogv *.csv *.f4v *.wmv *.mov *.avi *.htc *.lck *.doc *.bat *.map *.ics *.ppt *.swd *.db *.tar *.shtml *.properties *.vtt *.thmx *.m4v *.plain *.bmp *.crdownload *.WD3 *.emf *.otf *.wpd *.afm *.wav