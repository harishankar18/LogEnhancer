Log Enhancer

The current utility used for adding logs to source files of C, C++ and Java. The utility adds logs in multi contexts. 
The current utility tracks logs added and upon completion of the task, it removes all the logs added.

    In the following contexts, it adds logs to the source file.

    1. Track return of values of a specific function or all the functions.
    2. Track the change of the value of a global variable.


Working model

Current utility when it ran, it parses all the source files and generates tags, 
after that, it generates the config file where you can mention the function or variable which needs to be logged.

The priority of the configurations will be current directory and exported project path under that build directory
or the command line option absolute path of the configuration can be specified.

The newly added code can be tracked based on diff functionality with the original version.

The logging handler can be specified based on the language if it is not specified the default handler will be used.
Even the grammar of the logging handle can be specified.


    LOGGING_LEVEL=BASIC,MEDIUM,ADVANCED,VERBOSE                    
    FUNCTIONS=<FUNCTION_NAME> can be separated by the comma(,)
    GLOBAL_VARIABLES=names of the global variables separated by the comma


It uses local disk space for storing the tags information. Once the task is completed there will be command line options to remove all the files and reverting the changes.All the files are 
stored under .loge directory

The directory structure of the loge utility is mentioned below.
    .loge
      |
      +--> svn_diff: tracks the genuine changes done by the user
      |
      +--> tags: tags related to variables and function names are stores here.


These are the command line options supported by the loge utility

    loge            add the logs to sources based on the configuration available
    loge -c, --config    generates the config file.
    loge -r, --revert    reverts all the logs added by the loge utility.
    loge -s, --snuke    reverts all the changes and removes all the hidden files created by the loge utility

Optimization levels

    1. Performance specific
    
        There should be lazy initialization model which skips the generating the tags at the beginning of initialization. If the current model is followed then first time running will take time. If there is possibility of running in the background for 
        generating the tags it will be a win-win situation for both the people.

    2. Language specific
    
        Some optimization levels are specific to the language when while adding an extreme level of logging, it detects read-only branches of the variable and avoids logging in that specific function.
