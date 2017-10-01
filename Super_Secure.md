Problem Statement
> Oscar is more of an offline type of guy. Can you hack in his platform?

So we have a html form asking for username and password.

![](https://ibin.co/3cITDTdXlyr7.png)

Lets have a look at the source of the page.

![](https://ibin.co/3cITVH1107lN.png)

So, we have `Username: th1s1sn0tadmin3mail, Password: averysafesecurepassword` (change the type of input for username from email to text).

After submitting the credentials, following message is shown:
`With all do respects! Don't you think I am smarter than you? Don't you think I will keep my stuff offline? My secrets are on this website! But believe me the only way you can get your hand on it is to get offline! No internet!`

Based on the message shown, let's try and simulate offline mode by firing up firebug. Voila! An error message pops up trying to reconnect to internet, and it also shows the flag.

![](https://ibin.co/w800/3cITnh6opfZV.png)

The flag is not completely visible in the popup, so we just inspect it and get the flag. `Flag: DCTF{76c77d557198ff760ab9866ad1261a01a7298c349617cc4557462f80500d56a7}`
