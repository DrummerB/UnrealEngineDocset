# Unreal Engine 4 documentation in Dash

This python script generates [Dash](http://kapeli.com/dash) compatible documentation from the documentation that ships with Unreal Engine 4 in CHM format. As a result, you get one click access to the documentation directly from Xcode, if you're using Dash as your main documentation browser:

[![Imgur](http://i.imgur.com/YVDvGUk.png)](https://www.youtube.com/watch?v=YgmLtp-R1O8)

Xcode's own documentation browser is not (yet) supported, as it uses a slightly more complicated format and I'm using Dash personally. I don't have time for that right now, but if anyone wants to tackle that, just submit a pull request and I'll merge it, thanks! [Here](http://www.simplicate.info/1/post/2013/07/deconstructing-apple-doc-sets.html) is some info on Xcode's format.

# Instructions

1. Get the CHM documentation from:
	- Windows: `C:\Program Files\Unreal Engine\4.x\Engine\Documentation`
	- Mac: `/Users/Shared/UnrealEngine/4.x/Engine/Documentation`
2. Extract the CHM file to HTML. You should get a folder that looks something like this:   

	![Imgur](http://i.imgur.com/BUOvpx1.png)
	
	There are lots of tools that can do this. I used [CHM Decompiler](https://itunes.apple.com/ch/app/chm-decompiler/id476013157?mt=12). The script could probably be expanded to do this on its own using something like [PyCHM](http://gnochm.sourceforge.net/pychm.html), but for now, you have to do this manually.
3. The script uses [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/) to parse the documentation. If you don't have it already, install it:
	
		$ easy_install beautifulsoup4

3. Run the python script to generate the Dash compatible DocSet from the extracted HTML documentation:

		$ python ue4docset.py -n "Unreal Engine" ~/Desktop/API ~/Desktop/UE4.docset
		
	The first path is the location of the extracted HTML documentation. The second path is the output DocSet file. You can define the name of the documentaion as it will appear in Dash, using the -n option.
	
	The process will take some time to parse the entire documentation. On my relatively performant machine it takes around 7 minutes to finish.
4. Go to Dash > Preferences > Docsets. Click the + button and add select the generated .docset file.
	
