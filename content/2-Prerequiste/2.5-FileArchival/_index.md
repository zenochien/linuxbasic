---
title : "File Compression and Archival"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5 </b> "
---

### Viewing file sizes
![Createacloud](/images/2-Prerequiste/5/1.png)

1. du with -sk shows the size of a file or directory in Kilobytes

```
$ du -sk test.img
```

2. du with -sh shows the size of a file or directory in human readable format

```
$ du -sh test.img
```
3. we can also use long list , ls -lh to print the size of the file.

```
$ ls -lh test.img
```

### Archiving Files
![Createacloud](/images/2-Prerequiste/5/2.png)

4. `tar` is used to group multiple files and directories into a single file. Hence it is specially used for archiving data.

```
$ tar -cf test.tar file1 file2 file3 
$ ls -ltr test.tar
```

5. The tar command followed by -tf option followed by the tar filename is used to see the contents of the tarball.

```
$ tar -tf test.tar
```

6. The tar command followed by -xf option followed by the tar filename is used to extract the contents from the tarball.

```
$ tar -xf test.tar
```

7.  tar command followed by -zcf option is used to compress the tarball to reduce its size.

```
$ tar -zcf test.tar
```

### Compression and Uncompression
![Createacloud](/images/2-Prerequiste/5/3.png)

8. Let us now look at the three popular ones
- bzip2 (.bz2 extension)
- gzip (.gz extension)
- xz (.xz extension)

```
$ bzip2 test.img
$ gzip test1.img
$ xz test2.img
```

9. The compressed files can be uncompressed by using the below commands
- bunzip2
- gunzip
- unxz

```
$ bunzip2 test.img
$ gunzip test1.img
$ unxz test2.img
```

10. Tools such as zcat , bzcat and xzcat allow the compressed files to be read without an uncompress
![Createacloud](/images/2-Prerequiste/5/4.png)

```
$ zcat hostfile.txt.bz2
$ zcat hostfile.txt.gz
$ zcat hostfile.txt.xz
```

### Searching for files and Patterns
![Createacloud](/images/2-Prerequiste/5/5.png)

11. Run locate command followed by the filename you are searching as an argument. This should return all paths matching the pattern.

```
$ locate City.txt
```

12. To manually update the DB, run the command updatedb and then run the locate command again

```
$ sudo updatedb
```

13. find

```
$ find /home/michael -name City.txt
```

### Grep
![Createacloud](/images/2-Prerequiste/5/6.png)
![Createacloud](/images/2-Prerequiste/5/7.png)


14. To search for the word second from the sample.txt

```
$ grep second sample.txt
```

15. To search for the word capital with case-insensitive use -i flag.

```
$ grep -i capital sample.txt
```

16. To search for a pattern recursively.

```
$ grep -r "thrid Line" /home/michael
```

17. To print the lines that don't matches the pattern

```
$ grep -v "printed" sample.txt
```

18. Match a pattern that form a whole word

```
$ grep -w exam examples.txt
```

19. You can also combine multiple options together. For example, to reverse the search and print all lines of the same file that doesn't match the whole word exam. Use grep -vw

```
$ grep -vw exam examples.txt
```

20. To print the number of lines after and before matching a pattern. Use grep command with -A and -B flags respectively.

```
$ grep -A1 Arsenal premier-league-table.txt
$ grep -B1 4 premier-league-table.txt
```

21. The -A and -B can be combined into one single search.
![Createacloud](/images/2-Prerequiste/5/8.png)

```
$ grep -A1 -B1 Chelsea premier-league-table.txt
```

### IO Redirection
![Createacloud](/images/2-Prerequiste/5/9.png)

In this section, we will take a look at IO Redirection.

- IO Redirection
- Standard Streams in Linux

There are three data streams created when you launch a linux commnad.

- Standard Input (STDIN)
        - STDIN is the standard input stream which accepts text as an input.

- Standard Output (STDOUT)
        - Text output is delivered as STDOUT or the standard out stream

- Standard ERROR (STDERR)
        - Error messages of the command are sent through the standard ERROR stream (STDERR)

### REDIRECT STDOUT

![Createacloud](/images/2-Prerequiste/5/10.png)

22. To redirect STDOUT to a file instead of printing it on the screen.

```
$ echo $SHELL > shell.txt
```

23. To append STDOUT to an exisiting file

```
$ echo $SHELL >> shell.txt
```

