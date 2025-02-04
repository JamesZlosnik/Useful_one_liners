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
3. Find files of a certain name and copy them to a new folder using the name of the folder they are in as the name of the file (useful for examples such as the one below where a pipeline puts out a generic name, say for a fasta file)

```
find . -type f -name "contigs.fa" -printf "/%P\n" | while read FILE ; do DIR=$(dirname "$FILE" );\cp ."$FILE" "../fastas_for_emmtyper""$DIR".fa;done
```
Note also in this example, you can test it by adding echo immediately before cp.

From:  https://askubuntu.com/questions/746860/rename-a-file-to-parent-directorys-name-in-terminal

4. Generate a input tsv from a list of files of a given type (.fa used here) and their paths in multiple subdirectories:

```
find $PWD -name '*.fa' -type f -print0 | while IFS= read -r -d '' file; do echo -e "$(basename "$file" .fa)\t$file"; done > input.tab
```
Note, you can modify this as necessary to change the type of file or the amount of the file name removed to form the sample name in the first column

5. Check a sample list (samples.txt) against a directory of paired end fastq files to find missing samples:

```
while read sample; do
  ls data/"$sample"*.fastq.gz >/dev/null 2>&1 || echo "$sample is missing"
done < samples.txt
```

## Scripts

The below scripts may be of use:

| Script | Comment | Source |
|--------|---------|--------|
|Fasta parser | Python script to parse a multi fasta file and report composition as well as produce file listing entries that contain non-ATGC bases | made by Co-pilot|


## Nextflow

## General bioinformatics packages

### Seqkit


