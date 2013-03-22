README
======


Installation
============

By hand
-------

Clone project from git hub into a dir outside your Eclipse workspace:

::

    git clone git@github.com:pellekrogholt/crowdnet.git

Go to that dir *crowdnet* and do a svn check out 

::

    svn co http://simple-quickactions.googlecode.com/svn/trunk SimpleQuickactions 

The crowednet / PreciousCargo depends on the SimpleQuickactions android application (.apk)
which for now is not wrapped up as a jar file.

The rest of the dependencies is added to crowdnet/PreciousCargo/libs

Then import SimpleQuickactions and PreciousCargo as existing Android projects into eclipse (don't copy code into Eclipse workspace).

Thats it.

Additional libs in use
----------------------

- osmdroid (jar) https://code.google.com/p/osmdroid/downloads/list
- gson for android (jar) https://code.google.com/p/google-gson/downloads/list
- logging for android (jar) http://www.slf4j.org/android
- simple-quickactions (an apk) https://code.google.com/p/simple-quickactions/source/checkout


Ant build
---------

Well a *maven* build would probably be niece :)


We didn't succed to get the ant build up and run - here is roughy what we did.

Since its an existing project do:

::

    cd crowednet/PreciousCargo
    android update project -n PreciousCargo -p ./ -t android-17
    ant debug -lib ./libs


This keept raising:

::

    [javac] import org.example.qberticus.quickactions.BetterPopupWindow;
    [javac]                                          ^

We tried to do a check out of the Simple-Quickactions app inside the PreciousCargo
and then set it up as 

::

    cd crowednet/PreciousCargo
    svn co http://simple-quickactions.googlecode.com/svn/trunk simple-quickactions-read-only

That updated fine:

::

    $ android update project -n PreciousCargo -p ./ -t android-17 -s
    Updated project.properties
    Updated local.properties
    Updated file ./build.xml
    Updated file ./proguard-project.txt
    Updated project.properties
    Updated local.properties
    Updated file ./bin/build.xml
    Updated file ./bin/proguard-project.txt
    Updated and renamed default.properties to project.properties
    Updated local.properties
    Added file ./simple-quickactions-read-only/build.xml
    Added file ./simple-quickactions-read-only/proguard-project.txt

But the ant build failed

::

    ant debug -lib ./libs
    ...
    [javac] import org.example.qberticus.quickactions.BetterPopupWindow;
    [javac]                                          ^
    ...



Tried to google/search for how to build with ant having a dependecy on another apk
but didn't find it - perhaps is the right solution that *simple-quickactions* should
be cooked as a jar like they do https://github.com/pellekrogholt/Android-Universal-Image-Loader



We also tried with an ant.properties file - containing:

::

    extensible.classpath=/Users/pelle/dev/android_crowdnet/crowdnet/SimpleQuickactions/bin

well didn't work as well so for now we are stucked to build the app(s) through Eclipse for now.


Ad hoc notes
------------

Uninstall application:

::

    adb shell am start -a android.intent.action.DELETE -d package:com.matter2media.crowdz.preciouscargo


list application and perhaps grep

::

    adb shell pm list packages | grep crowd

