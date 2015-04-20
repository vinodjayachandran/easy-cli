# Easy-Cli #

Easy-Cli is a framework for building command-line interface using java. Easy-Cli uses a simple plugin architecture that let developers deploy components to build components with control over all aspects of console-based applications including display, IO, prompt, input control, and command delegation.
Easy-Cli comes with a default runtime that implements all of the basic components needed for a fully functioning console-based app. To customize the runtime with your own command, you simply create and deploy your own plugin jars

## Features ##
  * Easy to get started
  * Small API footprint with low learning curve
  * Ability to build complex CLI tools using plugin architecture
  * Simple component model that imposes little constraints on your design
  * The plugin architecture is designed for extensibility and feature-scalability:
  * If you don't like how the default implementation works, you can change it completely
  * Implement the components you want to change and your feature will be included next time the console is restarted
  * Provides flexibility to use any Java CLI parsers, to name a few  Jakarta Commons Cli,  JCommander, Martian JSAP etc
  * Easy CLI supports different types of options
    1. POSIX like options (ie. tar -zxvf foo.tar.gz)
    1. GNU like long options (ie. du --human-readable --max-depth=1)
    1. Java like properties (ie. java -Djava.awt.headless=true -Djava.net.useSystemProxies=true Foo)
    1. Short options with value attached (ie. gcc -O2 foo.c)
    1. long options with single hyphen (ie. ant -projecthelp)
  * Plugins are deployed as simple jar files

## Getting Started ##

It’s easy to get started with Easy-Cli to build your first console application.
  * Unzip easy-cli.zip at a locatin of your choice. The zip file will create a directory named easy-cli (will refer to it as {CLI\_HOME}).
  * Change directory inside {CLI\_HOME} and inspect the files. You will see the followings:

![http://crypticarticles.files.wordpress.com/2013/06/image.png](http://crypticarticles.files.wordpress.com/2013/06/image.png)

  1. config – All the configuration files are placed here
  1. cli.jar - The launcher jar file
  1. lib - Library files to boot Easy-Cli and place your dependency jars here
  1. plugin - Location for Easy-Cli plugin jars. All the cli commands are developed and deployed as jars (plugins) in

From within {CLI\_HOME}, start the Easy-Cli by executing cli.sh (Linux variants) /cli.bat (Windows) depending on your OS

![http://crypticarticles.files.wordpress.com/2013/06/cli-1.png](http://crypticarticles.files.wordpress.com/2013/06/cli-1.png)

If you type ‘help’ at the prompt, for instance, you will be actually invoking in built in help command which lists help info for all Command objects that are mapped. Each command is backed by a plugin class installed in the plugins directory.

![http://crypticarticles.files.wordpress.com/2013/06/cli-help.jpg](http://crypticarticles.files.wordpress.com/2013/06/cli-help.jpg)

## Adding A Command ##
As stated above, Easy-Cli uses a plugin architecture. All extension points of the framework can be customized by providing your own plugins. This section shows how to add a new Command plugin and deploy it. It examines the implementation of the hello command using the HelloCmd plugin (deployed with the runtime).

Here are the simple steps for creating your own Command:

  * Create a new Java project in your favorite IDE with a class that implements interface com.cli.ICommand interface present in cli.jat under {CLI\_HOME} directory
  * Export your project as jar (say cli-is-hello.jar) and drop it in directory plugin
  * Voila! You just added your first command to Easy-Cli

### Update File config/config.properties ###
Before your command can be made available in the console, you must let Easy-cli know about it though config.properties which is a java property file where you declare your command and implemented java class.

### Deploy and Test the Command ###
  * Drop the jar file in the plugins/ directory (shown above).
  * Start the Easy-Cli.
  * From the command-line type ‘help’ and you should see your new command listed.

### Comparison with existing open source CLI frameworks ###
  1. Spring Shell
URL  http://www.springsource.org/spring-shell
Limitation : Spring Based Programming model. Lack of Spring knowledge, could lead to a longer learning curve.
  1. Clam Shell
URL https://code.google.com/p/clamshell-cli/
Limitation : If you are using the default implementation of clamshell-cli, the default Controller class makes usage of jCommander (jcommander.org) for parsing command line argument. If you don’t want to use jCommander because of special requirements (whatever that may be), you will have to implement your own Controller class.

### Advantages of Easy CLI over the above 2 ###
Easy Cli doesn’t restrict you to any particular command line arguments parser. Easy cli passes you the command line arguments as is and you are free to use any of the command line argument parser of your choice such as  Jakarta Commons Cli,  JCommander, Martian JSAP etc or write your own parser. This gives flexibility and helps in getting started really fast.