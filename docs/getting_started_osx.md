# TOC

* [System Prerequisites](#system-prerequisites)
* [IntelliJ make use of GraalVM](#intellij-make-use-of-graalvm)
* [TroubleShooting 'Choose Runtime'](#troubleshooting-choose-runtime)
* [Use Oracle Native-Image at OSX Catalina](#use-oracle-native-image-at-osx-catalina)
* [Exports](#exports)
* [Cool Stuff](#cool-stuff)
* [Official GraalVM Docs](https://www.graalvm.org/docs/)

____


## System Prerequisites
* install XCode [Xcode](https://apps.apple.com/de/app/xcode/id497799835?mt=12)
* xcode-select --install
* install: [intellij](https://www.jetbrains.com/de-de/idea/download/#section=mac)
* install brew: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
* zlib-devel : `brew install zlib` (needed?)
* glibc-devel osx catalina: `brew install glib` (needed?)
* install: graal vm via brew: `brew cask install graalvm/tap/graalvm-ce-java11`
* locate the directory of graalvm-ce-java11 and run:
* `export GRAALVM_DIR=/Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0/Contents/Home`

## IntelliJ make use of GraalVM

* install plugin: '**Choose Runtime**'
* restart intellij
* click on Menu: Help -> Find Action
* type: Choose Runtime
* select: Graal-VM

#### TroubleShooting 'Choose Runtime'
If it not start, modify: idea.jdk at, for example: Users/MyUserName/Library/Preferences/IntelliJIdea2019.3/idea.jdk
* edit: `sudo vi  ~/.bash_profile`
* edit: `vi  ~/.zsh`
* maybe solves permissions: `sudo xattr -r -d com.apple.quarantine /Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0`
* check Java default VM: `/usr/libexec/java_home -V`
* or `java --version`
* 


java -cp /Users/$(whoami)/GraalVM/native-image-installable-svm-java11-darwin-amd64-19.3.0.jar \  
  com.mycomp.myproj.dir2.MainClass2 /home/myhome/datasource.properties /home/myhome/input.txt

## Use Oracle Native-Image at OSX Catalina

* Download for example:
  * https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-19.3.0/native-image-installable-svm-java11-darwin-amd64-19.3.0.jar

* extract the file with [The Unarchiver](https://apps.apple.com/de/app/the-unarchiver/id425424353?mt=12)

inside the archive you will find:
/Users/$(whoami)/GraalVM/native-image-installable-svm-java11-darwin-amd64-19.3.0/lib/svm/bin/native-image

1. open your Terminal:
2. type: chmod a+x /Users/$(whoami)/GraalVM/native-image-installable-svm-java11-darwin-amd64-19.3.0/lib/svm/bin/native-image
3. and then execute it:
4. `/Users/$(whoami)/GraalVM/native-image-installable-svm-java11-darwin-amd64-19.3.0/lib/svm/bin/native-image`
5. then it pop up an alert to delete the file
6. click on cancel
7. open your Preferences -> Security & Privacy -> click on "open"
8. execute on your Terminal it again

Now you will see a line like this:
`Please specify options for native-image building or use --help for more info`

* repeat the step 2 for "rebuild-images"

*Note: If you open your finder and right click: "COPY" the file you can past the full path into your Terminal.App

## Exports
* `export GRAALVM_DIR=/Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0/Contents/Home`
* `export JAVA_HOME=/Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0/Contents/Home`
* `export PATH=/Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0/Contents/Home/bin/:$PATH`
* `/usr/libexec/java_home -v 11.0.5` (set this if GraalVM is 11.0.5, check with: `/usr/libexec/java_home -V` )
* `export LLVM_TOOLCHAIN=$(lli --print-toolchain-path)`
* double check path: `echo $PATH` (fix it if needed)
* set exports into zsh and bash profile [see troubleshooting](#troubleshooting-choose-runtime)

* my `sudo vi  ~/.bash_profile`
``export JAVA_HOME=$(/usr/libexec/java_home -v 11.0.5)
export PATH=/Users/${whoami}/GraalVM/graal/mx:$PATH
export GRAALVM_DIR=/Library/Java/JavaVirtualMachines/graalvm-ce-java11-19.3.0/Contents/Home
export PATH=$GRAALVM_DIR:$JAVA_HOME/bin:$PATH
export LLVM_TOOLCHAIN=$(lli --print-toolchain-path)``

* fck: no idea at moment to run without a new re/login you need to run this: `source ~/.zsh`

## Install GraalVM

* some Oneliners
`wget -O - https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-19.3.0.2/native-image-installable-svm-java11-darwin-amd64-19.3.0.2.jar | gu -L install llvm-toolchain-installable-java11-darwin-amd64-19.3.0.2.jar`
`wget -O - https://github.com/graalvm/graalvm-ce-builds/releases/download/vm-19.3.0.2/llvm-toolchain-installable-java11-darwin-amd64-19.3.0.2.jar | gu -L install llvm-toolchain-installable-java11-darwin-amd64-19.3.0.2.jar`

* []()
* open your Terminal.app
* gu -L install llvm-toolchain-installable-java11-darwin-amd64-19.3.0.jar

* gu install native-image
* gu install R
* gu install python
* gu install ruby
* gu install llvm-toolchain

## Cool Stuff
* [https://quarkus.io/guides/building-native-image](https://quarkus.io/guides/building-native-image)
* [https://github.com/quarkusio/quarkus-quickstarts.git](https://github.com/quarkusio/quarkus-quickstarts.git)



