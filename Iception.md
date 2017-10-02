Problem Statement
> Do you like our logo?
![](https://ibin.co/3cMz5J6L7nFD.png)

Looking normally at the image in my hex editor, I found more than one `IEND`. So, it means that this image contains more than one image. Let's cross-check.
```
$ strings Youmaynotseeme.png | grep "IEND" | wc -l
13
$ strings Youmaynotseeme.png | grep "IHDR" | wc -l
13
```

So, we got 13 `IEND` and 13 `IHDR` chunks in the main datastream, and this means that our PNG main datastream has 13 PNG datasteams inside it.

I wrote this [python script](https://gist.github.com/mananpal1997/4e9f3f8ecda4b2a5b7050afa1a784a44) to split the original image further into 13 PNGs.

Looking through these 13 images obtained, all are same to original image but one, which contains the flag.

![](https://ibin.co/w800/3cN53uTZsqel.png)

`Flag: DCTF{61c9183bf4e872b61d71697891e0a4451eff0b07bcd3373d4aac94aa74baccb9f}`
