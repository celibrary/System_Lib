
# SystemLibCourse
For use in my system's librarian course.
## Some systems we are using



  * VMs
  * Bash
  * GitHub
  * Nano
  * Markup Language

There will be more in future weeks.

I added this line in VM on Feb. 5th, 2026

## Notes from Week 5
I someone created 2 README.md files.  I deleted one using the command rm

## Notes on using grep
* Used cntrl Z to return to the shell when "lost"
*cat used to combine file but also opened the file
*Logout will close Linux
*grep -vic "article"
"grep -oi "^[a-z*]" savedrecs.bib | sort |uniq -c count of articles

## Notes from additional practice Feb. 15th
	* Repetition is key
	* Flashcard Program - each time I use it is is helpful
	* Less = view and paginate text files
	* Repetition with grep crucial
	* Cat will allow you to view the file
	* structure is grep -ic or -in  "" file

> forgot i need nano to edit text file
>> [Textbook](https://cseanburns.github.io/systems-librarianship/3a-searching-with-grep.html)


## grep
-case senstitive
-fast, precise searching of a file.
--i ignores case
-v search lines that do not match
-c count

grep -oi "search term" file name

## apt and sudo
Apt installs a program and updates
sudo allows you to give commands as an administrator
sudo apt yaz

## yaz
allows searches of another system like a library catalog.
search by marc terms
-yaz-client
Z> Open
bib1-attr documentation
f = find
infor retrieval using z39.50 protocols
PQF-prefix query format
-f @and @attr 1= "term"
