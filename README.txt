FWLog - Fireworks Logging

This library is intended to make developing custom panels for Adobe Fireworks a little bit easier. 
It provides a library of actionscript functions to do logging for the custom panels you develop while they execute inside the Fireworks javascript execution environment.
This is a library of actionscript loggin functions which wrap javascript logging functions.


Get Started

Reference the FWLog.swc contained in the bin folder from your Flash Builder project.
Instantiate the FireworksFileIO project like so:

	var message = "hello Fireworks";

	var fw:FireworksLog = new FireworksLog("console.log");
	fw.log("message: ", message);									//at the moment, the log function can take a maximum of two arguments
	
The API is below:

	public function log(message:String, value:String = ""):void
	
	
The Problem

Fireworks has a 2-tiered development workflow. 
Panels must be written in actionscript. At the same time the Fireworks API provided by Adobe to manipulate and extend Fireworks is javascript.
To execute that javascript, panels must pass it as a string argument to the MMExecute function, eg. MMExecute('alert("hi");');

Besides the development workflow challenges this creates, there are also problems when passing strings as arguments to the javascript functions you will be executing.
This is because those javascript functions are also being passed as a string, so you get into a nested string situation and all the annoyances that this entails like having to escape characters, and writing things like this:

actionscript...

	var greeting = "hello";
	MMExecute('alert("greeting: ' + greeting + '");');

the string being passed to MMExecute is javascript.

This nested string situation is a little bit nightmarish, especially when you have to start dealing with multiple variables, and newlines, which have to be encoded and escaped on their journey through this string maze.
This library takes care of all that for you and lets you just call a log function with the variables and strings you want output.

The Set Up

The FireworksFileIO class embeds FFIO.jsf. When it is instantiated it executes this javascript loading a "fireworks_file_io_library" global variable into the Fireworks javascript environment.
From that point on, that global variable exposes functions which can be called by the actionscript IO functions of the FireworksFileIO object.

Miscellaneous

The lib folder contains the FWLog.swc which FireworksFileIO uses for logging. If you wish to change and recompile FireworksFileIO, you may need to re-reference this swc from your Flash Builder project.



Released under the BSD License.		

