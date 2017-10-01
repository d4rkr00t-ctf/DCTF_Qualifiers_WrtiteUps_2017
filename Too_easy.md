Problem Statement
> Ah man... I hate when I forget my password... Do you know it?

Here's the [executable](https://drive.google.com/open?id=0BzEeBAqEX505ODR4Tm1zSmhRMDA)

Let's do some analysis on file.
```
$ file looksgood.exe
looksgood.exe: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=5895d074bfc9c7835b9e8f06face0451e04c5004, not stripped
$ chmod +x looksgood.exe
$ ./looksgood.exe
Enter password:test
Wrong password
```

Okay, let's see dynamic lib calls and see if that's of any use.
```
$ ltrace ./looksgood.exe
__libc_start_main(0x400e16, 1, 0x7ffe816e50e8, 0x4011d0 <unfinished ...>
_ZNSt8ios_base4InitC1Ev(0x6022f1, 0xffff, 0x7ffe816e50f8, 160)                              = 0
__cxa_atexit(0x400c10, 0x6022f1, 0x6020b8, 6)                                               = 0
_ZNSaIcEC1Ev(0x7ffe816e4eff, 0x7ffe816e50e8, 0x7ffe816e50f8, 192)                           = 0x7ffe816e4eff
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_(0x7ffe816e4f00, 0x401254, 0x7ffe816e4eff, 192) = 0
_ZNSaIcED1Ev(0x7ffe816e4eff, 0x401254, 0x181ac20, 0x7f4b83bfbb20)                           = 0x7ffe816e4eff
_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc(0x6021e0, 0x40126c, 0x181ac20, 0x7f4b83bfbb20) = 0x6021e0
_ZNSolsEPFRSoS_E(0x6021e0, 0x400c90, 0x7f4b84199960, 0xfbad2a84 <unfinished ...>
_ZSt5flushIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_(0x6021e0, 0x400c90, 0x7f4b84199960, 0xfbad2a84Enter password:) = 0x6021e0
<... _ZNSolsEPFRSoS_E resumed> )                                                            = 0x6021e0
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1Ev(0x7ffe816e4f20, 0x7f4b83bfd780, 0, 0x7f4b8392e290) = 0x7ffe816e4f30
_ZSt7getlineIcSt11char_traitsIcESaIcEERSt13basic_istreamIT_T0_ES7_RNSt7__cxx1112basic_stringIS4_S5_T1_EE(0x6020c0, 0x7ffe816e4f20, 0, 0x7f4b8392e290
...
```

Too much obfuscation! No use here. Let's go to basic 101 and see the data of the elf file.
```
$ strings looksgood.exe | grep "pass" # just a guess for grep patter
strongpassword_as_a_pro
Enter password:
Wrong password
```

High chance that we have the password now! Let's see.
```
$ ./looksgood.exe
./looksgood.exe 
Enter password:strongpassword_as_a_pro
444354467b366436653137363063316133616539653465646532343537643864323462306263663230376561383337653833646362346430396532643734656639353862327d ... now decrypt hex.
$ echo 444354467b366436653137363063316133616539653465646532343537643864323462306263663230376561383337653833646362346430396532643734656639353862327d | xxd -r -p
DCTF{6d6e1760c1a3ae9e4ede2457d8d24b0bcf207ea837e83dcb4d09e2d74ef958b2}
```

`Flag: DCTF{6d6e1760c1a3ae9e4ede2457d8d24b0bcf207ea837e83dcb4d09e2d74ef958b2}`
