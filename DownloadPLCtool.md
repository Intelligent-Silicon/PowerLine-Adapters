# Download Open PLC Utils

Having installed Visual Studio now download the open source program code which compiles into the Toolkit.

Start up Visual Studio.

Click on the ```Clone``` a repository button and fill in these details

Repository Location: ```https://github.com/qca/open-plc-utils```

Path: ```%UserProfile%\source\repos\open-plc-utils```
This translates to a path like this: ```C:\Users\[Your Username]\source\repos\open-plc-utils```

If you have Github installed already on your windows box, specify the path to your github repos and add on suitable folder name like ```\open-plc-utils\```.

Click the ```Clone``` button and wait for the repo to download to the specified folder, this will only take a moment or two.

Once completed you'll be presented with a Setup assistant tabbed window which lists a number of projects that represent each .EXE program found in Open PLC Utils.

In the top right of this tabbed window, click the ```Retarget All``` button, and your see each project change to:
```
Retarget to Platform Toolset (v145), MSVC Build Tools for x64/x86 (Latest)
```
and
``` 
Retarget to Windows 11 SDK (latest).
```

Now click the ```Apply``` button and wait a few seconds.

Now you are ready to build (compile) the source code and make the .EXE programs.

Click ```Build```, then click on ```Build Solution```. 

In the Output pane on the bottom, you should see the progress of the build process. 

If all went well, you should finally see these last few lines in the Output pane.

```
========== Build: 113 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
========== Build completed at 18:27 and took 21.377 seconds ==========
```

You have now successfully built all the .EXE programs. 

You will be able to find all these .EXE programs in the folder ```C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs``` or your Github folder if using [Github Desktop.](https://desktop.github.com/download/).

Now if you are using the folder ```C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs```, it wont be accessible from File Explorer unless you select your Local Disk C:, so navigate to the VisualStudioNetfolder and right mouse click on the ```Programs``` in File Explorer and select Pin to Quick Access menu option. This will put a shortcut to the Programs folder in your Quick Access section in File Exporer, if you have this enabled. 

And if you Microsoft Terminal intalled from the Microsoft (App) Store, you can right mouse click on a blank part of the Programs folder in File Explorer, and choose the menu option Open in Terminal. This will open MS Terminal in the ```C:\Users\[Your Username]\source\repos\open-plc-utils\VisualStudioNET\Programs``` folder so you can run the programs using ```.\[Program Name][Command Line Switches/Flags]``` in future.




