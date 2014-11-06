Settings (object) (intermediate)
--------------
Settings object can be imported into a project and accessed from QML (Q_INVOKABLE) and c++ (exactly the same way as QSettings, except that I recommend using a pointer to refer to this object instead of calling it directly, but this is not mandatory).

This was done to mimic QSettings but using a JSON file instead. Only the most common functions from QSettings have been implemented. Those are :
- allKeys()
- contains()
- clear()
- fileName()
- remove()
- setValue()
- sync()
- value()

The problem with QSettings is it will crash your headless part if the QSettings file is too big, and that will not happen using JSON. This object was created with headless in mind, you can add a Settings object in both your headless and UI parts and they will stay in sync as soon as one part makes a change to the file.

To add this object to your project, follow these steps :

1- Copy both Settings.cpp and Settings.h to your src folder

2- In your applicationui.hpp, add those lines :

	#include "Settings.h"
	
	private:
 	     Settings *settings;
3- In your application.cpp, add those lines :

	(in constructor)
	settings = new Settings(this);
		...
	QmlDocument *qml = QmlDocument::create("asset:///main.qml").parent(this);
	qml->setContextProperty("_settings", settings);

4- In your PRO file :

	LIBS += -lbbdata


You can see an example how to include Settings object into a project by going at this repository :
https://github.com/RodgerLeblanc/Settings


LICENSE
--------------
The MIT License (MIT)

Copyright (c) 2014 Roger Leblanc

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
