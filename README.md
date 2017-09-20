# Serial Number System

An extremely basic serial number and HWID lock system for selling VB.NET and C# programs!

## Setup

### SQL

Enter PHPMyAdmin, make a new database named "serial".

Click on the "SQL" tab and enter 
``` sql
CREATE TABLE `serial`.`serial`(
    `id` INT NOT NULL AUTO_INCREMENT,
    `serial` VARCHAR NOT NULL,
    `hwid` VARCHAR NOT NULL,
    PRIMARY KEY(`id`)
) ENGINE = InnoDB;
```
then hit "Go"

### Web Files

Edit serialcheck.php from

``` php
$link = mysqli_connect('localhost','root','');
$database = mysqli_select_db($link,'serial');
```

to match your SQL login! (Example)

``` sql
$link = mysqli_connect('localhost','user','password');
$database = mysqli_select_db($link,'serial');
```

Now edit generateserial.php

``` sql
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "serial";
```

(Yes I know 2 different login forms is trash but whatever.

### Application

Edit line 81 and 122 from

``` vb.net
WebBrowser1.Navigate("http://localhost/serial/serialcheck.php?serial=" + TextBox1.Text + "&hwidin=" + TextBox2.Text + "&submit=Submit")
```

To

``` vb.net
WebBrowser1.Navigate("http://YOURDOMAINGOESHERE.com/PATH/TO/serialcheck.php?serial=" + TextBox1.Text + "&hwidin=" + TextBox2.Text + "&submit=Submit")
```

Finally, edit lines 99-106 to be something like:

``` vb.net
            ElseIf (WebBrowser1.DocumentText.Contains("1")) Then
                check = 0
                Button1.Enabled = True
                My.Settings.Installed = True
                My.Settings.Serial = TextBox1.Text
                My.Settings.Save()
                Timer1.Stop()
                Form2.Show()
```

And build your program on Form2

Best of luck!

## Credits

[JackkTutorials](https://www.youtube.com/channel/UC64x_rKHxY113KMWmprLBPA) for the [HWID creation and encryption code.](https://www.youtube.com/watch?v=CBe-gQiO-dA)
