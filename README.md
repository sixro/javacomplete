# vim-javacomplete
> This is javacomplete, an omni-completion script of JAVA language for vim.

[![Build Status](https://travis-ci.com/sixro/javacomplete.svg?branch=master)](https://travis-ci.com/sixro/javacomplete)

This is a fork of the [mirror](https://github.com/vim-scripts/javacomplete) of http://www.vim.org/scripts/script.php?script_id=1785


## Summary

  * [Features](#features)
  * [Requirements](#requirements)
  * [What it offers](#what-it-offers)
  * [How to contribute](#how-to-contribute)
  * [Limitations](#limits)
  * [TODOs](#todos)
  * [Credits](#credits)


## <a name="features"></a>Features

  * List members of a class, including (static) fields, (static) methods and ctors.
  * List classes or subpackages of a package.
  * Provide parameters information of a method, list all overload methods.
  * Complete an incomplete word.
  * Provide a complete JAVA parser written in Vim script language.
  * Use the JVM to obtain most information.
  * Use the embedded parser to obtain the class information from source files.
  * Tags generated by ctags can also be used.
  * JSP is supported, Builtin objects such as request, session can be recognized.
  * The classes and jar files in the WEB-INF will be appended automatically to classpath.


## <a name="requirements"></a>Requirements

It works on all the platforms where
  * Vim version 8.0 and above
  * JDK version 8 and above
existed 


## <a name="what-it-offers"></a>What it offers

It recognize nearly all kinds of Primary Expressions (see langspec-3.0)
except for "Primary.new Indentifier". Casting conversion is also supported.
Samples of input contexts are as following:	(<kbd>|</kbd> indicates cursor)


### after `.`, list members of a class or a package

  * `package.`<kbd>|</kbd>         subpackages and classes of a package
  * `Type.`<kbd>|</kbd>                static members of the 'Type' class and "class"
  * `var.`<kbd>|</kbd> or `field.`<kbd>|</kbd>     members of a variable or a field
  * `method().`<kbd>|</kbd>         members of result of method()
  * `this.`<kbd>|</kbd>                   members of the current class
  * `ClassName.this.`<kbd>|</kbd>  members of the qualified class
  * `super.`<kbd>|</kbd>               members of the super class
  * `array.`<kbd>|</kbd>                members of an array object
  * `array[i].`<kbd>|</kbd>             array access, return members of the element of array
  * `"String".`<kbd>|</kbd>            String literal, return members of java.lang.String
  * `int.`<kbd>|</kbd> or `void.`<kbd>|</kbd>       primitive type or pseudo-type, return "class"
  * `int[].`<kbd>|</kbd>                   array type, return members of a array type and "class"
  * `java.lang.String[].`<kbd>|</kbd>
  * `new int[].`<kbd>|</kbd>           members of the new array instance
  * `new java.lang.String[i=1][].`<kbd>|</kbd>
  * `new Type().`<kbd>|</kbd>      members of the new class instance 
  * `Type.class.`<kbd>|</kbd>      class literal, return members of java.lang.Class
  * `void.class.`<kbd>|</kbd> or `int.class.`<kbd>|</kbd>
  * `((Type)var).`<kbd>|</kbd>         cast var as Type, return members of Type.
  * `(var.method()).`<kbd>|</kbd>   same with `var.`<kbd>|</kbd>"
  * `(new Class()).`<kbd>|</kbd>    same with `new Class().`<kbd>|</kbd>"


### after `(`, list matching methods with parameters information.

  * `method(`<kbd>|</kbd>)                 methods matched
  * `var.method(`<kbd>|</kbd>)           methods matched
  * `new ClassName(`<kbd>|</kbd>)  constructors matched
  * `this(`<kbd>|</kbd>)                        constructors of current class matched
  * `super(`<kbd>|</kbd>)                     constructors of super class matched

Any place between `(` and `)` will be supported soon.  
Help information of javadoc is not supported yet.


### after an incomplete word, list all the matched beginning with it [![TEST](https://img.shields.io/badge/x-TEST-brightgreen)](#)

  * `var.ab`<kbd>|</kbd>  subset of members of var beginning with `ab`
  * `ab`<kbd>|</kbd>      list of all maybes


### import statement

  * `import         java.util.`<kbd>|</kbd>
  * `import         java.ut`<kbd>|</kbd>
  * `import         ja`<kbd>|</kbd>
  * `import         java.lang.Character.`<kbd>|</kbd>        e.g. `Subset`
  * `import static java.lang.Math.`<kbd>|</kbd>        e.g. `PI, abs`


### package declaration

   * `package com.`<kbd>|</kbd>

The above are in simple expression.

### after compound expression:

  * `PrimaryExpr.var.`<kbd>|</kbd>
  * `PrimaryExpr.method().`<kbd>|</kbd>
  * `PrimaryExpr.method(`<kbd>|</kbd>)
  * `PrimaryExpr.var.ab`<kbd>|</kbd>
  * `java.lang.System.in.`<kbd>|</kbd>
  * `java.lang.System.getenv().`<kbd>|</kbd>
  * `int.class.toString().`<kbd>|</kbd>
  * `list.toArray().`<kbd>|</kbd>
  * `new ZipFile(path).`<kbd>|</kbd>
  * `new ZipFile(path).entries().`<kbd>|</kbd>


### Nested expression:

  * `System.out.println( str.`<kbd>|</kbd>` )`
  * `System.out.println(str.charAt(`<kbd>|</kbd>` )`
  * `for (int i = 0; i < str.`<kbd>|</kbd>`; i++)`
  * `for ( Object o : a.getCollect`<kbd>|</kbd>` )`


## <a name="how-to-contribute"></a>How to contribute

Open a pull request.

At the moment, this is pretty the original project.  
The only changes I made are:
  * Changed the `s:Log` function to write in a file under `/tmp/` in this way I can debug what happens (the plugin is pretty complex to follow)
  * Added a huge amount of logs
  * Disabled the collection of data from `tags` because it is really bugged: in a sense that it collects data from tags and then it expects a format that is absolutely not matching with the content returned by that function
  * Added [vim-vspec](https://github.com/kana/vim-vspec) in order to add tests so that changing it would not break everything


## <a name="limits"></a>Limitations

The embedded parser works a bit slower than expected.


## <a name="todos"></a>TODOs

  - Improve performance of the embedded parser. Incremental parser.
  - Add quick information using balloonexpr, ballooneval, balloondelay.
  - Add javadoc
  - Give a hint for class name conflict in different packages.
  - Support parameter information for template
  - Make it faster and more robust.


## <a name="credits"></a>Credits

The first version has been created and maintained by [Fang Cheng](mailto:fangread@yahoo.com.cn).
