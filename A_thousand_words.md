Problem Statement
> I bet your eye can spot the original photo!

So, we're provided with a zip file [images.zip](https://drive.google.com/open?id=0BzEeBAqEX505S0hrMlFjSW95VEU). Let's unzip it and see.
```
$ unzip images.zip -d data/
Archive:  images.zip
  inflating: data/0001.png           
  inflating: data/0002.png           
  ...           
  inflating: data/1154.png
```

These are a lot of images! Looking normally through some photos, all looked same. I checked more and observed that each image has somewhat similar part at end of it which is
```
DCTF
%tEXtCopyright
trololololololololololololo
%tEXtdate:create
2017-09-29T13:30:00+03:00c6&
%tEXtdate:modify
2017-09-29T13:30:00+03:00
tEXtSoftware
Shutterc
IEND
```

Focussing more on problem statement, there's an odd-one out image. So, lets see data of all images and try to grep for flag.
```
$ grep -H "DCTF{" data/*
Binary file data/1024.png matches
$ strings data/1024.png | grep "DCTF{"
DCTF{162d6e3865b2be32851fb8bd3cca73bdc1a052f9da75d8680c471eb45af522df}
```

`Flag: DCTF{162d6e3865b2be32851fb8bd3cca73bdc1a052f9da75d8680c471eb45af522df}`
