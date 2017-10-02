Problem Statement
> Every book is unique in its own way! Go and read the story of a brave man!

We're provided with a zip file [books.zip](https://drive.google.com/open?id=0BzEeBAqEX505SlI4VjdyLUpjc00)
```
$ unzip books.zip -d books/
Archive:  books.zip
  inflating: books/0001.txt          
  inflating: books/0002.txt          
  inflating: books/0003.txt          
  inflating: books/0004.txt          
  inflating: books/0005.txt          
  inflating: books/0006.txt          
  inflating: books/0007.txt          
  inflating: books/0008.txt          
  inflating: books/0009.txt          
  inflating: books/0010.txt
```

So, all these txt are like huge novels, and I currently had no idea what to do. As I started reading some a little bit, I found that they were all same in the starting.Hmmm. Let's find if something is different.
```
$ sort books/0001.txt books/0002.txt | uniq -u
glimpse last summer at the Palais-Royal. Some of 
glimpse last summer DC at the Palais-Royal. Some of
```

I can see above that there's **DC** extra in `0002.txt`. Still not sure where to go. Let's check again for other file.
```
$ sort books/0001.txt books/0003.txt | uniq -u
benches ranged along TFthe walls, and in the centre of 
benches ranged along the walls, and in the centre of
```

So here, **TF** is an extra word in the file `0003.txt` as compared to `0001.txt`, rest is same. So, so far, we've got **DCTF**. Now we know exactly what to do :D

But when I did this for `0001.txt` and `0010.txt`, I got more than 2 lines with different text, and `sort` command just messes up with the order, so can't use that to get the flag.

Why not use diff then, right? Let's write a loop to traverse all txt files and create a dump of diff of all files with `0001.txt`.
```
$ for file in books/*; do diff books/0001.txt $file | grep -v "^---" | grep -v "^[0-9c0-9]" >> dump; done
$ wc -l dump
32 dump
$ # We'll take two lines at a time and find the words which are different, narrowing down our search
$ for i in {1..16}; do head -"$((2*i))" dump | tail -2 | grep -oE '\w+\S+' | sort | uniq -u; done
```
<pre>
<b>DC</b>
<b>TF</b>the
have
h<b>{</b>ave
<b>7ba61</b>
wa<b>0cc5d</b>s
was
a<b>a3966</b>nd
and
fo<b>b7c64</b>r
for
<b>a81c3</b>
Mor<b>cfcdb</b>eau,
Moreau,
<b>1b1d0
9e3de
5ad11
89268
bf0e6
18ff7
1f08}</b></pre>

So, we can easily figure out the flag now.

`Flag: DCTF{7ba610cc5da3966b7c64a81c3cfcdb1b1d09e3de5ad1189268bf0e618ff71f08}`
