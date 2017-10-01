Problem Statement
> A friend of mine is learning about encryption and now is challenging me to break it! Can you give it a go?

We're provided a zip file [junior3.zip](https://drive.google.com/open?id=0BzEeBAqEX505aHl0TFUtOWl1SkU)
```
$ unzip junior3.zip
Archive:  junior3.zip
  inflating: lock.iso                
  inflating: ransomware.py
```

Lets have a look at [ransomware.py](https://gist.github.com/mananpal1997/7f43e94f61057f1986bda178a8cc5394)
```
buf = ""
f = open("backup.zip", "r")
bu1 = ""
buf += f.read()
print buf
buf = buf.encode('hex')
buf += "831a34cdf478f76ad054f38c9aee6abd"
...
bu1 += "fd377a585a000004e6d6b44602002101"
...
buf = bu1 + buf
buf = buf.decode('hex')
g = open("lock.iso", "w")
g.write(buf)
g.close
f.close
```

We can see that there must be a backup.zip provided which cotains hex data, then more hex data is appended to it, and then all this hex data is stored in a file named `lock.iso`. So, we have to work in reverse way here and have to get `backup.zip` from `lock.iso`.

We can observe that the `backup.zip content` must start with end of variable `bu1`(...6a55642402) and end with start of `buf1` (831a...) . Lets get all hex data from lock.iso preceeding this extra data. Also, original data is hex-encoded, so we have to decode it.
```
$ #select the line which contains end of bu1 and dump all data after that in the line
$ xxd -p lock.iso | sed -n '1,/831a/ p' | sed 's/831a.*//' | sed -ne 's/^.*2402//p' > dump
$ #now trim all the buf part
$ xxd -p lock.iso | sed -n '1,/831a/ p' | sed 's/831a.*//' | sed -e '1,/2402/d' >> dump
$ cat dump | tr -d '\n' | xxd -r -p > backup.zip # hex decoding and recovering backup.zip
$ unzip backup.zip
Archive:  backup.zip
  inflating: index.txt
```

Inside `index.txt`, we find `Flag: DCTF{474dac08d29d013515a312d1a8460050634f9b3cb6a696a4c73652d1802a1872}`
