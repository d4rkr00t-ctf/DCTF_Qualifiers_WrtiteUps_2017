Problem Statement

> What do you think about this algorithm? I worked with my good friend to push it to the repository.

We're given a python file named `get_flag_at_dctf2k17.py` which is a python script. It must have a key to decrypt a message in the file and give us the flag. But how to find the key??

There's these lines in the code
```
f = open ("jaksjkljaflk124.dctf.def.camp", "r")
buf =f.read()
f.close()
key = buf
```

So, `jaksjkljaflk124.dctf.def.camp` contains the file, but we don't know where to find this file. After effortless tries, I read the problem statement again.
> I worked with my good friend to push it to the **repository**.

Hmmm, repository, github... hmmm. (see where I'm going). I quickly go to github and search for the file name `get_flag_at_dctf2k17.py` and to my surprise, there's only one such file. I started looking at the commit history and Voila!

![](https://ibin.co/3cIcxJ4uJ5Ir.png)
![](https://ibin.co/w800/3cId1Mj4EhpN.png)

So, I change the original [file](https://gist.github.com/mananpal1997/10688fb8ec44e584b1927b46f42563d6) accordinly and then run it.
```
$ python get_flag_at_dctf2k17.py
Key: 'fossil'
Decrypted: 'I have always believed the you can recover this basic flag from my so basic encryption. And actually you found it in your own way. I appreciate that. Well My friend this is your key: >>>>>>>>>> DCTF{a752958e5efbaa808d8c173c9d21208f06927d1a0929d2f3068ea083c692513b} <<<<<<<<<<<<. Now I will just sing a song in order to prelong the length of this message. A B C D E F G Come and sing along with me H I J K L M N O P Tell me what you want to be Q R S T U V W X Y and ZNow I know my ABCs Next time won t you sing with me A B C D E F G H I J K L M N O P Q R S T U V W X Y and Z Now I know my ABCs Next time won t you sing with me! ONE MORE TIME! A B C D E F G Come and sing along with me H I J K L M N O P Tell me what you want to be Q R S T U V W X Y and ZNow I know my ABCs Next time won t you sing with me A B C D E F G H I J K L M N O P Q R S T U V W X Y and Z Now I know my ABCs Next time won t you sing with me!'
```

`Flag: DCTF{a752958e5efbaa808d8c173c9d21208f06927d1a0929d2f3068ea083c692513b}`
