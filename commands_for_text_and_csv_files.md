# Most used Ubuntu terminal commands for manipulating CSV and text files

Here are some of the most used Ubuntu terminal commands for manipulating CSV and text files:

* `cat`: Displays the contents of a file.
* `head`: Displays the first few lines of a file.
* `tail`: Displays the last few lines of a file.
* `grep`: Searches for a pattern in a file.
* `sort`: Sorts the lines of a file.
* `uniq`: Removes duplicate lines from a file.
* `wc`: Counts the lines, words, and characters in a file.
* `awk`: A powerful text processing language that can be used to manipulate CSV and text files.
* `sed`: A stream editor that can be used to search and replace text in a file.
* `tr`: Translates characters in a file.

## Examples

- To display the contents of a CSV file called `data.csv`, you would use the following command:  
`cat data.csv`  

- To display the first 10 lines of a CSV file called data.csv, you would use the following command:  
`head -n 10 data.csv`  

- To display the last 10 lines of a CSV file called `data.csv`, you would use the following command:  
`tail -n 10 data.csv`  

- To search for the word "hello" in a CSV file called data.csv, you would use the following command:  
`grep "hello" data.csv`  

- To sort the lines of a CSV file called data.csv by the first column, you would use the following command:  
`sort -k1 data.csv`  

- To remove duplicate lines from a CSV file called `data.csv`, you would use the following command:  
`uniq data.csv`  

- To count the number of lines, words, and characters in a CSV file called data.csv, you would use the following command:  
`wc -l data.csv`  
`wc -w data.csv`  
`wc -c data.csv`  

- To use `awk` to extract the first and third column from a CSV file called data.csv and print the results to the console, you would use the following command:  
`awk -F, '{print $1,$3}' data.csv`  

- To use sed to replace all occurrences of the word "hello" with the word "goodbye" in a CSV file called data.csv, you would use the following command:  
`sed 's/hello/goodbye/g' data.csv`  

- To use tr to translate all spaces in a CSV file called data.csv to tabs, you would use the following command:  
`tr ' ' '\t' data.csv`  

