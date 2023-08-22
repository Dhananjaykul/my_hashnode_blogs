---
title: "Basic Linux Commands"
seoTitle: "Basic Linux Command"
seoDescription: "Learn the most important and useful basic Linux commands for beginners with this comprehensive guide. Master the command line interface with step-by-step in"
datePublished: Mon Apr 03 2023 02:50:25 GMT+0000 (Coordinated Universal Time)
cuid: clg08hohx000109jq39rr0xxq
slug: basic-linux-commands
tags: devops, 90daysofdevops, wemakedevs, trainwithshubham, 90daysofdevops-chanllenge

---

Task 1. To view what's written in a file.
>>>>      cat example.txt

Task2. To change the access permissions of files.
>>>>     chmod [options] mode filename
you can use a numeric mode to set the permissions. In this mode, each permission is represented by a number:
4 - read , 2 - write , 1 - execute
eg. chmod 740 example.txt   for user 7 =>rwx
                                                 for group 4 =>r--
                                                 for others 0=>---


Task 3. To check which commands you have run till now.
 >>>> history

Task 4. To remove a directory/ Folder.
>>>> rm -r directory_name


Task 5. To create a fruits.txt file and to view the content.
>>>>  to create file and add content to it 
              echo "Apple" > fruits.txt    
>>>> to view the content
              cat fruits.txt
>>>> to add more fruits to the file, you can use the >> operator.
            echo "Banana" >> fruits.txt

Task 6. Add content in devops.txt (One in each line) - Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava.
>>>>>            echo "Apple"  >> devops.txt 
                        echo "Mango"  >> devops.txt 
                        echo "Banana"  >> devops.txt 
                        echo "Cherry"  >> devops.txt 
                        echo "Kiwi"  >> devops.txt 
                        echo "Orange"  >> devops.txt 
                        echo "Guava"  >> devops.txt 

Task 7.   To Show only top three fruits from the file.
>>>>    head -n 3 fruits.txt


Task 8.  To Show only bottom three fruits from the file.
>>>>   tail -n 3 fruits.txt

Task 9.  To create another file Colors.txt and to view the content.
>>>> touch  Colors.txt or    echo "Red"  > Colors.txt      (to create a file and added content to it)
            cat Colors.txt   (to view the content)

Task 10. Add content in Colors.txt (One in each line) - Red, Pink, White, Black, Blue, Orange, Purple, Grey.
>>>>          echo "Red" >> Colors.txt
                   echo "Pink" >> Colors.txt
                   echo "White" >> Colors.txt
                   echo "Black" >> Colors.txt
                   echo "Blue" >> Colors.txt
                   echo "Orange" >> Colors.txt
                   echo "Purple" >> Colors.txt
                   echo "Grey" >> Colors.txt


Task 11. To find the difference between fruits.txt and Colors.txt file.
>>>>      diff fruits.txt Colors.txt
