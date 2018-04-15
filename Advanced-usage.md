# Advanced Gunbot usage

Thanks to community feedback, Gunbot is extendable with tools from many third party devs.

Such tools will usually either interact with Gunbot over websockets, or by providing a config.js for Gunbot to load. When config.js is being overwritten, Gunbot will automatically pick up the changes, without restarting Gunbot manually.

You can also run multiple instances of Gunbot on the same machine. Automation of running Gunbot instances can be done with pm2.

Check the growing list of community resources for Gunbot



## Load external config.js 

You can load config.js from an external location by starting Gunbot manually, and set the external location in an extra parameter. 

Example:

> ./gunthy-linx64 -config=https://gunthy.org/config.js



## Change the port of Gunthy GUI

By default Gunthy GUI works on port 5000, but you can change this to whatever port you want, by opening command prompt in your Gunbot folder and following these steps:



**Windows:**

> set PORT=9000
>
> gunthy-gui.exe



**Linux:**

> PORT=9000 ./gunthy-gui-linx64



**Mac:**

> PORT=9000 ./gunthy-gui-mac



**ARM:**

> PORT=9000 ./gunthy-gui-arm

