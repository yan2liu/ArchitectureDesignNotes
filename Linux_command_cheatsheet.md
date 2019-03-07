# Data clean & preparation

- [Select line with end with String ('new_whale') & write to a new file ](https://www.linode.com/docs/tools-reference/tools/how-to-grep-for-text-in-files/)
    ```
    $ grep 'new_whale$' train.csv > new_whale.csv
    ```

- Select each line of string from query_str.csv, and find match line in table.csv, output to matched_table.csv
  ```
  $ grep -f query_str.csv table.csv > matched_table.csv
  ```
- [Delete all lines end with String ('new_wale') from one file (origin.csv) & write result to a new file (known_wales.csv)](http://www.theunixschool.com/2012/06/sed-25-examples-to-delete-line-or.html)
  ```
  $ sed '/new_wale$/d' origin.csv > known_wales.csv
  ```
- Replace ',5004' with ',-1,0.0,0.0,1.0,1.0' in file new_whale_with_neg_one_id.csv
  ```
  $ sed -i 's/,5004/,-1,0.0,0.0,1.0,1.0/g' new_whale_with_neg_one_id.csv
  ```
- Parse csv file with ',' (or ' ') as delimiter, choose  the '2' column to output file(second_col.csv). 
  ```
  $ cut -d , -f 2 comma.csv > second_col.csv
  ```
- Merge two files into one file with  each line as first file concatenate to second file & seperate by ','
  ```
  $ paste -d , first.csv second.csv
  ```
- Select id, count(id) from ids.csv, output as id,count format
  ```
  $ sort ids.csv | uniq -c | awk '{printf("%s,%s\n",$2,$1)}' > id_occurence_count.csv 
  ```
- Count total number of difference between two files.
  ```
  $ diff --suppress-common-lines --speed-large-files -y File1 File2 | wc -l
  ```
- Take first 858 lines to new file:
  ```
  $ head -858 total.csv >> first_858.csv
  ```
- Merge two files into one, one after another
  ```
  $ cat end.csv >> begin.csv
  ```
- Linux & Window dos forat change
  ```
  $ dos2unix window.txt
  $ unix2dos linux.txt
  ```
