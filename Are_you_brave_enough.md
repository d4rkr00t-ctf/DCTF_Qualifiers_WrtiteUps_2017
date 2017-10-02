Problem Statement
> You have a simple challenge, proove your web skills and get the flag.

![](https://ibin.co/3cNODtppuSkv.png)
We're give hint to access `index.php~`. Files ending with `~` are backups created by some editors.

Accessing the backup file, following source code is pulled off.
```
<?php

$db  = mysqli_connect('localhost','web_brave','','web_brave');

$id  = @$_GET['id'];
$key = $db->real_escape_string(@$_GET['key']);

if(preg_match('/\s|[\(\)\'"\/\\=&\|1-9]|#|\/\*|into|file|case|group|order|having|limit|and|or|not|null|union|select|from|where|--/i', $id))
    die('Attack Detected. Try harder: '. $_SERVER['REMOTE_ADDR']); // attack detected

$query = "SELECT `id`,`name`,`key` FROM `users` WHERE `id` = $id AND `key` = '".$key."'";
$q = $db->query($query);

if($q->num_rows) {
    echo '<h3>Users:</h3><ul>';
    while($row = $q->fetch_array()) {
        echo '<li>'.$row['name'].'</li>';
    }

    echo '</ul>';
} else {    
    die('<h3>Nop.</h3>');
}
```

So, we see `index.php` takes two queries `id` and `key`. `id` is passed as it is, without checking for string escaping but it has lots of regex matching. We need to perform sql injection through `id` paramter in a way, bypassing the regex patterns as well.

Observing the regex properly, I found that characters <pre>` ; % 0</pre> are not checked for.

SQL query <pre>select * from table where id=\`id\`</pre> evaluates to <pre>select * from table where 1=1</pre> and we have our bypass technique now.

We need to append `;%00` at end for `;` to terminate the sql query and `%00` (null byte) to inidcate end of string and ignore eveything else.

![](https://ibin.co/3cNOMdqUNFUr.png)

`Flag: DCTF{602dcfeedd3aae23f05cf93d121907ec925bd70c50d78ac839ad48c0a93cfc54}`
