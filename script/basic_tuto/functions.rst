Creating Functions
*******************

Syntax Review
===============
Depending on the type of function you are writing or calling, the syntax will vary.

**Stand Alone Function Declaration:**

.. cpp:function:: function function_name([arg0],...){...}

	Declaration of function
	
	Syntax::

		function function_name([arg0],...)
		{
			statements;
			[return val;]
		}
	
	:param function: Is a keyword telling TorqueScript we are defining a new function.
	:param function_name: Is the name of the function we are creating.
	:param [arg0]: Argument. Value passed into function for use.
	:param ...: Any number of additional arguments.
	:param statements: Your custom logic executed when function is called.

	:return: **return val** *Optional*. The value the function will give back after it has completed.

	Examples::
	
		// Print 0 to value of %repeatCount in console
		function echoRepeat (%echoString, %repeatCount)
		{
		   for (%count = 0; %count < %repeatCount; %count++)
		   {
		      echo(%echoString);
		   }
		}

Calling Functions
===================

Once a function is written, you can call it from script or the console. You only need to know the name of the function and its parameters, if it has any. The **echo** function is the easiest method to start with. It is a stock ConsoleFunction which accepts up to 2 parameters:

**Example**::

	// Print "Hello World" in the console
	// Only passing in 1 argument
	echo("Hello World");

The echo command can actually make use of 2 arguments, depending on your goal:

**Example**::

	// Print "HelloWorld" in the console
	// Passing in 2 arguments
	
	%hello = "Hello";
	%world = "World";
	
	echo(%hello, %world);

If your function does not use arguments, you do not have to type anything in the parenthesis:

**Example**::

	// Function declaration
	function CreateLevels()
	{
	   echo("Levels Created");
	}
	
	// Calling the function
	CreateLevels();

The last way to call a method is invoking a member function. You can call the member functions of an object, such as a Player, using a scoping symbol:

**Example**::

	// Player function "doSomething"
	// %this - The Player class/object
	// %action - String to print out
	function Player::doSomething(%this, %action)
	{
	   echo(%action);
	}
	
	// Create a player object
	%myPlayer = new Player(){...};
	
	// Call "doSomething" member function
	%myPlayer.doSomething("Dance");


Creating the Script
=====================
Now that you know how to declare and call functions, we can create a few examples from scratch. First, we need to create a new script:

#. Navigate to your project's **game/scripts/client** directory.
#. Create a new script file called "sampleFunctions". In Torsion, right click on the directory, click the "New Script" option, then name your script. On Windows or OS X, create a new text file and change the extension to .cs
#. Open your new script using a text editor or Torsion.


Before writing any actual script code, we should go ahead and tell the game it should load the script. Open **game/scripts/client/init.cs**. Scroll down to the **initClient** function. Under the // Client scripts section, add the following:


Execute our new script::

	exec("./sampleFunctions.cs");


Now, let's write an extremely simple function that prints a message to the console. The **echo(...)** function already performs this, but we are going to create a more intuitively named method to work with. Type the following in the script::

	// Print a message to the console
	// Kind of repetitiously redundant
	// %message - The message to print
	function printMessage(%message)
	{
	   echo(%message);
	}


To test your new script:

#. Save
#. Run your game
#. Open the console by pressing the tilde (~) key
#. Type the following, pressing enter after each line::

	printMessage("Of melodies pure and true,");
	printMessage("Sayin, this is my message to you-ou-ou");


Fairly straight forward. From here on, it will be assumed you know how to save your script, run the game, and call functions in the console. Next, let's create a function that takes multiple parameters. Write the following code in your script::

	// Print two separate strings to the console
	// Equally redundant in equality
	// %part1 - First part of message
	// %part2 - Second part of message
	function printAdvancedMessage(%part1, %part2)
	{
	   echo(%part1, %part2);
	}


Run the game and type the following in the console::

	printAdvancedMessage("Singin: dont worry about a thing,", "\ncause every little thing gonna be all right");


In a single function call, the above code will write out two separate lyrics on different lines. Every game always has at least one initialization function. Some even have multiple inits. We can write a function that creates and initializes a few game specific variables. Note, that the variables used here are completely new and not used by stock Torque 3D projects::

	// Change global game variables to default values
	function resetGameVariables()
	{
	   // Game's name
	   $GameName = "Blank";
	   
	   // Player's name
	   $PlayerName = "Player";
	   
	   // Game play type
	   $GameType = "Default";
	}

The above code simply declares three global variables and sets them to default values. Every time this function is called, the same logic will execute. If you were to call this in the console, you will not see anything for output. Let's add a function to do this::

	// Print our game's information to the console
	function printGameInformation()
	{
	   echo("Game Name: ", $GameName);
	   echo("Player's Name: ", $PlayerName);
	   echo("Game Type: ", %gameType);
	}

Save your new script and run the game. In the console, you will need to call the init function before the print function. Invoke the functions in this order::

	resetGameVariables();
	printGameInformation();


Instead of manually setting each variable in the console, we can write a "set" function for our game variables. Add the following to your script::

	// Set the global game variables
	// %gameName - Game's name
	// %playerName - Player's name
	// %gameType - Game play type
	function setGameVariables(%gameName, %playerName, %gameType)
	{
	   $GameName = %gameName;
	   $PlayerName = %playerName;
	   $GameType = %gameType;
	}


Now, you can set your game variables to whatever you wish through a single function call::

	setGameVariables("Ars Moriendi", "Mich", "Survival Horror");

	printGameInformation();

	resetGameVariables();

	printGameInformation();


We will get into creating member functions in a later section of the script documentation. For now, you should know enough about functions to move on. 

Conclusion
============
A large portion of your Torque 3D development will occur in TorqueScript. 90% of that will be writing functions to handle your game play and other logic. With TorqueScript, it is easy to create and use functions without having to recompile the engine.

The information you learned in this doc will be used throughout the rest of the documentation, so make sure you are comfortable in your knowledge of functions. Continue reading to learn more advanced logic and math operators. 

You can download the entire script from this lesson HERE. Save the script as you would any other text file from a website::

	//-----------------------------------------------------------------------------
	// Torque 3D
	// Copyright (C) GarageGames.com 2000 - 2009 All Rights Reserved
	//-----------------------------------------------------------------------------
	
	// Print a message to the console
	// Kind of repititiously redundant
	// %message - The message to print
	function printMessage(%message)
	{
	   echo(%message);
	}
	
	// Print two separate strings to the console
	// Equally redundant in equality
	// %part1 - First part of message
	// %part2 - Second part of message
	function printAdvancedMessage(%part1, %part2)
	{
	   echo(%part1, %part2);
	}
	
	// Change global game variables to default values
	function resetGameVariables()
	{
	   // Game's name
	   $GameName = "Blank";
	   
	   // Player's name
	   $PlayerName = "Player";
	   
	   // Game play type
	   $GameType = "Default";
	}
	
	// Set the global game variables
	// %gameName - Game's name
	// %playerName - Player's name
	// %gameType - Game play type
	function setGameVariables(%gameName, %playerName, %gameType)
	{
	   $GameName = %gameName;
	   $PlayerName = %playerName;
	   $GameType = %gameType;
	}
	
	// Print our game's information to the console
	function printGameInformation()
	{
	   echo("Game Name: ", $GameName);
	   echo("Player's Name: ", $PlayerName);
	   echo("Game Type: ", $GameType);
	}