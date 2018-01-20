# How-to-setup-PHP-Debugging-xdebug-with-VSCode-Visual-Studio-Code-
Setup Xdebug in VS Code to debug your PHP Code on fly. follow the step by step instruction to setup xdebug properly.

## See in action (Video) [Click to Play](https://drive.google.com/file/d/1cZ7uTBFiOXQ6oERi-vXPO5znBwKoFtjj/view?usp=sharing)

## How to setup PHP Debugging (xdebug) with VSCode?

1. [First of all Install VSCode](https://code.visualstudio.com/Download)

2. [Install PHP Debug Adapter for Visual Studio Code](https://github.com/felixfbecker/vscode-php-debug)

3. [Install XDebug in WAMP](https://xdebug.org/wizard.php)

>Open phpinfo in browser
>Copy the view sorce code
>Paste in https://xdebug.org/wizard.php
>Download the suggested xdebug dll file
>Paste dll file inside the current version of php folder ext or zend_ext folder
>Open phpinfo and find 'Loaded Configuration File' to know what php.ini file wamp using
>Open php.ini file & place below code

```apache
[Xdebug]
zend_extension="FULL-XDEBUG-DLL-FILE-PATH"

; Example
; zend_extension="d:\wamp64\bin\php\php7.1.9\zend_ext\php_xdebug-2.6.0beta1-7.1-vc14-x86_64.dll"
; OR
; zend_extension="d:\wamp64\bin\php\php7.1.9\ext\php_xdebug-2.6.0beta1-7.1-vc14-x86_64.dll"

xdebug.remote_enable=1
xdebug.remote_autostart = 1
xdebug.remote_port="9000"
xdebug.profiler_enable=1
xdebug.remote_host="localhost"

xdebug.profiler_output_dir="<tmp path>"
;Example
;xdebug.profiler_output_dir="d:\wamp64\tmp"
```

4. Restart WAMP Server

>Open phpinfo & find xdebug, If found then you have installed xdebug successfully!
>If Wamp Restart But localhost not opening then try to change PORT. May PORT using by any other
>application already.

### [How can you find out which process is listening on a port on Windows?](https://stackoverflow.com/questions/48198/how-can-you-find-out-which-process-is-listening-on-a-port-on-windows)

### [Setup XDebug in VSCode](https://github.com/felixfbecker/vscode-php-debug)


>Example JSON - launch.json

```code
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```

5. Update VSCode Setting for PHP to add PHP Executable Path

```json
"php.validate.run": "onType",
"php.validate.executablePath": "<Your-Full-PHP-Path>php.exe"
```

6. Save and restart VSCode

Open PHP Project Folder and try to Debug code..If you are getting following error

#### VS Code Debug adapter process has terminated unexpectedly
#### VS Code Console Error -> listen EADDRINUSE::900)

Thats mean the PORT 9000 is being used by another, May have you are running PHPStorm Xdebug
Close the PHPStorm and try to debug again.

Still getting error then try to find which program using PORT 9000 and kill them
.. Still getting error try to change PORT in php.ini and launch.json and restart wamp and VSCode.

Now you can see Xdebugger working in VSCode.

#### Example Code to test

```php
<?php

/*
|--------------------------------------------------------------------------
| PHP XDebug Code Example - VS Code
|--------------------------------------------------------------------------
|
|  Information:
|
|   VS Code         :
|     Version       :   1.19.2
|     Commit        :   490ef761b76b3f3b3832eff7a588aac891e5fe80
|     Date          :   2018-01-10T15:55:03.538Z
|     Shell         :   1.7.9
|     Renderer      :   58.0.3029.110
|     Node          :   7.9.0
|     Architecture  :   x64
|
|   Windows         :   10
|
|   WAMP Server     :   3.1.0
|       PHP         :   7.1.9
|       APACHE      :   2.4.27
|       MySQL       :   5.7.19
|
|   PHP INI PATH    :   D:\wamp64\bin\apache\apache2.4.27\bin\php.ini
|       [Xdebug]
|       zend_extension              =   "d:\wamp64\bin\php\php7.1.9\zend_ext\php_xdebug-2.6.0beta1-7.1-vc14-x86_64.dll"
|       xdebug.remote_enable        =   1
|       xdebug.remote_autostart     =   1
|       xdebug.remote_port          =   "9000"
|       xdebug.profiler_enable      =   1
|       xdebug.remote_host          =   "localhost"
|       xdebug.profiler_output_dir  =   "d:\wamp64\tmp"
|
*/


// first loop
for ($i=0; $i < 10; $i++) {
        echo $i;
}

echo PHP_EOL;

// second loop
for ($i = 0; $i < 20; $i++)
{
    echo $i;
}

/* End of file php-test.php */
/* Location: /wamp64/www/test/php-test.php */
```

If you are facing any issue just ask your query by creating an issue.

Thanks :)

