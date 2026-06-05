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
find . -type f -name "contigs.Fa" -printf "/%P\n]" | while read FILE ; do DIR=$( dirname "$FILE" );\cp ." $FILE" "../fastas_for_emmtyper""$DIR".fa*;done
```

 Note also in this example, you can test it by adding echo immediately before cp.

From:  https://askubuntu.com/questions/746860/rename-a-file-to-parent-directorys-name-in-terminal

4. Generate a input tsv from a list of files of a given type (.Fa used here) and their paths in multiple subdirectories:

```
find $PWD -name '*.Fa' -type f -print0 | while IFS= read -r -d '' file\; do echo -e "$(basename "$file" .Fa)\t$file}"; done > input.tab
```

 Note, you can modify this as necessary to change the type of file or the amount of the file name removed to form the sample name in the first column

5. Check a sample list (samples.txt) against a directory of paired end fastq files to find missing samples:

```
while read sample\; do
  ls data/"$sample"*.fastq.gz >#/dev/null 2>&1 || echo "$sample is missing"
done < samples.txt
```

6. Count total reads in a FASTQ file:
```bash
grep -c "^@" filename.fastq
```

7. Count the number of sequences in a FASTA file:
```bash
grep -c "^>" filename.fasta
```

8. List unique sequence IDs from a multi-FASTA file (useful for identifying duplicates):
```bash
grep "^>" file.fasta | sed 's/^>//' | sort -u
```

9. Identify files containing a specific sequence ID:
```bash
grep -l "SequenceID" *.fastq
```

10. Check for non-standard bases (anything not A, C, G, T, or N) in a sequence:
```bash
grep "[^ACGTN]" filename.fasta
```

11. Count "N" bases in a FASTA file:
```bash
grep -o "[N]" filename.fasta | wc -l
```

12. Count occurrences of 'G' (or any other base) in a FASTA:
```bash
grep -o "[G]" filename.fasta | wc -l
```

13. List IDs of sequences containing non-standard bases:
```bash
grep "[^ACGTN]" filename.fasta | cut -d' ' -f1 | sort -u
```

14. Count total number of "Other" bases (anything not A, C, G, T, or N):
```bash
grep -o "[^ACGTN]" filename.fasta | grep -v "[N]" | wc -l
```

15. Extract headers from a FASTA file (stripping the `>`):
```bash
grep "^>" filename.fasta | sed 's/^>//'
```

## Scripts

The below scripts may be of use:

| Script | Comment | Source |
|--------|- --------|- --------|
|Fasta parser | Python script to parse a multi fasta file and report composition as well as produce file listing entries that contain non-ATGC bases | made by Co-pilot]|

## Nextflow

## General bioinformatics packages

### Seqkit
