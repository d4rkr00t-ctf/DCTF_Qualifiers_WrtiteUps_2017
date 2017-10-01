Problem Statement
> I like to write and move all around the world. But do you know my story?

We're provided a [pcapng file](https://drive.google.com/open?id=0BzEeBAqEX505Q0RZMTFXTjAwQ2M)

Without much thinking I go first with finding data in the file and seeing if there's any flag.
```
$ strings kingofstone.pcapng | grep "DCTF"
DCTF{2d9895ecea1081b2241398d1b2c94eaf5be3bfaffec1ad946ed0a68ae95f8ed9}
```

Woah, damn! That was easier than the "Too easy" problem :D

`Flag: DCTF{2d9895ecea1081b2241398d1b2c94eaf5be3bfaffec1ad946ed0a68ae95f8ed9}`
