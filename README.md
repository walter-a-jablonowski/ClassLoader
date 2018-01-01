# ClassLoader

A self-updating PHP class loader

**Download** http://github.com/walter-a-jablonowski/ClassLoader

**Authors**

- Walter A. Jablonowski <walter.a.jablonowski@gmail.com>
- Al-Fallouji Bashar bashar@alfallouji.com
- Charron Pierrick pierrick@webstart.fr


# About

ClassLoader is a **self-updating** PHP class loader

- Install once and forget class loading
- Just put new classes in your library folder or any subfolder
- ClassLoader will find them on its own

You don’t have to implement complex naming rules between the filename and the classname. Just define (at least) one single library base folder, thats it! ClassLoader will allow you to implement whatever naming rules you want and may have mutliple classes in one file


# How can I use it?

```php
include('lib/ClassLoader.php');

$classLoader = new ClassLoader();
$classLoader->setCacheFile('class_loader_cache.php');

// By default the ClassLoader will parse all .php files. You can
// modify this behavior by using the setFileRegex method as below
// $classLoader->setFileRegex('/\.(inc|php)$/');

// Add library base folder

// at last one, all subfolders and classes will be scanned
$classLoader->addLibraryFolder('/my/common/php-lib'); // ... all my commonly used classes
$classLoader->addLibraryFolder('/my/proj/lib');       // ... all my proj classes

// Skip folders (if you want)

$classLoader->skipFolder('/my/common/php-lib/skip_this_classes');
$classLoader->skipFolder('/my/proj/lib/skip_this_classes');

$classLoader->skipAnyNameContaining('_NO_USE');

$classLoader->install();

```


# How does it work?

Using the PHP tokenizer mechanism, it will parse folder(s) and discover the different classes and interfaces defined

- It will scan any given folder and find any defined PHP classes or interfaces
- It will then create an hashtable that will reference what class can be found in what file
- This hash table is serialized and cached in a file

- Whenever, your program will look for a non-existing class, ClassLoader will look on that hash table and load the file if it exists

- A fallback mechanism can be used also in a development environment that will try to rescan all the folders once more (this mechanism is usefull when you are often adding new classes to your program)


# License

```
This Code is released under the GNU LGPL

This library is free software; you can redistribute it and/or modify it
under the terms of the GNU Lesser General Public License as published
by the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This library is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
or FITNESS FOR A PARTICULAR PURPOSE.

See the GNU Lesser General Public License for more details
```


# Original Source

Based on PHP-Autoload-Manager-1.0 2017-12 https://github.com/alfallouji/PHP-Autoload-Manager

- Added the ability to exclude if a certain string is found in fil or folder name
  $classLoader->skipAnyNameContaining('_NO_USE');

- New name for class, changed names
- Readme
- Minor changes


# Tasks

- ClassLoader::SCAN_CACHE? see line 275
