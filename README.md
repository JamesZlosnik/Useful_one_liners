# Useful_one_liners
A place to keep one-line pieces of code that might come in handy

## Bash

1. Find files of a certain type and copy to another location:

```
find . -name \*.xls -exec cp {} newDir \;
```

From: https://stackoverflow.com/questions/15617016/copy-all-files-with-a-certain-extension-from-all-subdirectories

2. Find files of a certain type and copy to a new location retaining file structure:

```
find top_level_folder/ -name '*.tsv' | cpio -pdm new_folder_name/
```