### REDIRECT STDERR
![Createacloud](/images/2-Prerequiste/5/11.png)

24. To redirect just the ERROR message we need to use 2 followed by forward arrow > symbol and then the name of the filename in which the errors are written.

```
$ cat missing_file 2> error.txt
```

25. To append the STDERR to the exisiting file

```
$ cat missing_file 2>> error.txt
```

26. If you want to execute and not print ERROR messages on the screen even if it generates a standard ERROR. You can redirect to /dev/null

```
$ cat missing_file 2> /dev/null
```

### Command Line Pipes
![Createacloud](/images/2-Prerequiste/5/12.png)

27. Command Line Pipes allow the linking of multiple commands.

```
$ grep Hello sample.txt | less 
```
### STDIN and STDOUT is the tee command.
![Createacloud](/images/2-Prerequiste/5/13.png)

28. Instead of the redirect operator, we can use the command line pipe (|) followed by tee command.

```
$ echo $SHELL | tee shell.txt
```

29. Use tee with -a option, to append instead of overwritting it

```
$ echo "This is the bash shell" | tee -a
```
### Lab - Working With Shell Part - II

30. Create a tarball of the directory called python and compress it using gzip. The compressed tar file should be available at /home/bob/python.tar.gz

```
$ tar -cf /home/bob/python.tar /home/bob/reptile/snake/python
$ gzip /home/bob/python.tar
```

31. There is a compressed file called eaglet.dat.gz located under the eagle directory. Extract it in the same location

```
$ gunzip /home/bob/birds/eagle/eaglet.dat.gz
```

32. A file has been copied to the laptop by the name of caleston-code. But he does not remember which directory he saved it in.Can you find it?

```
$ sudo find / -name caleston-code
```

33. Find the location of the file called dummy.service and redirect its absolute path to the file /home/bob/dummy-service. You can use the redirect operator with the echo command to save the answer to the file.

```
$ sudo find / -name dummy.service
$ echo /etc/systemd/system/dummy.service > /home/bob/dummy-service 
```

34. Find the file under /etc directory that contains the string 172.16.238.197. Save the answer using the absolute path in the file **/home/bob/ip**

```
$ sudo grep -ir 172.16.238.197 /etc/ > /home/bob/ip
```

35. Create a new file called /home/bob/file_wth_data.txt. This file should have one line of text that says a file in my home directory. Make use of the redirect operator.

```
$ echo "a file in my home directory" > /home/bob/file_wth_data.txt
```

36. Run the command python3 /home/bob/my_python_test.py and redirect the standard error to the file /home/bob/py_error.txt.

```
$ python3 /home/bob/my_python_test.py 2>/home/bob/py_error.txt
```

37. Read the file /usr/share/man/man1/tail.1.gz and without extracting it copy the first line of this file to /home/bob/pipes

```
$ zcat /usr/share/man/man1/tail.1.gz | head -1 > /home/bob/pipes
```

### Vi Editor
![Createacloud](/images/2-Prerequiste/5/14.png)

38. The command to open the vi editor is vi followed by the filename that you want to create or append.

```
$ vi /home/michael/sample.txt
```

### Command Mode

![Createacloud](/images/2-Prerequiste/5/15.png)

![Createacloud](/images/2-Prerequiste/5/16.png)

![Createacloud](/images/2-Prerequiste/5/17.png)

![Createacloud](/images/2-Prerequiste/5/18.png)

![Createacloud](/images/2-Prerequiste/5/19.png)

![Createacloud](/images/2-Prerequiste/5/20.png)

![Createacloud](/images/2-Prerequiste/5/21.png)

### Lab - VI Editor

39. Go to insert mode

```
Press i
```

40. Exit from insert mode and go to command mode

```
Press ESC
```

41. To remove a character

```
Move Cursor to the characters to be removed and press x to remove them
```

42. Change the file contents to Welcome to KodeKloud and save file.

```
Go to insert mode by pressing i and delete all content and type in new content. Once done press ESC key and go to command mode. Then type in command :w!
```

43. Update the port it listens on from 80 to 5000 in apache webserver.

```
Go to insert mode by pressing i and replace 80 with 5000 in line 10
```

44. Remove the line that starts with LogFormat.

```
Go to the line 33 and press dd (d twice) to remove the entire line.
```
45. To undo the previous change

```
Press u to undo previous change
```

46. There's a 6 hiding in the file. Find it.

```
find command /6
```



