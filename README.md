Log Enhancer

The current utility used for adding logs to source files of C, C++ and Java. Utility adds logs in multi contexts. 
The current utility tracks logs added and upon completion of task it removes all the logs added.

	In the following contexts it adds logs to source file.

	1. Track return of values of a specific function or all the functions.
	2. Track the change of value of a global variable.


Working model

Current utility when its ran , it parses all the souce files and generates tags, 
after that it generates the config file where you can mention the function or variable which needs to be logged.

The priority of the configurations will be current directory and exported project path under that build directory
or the command line option absolute path of the configuration can be specified.

Newly added code can be tracked based on diff functionality with original version.

The logging handle can be specified based on the language, if it is not specificed the default handle will be used.
Even the grammer of the loging handle can be specified.


	LOGGING_LEVEL=BASIC,MEDIUM,ADVANCED,VERBOSE					
	FUNCTIONS=<FUNCTION_NAME> can be separated by the comma(,)
	GLOBAL_VARIABLES=names of the global variables separated by the comma


It uses local disk space for storing the tags information. Once the task is completed there will be command line options for remove all the files and reverting the changes.All the files are stored under .loge directory

The directoy structure of the loge utility is mentioned below.
	.loge
	  |
	  +--> svn_diff : tracks the genuene changes done by the user
	  |
	  +--> tags	: tags related to varibles and function names are stores here.


These are the command line options supported by the loge utility

loge			: add the logs to sources based on the configuation available
loge -c, --config	: generates the config file.
loge -r, --revert	: reverts all the logs added by the loge utility.
loge -s, --snuke	: reverts all the changes and removes all the hidden files created by the loge utility



Optimization levels

	1. Performance specific
		There should be lazy initialization model which skips the generating the tags at the begining of initilization.
		If the current model is followed then first time running will take time.
		If there is possibity of running in the background for generating the tags it will be win win situation for both the people.

	2. Language specific
		Some optimization levels are specific to the language when while adding extreme level of logging it detects readonly
		branches of the variable and avoids logging in that specific function.
