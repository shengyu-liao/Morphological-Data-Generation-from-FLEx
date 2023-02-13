README-Lookup.txt
09 February 2023

Beth Bryson

Contents
1. Installing the components for the Lookup package
2. Using the Lookup package

1. Install the pieces needed for the Lookup package:

FieldWorks Language Explorer (FLEx) version 9.1.14
	(At the time of writing, there are issues with using FLEx 9.1.18.
	FLEx 9.1.14 is known to work with this version of FLExTools.)
	
	These instructions assume the following are already in place:
	1. You already have FLEx installed
	(from https://software.sil.org/fieldworks/download)
	2. You have a FLEx project with language data in it.
	3. Your project includes a lexicon with some number of roots (marked for 
	Grammatical Category).
	4. You have set up templates for the Grammatical Categories you want
	to generate words for, and have added affixes to the slots in those templates.
	(It may be most straightforward to focus on nouns and verbs to begin with.)
	5. You have entered the appropriate allomorphs and environments for the roots
	and affixes in your lexicon, following principles in the "Introduction to Morphological
	Parsing" document under Help/Resources in FLEx.
	6. To confirm that your morphological description matches what you expect, you
	can create texts in the Texts & Words area containing paradigms, and run the
	parser over them using the command Parser/Parse Words in Text. More details 
	about the parser can be found in Help/Language Explorer and Help/Demo Movies
	(https://vimeo.com/channels/fieldworks),
	starting at video #44: "Using the Parser".

Python:
	(This version of FLExTools doesn't work with Python 3.8 or later. Future versions will.)
	1. Download the Windows installer for Python 3.7.4:
	https://www.python.org/ftp/python/3.7.4/python-3.7.4-amd64.exe 
	2. Run the installer from your user account.
	 - Tick the box for Add Python 3.7.4 to the path.
	 - Make sure the box for "Install launcher for all users" is ticked.
	 - "Install Now" (not "Custom").

FlexTools and custom Lookup modules
	1. Unzip Lookup-FlexTools-2.3.zip into your Documents folder.
	2. Go into the resulting folder (Lookup-FlexTools-2.3). Double click Command.bat
	to install the Python dependencies listed in requirements.txt for FlexTools.
	3. Go to the folder Lookup-FlexTools-2.3/WorkProjects
	4. Duplicate the folder Generate-Words-template
	5. Rename the copy with the name of your language (e.g., Lookup-Spanish)
	6. This will be your project folder. Normally you will start FlexTools from here, and all of your
	output files will be under this folder, in the Build and Output folders.
	7. To verify that everything got installed correctly, go to the Config folder, and
	double click FlexTools.bat, to run FlexTools.
	8. If it runs, then everything is set up. If there is an error, then additional debugging
	is needed to get the system set up.
	9. There is a README.md telling where to get more info about FlexTools.
	10. The custom Lookup routines (not a part of the FlexTools package) are in 
	Lookup-FlexTools-2.3/FlexTools/Modules/Lookup

Setting up to use the Lookup package with your data

2. To run the Lookup routines:
    Initial setup (one time only)
	1. Go into the folder for your project (e.g., Lookup-FlexTools-2.3/WorkProjects/Lookup-Spanish), 
	and double click FlexTools.vbs to start FLExTools
	2. Click Collections, click on Lookup Tools collection, click X to close
	3. Set the Source project to your FLEx project
		- Click the FLEx icon in upper left (colorful cube)
		- Find your project name, double click it
    Setting up for a specific run on the data (repeat for different scenarios)
	4. Configure the settings.
	[There is a module "Lookup Settings Tool" for setting these values, but currently there is a bug.
	For now, just edit the config file by hand: Lookup-FlexTools-2.3/WorkProject/<YourProject>/Config/Lookup.config]
		- Set Target Project to your project name (both source and target should be the same)
		- Set "Limit number of stems" ("LimitStemCount") to a number if you want just a few stems (e.g., 1 or 5, for testing)
		- Set "Limit to specific POS value" ("LimitPOS") if you only want some POS: v, or n,v,
		- Set "Limit to specific Citation Form" ("LimitLex") if you want only a single Headword
		(You can set all three, or only one or two, of these limiting variables.)
	5. Run "Generate all parses from FLEx project in ANA format" module
		- Look in the Output folder for words-uf.txt to find the "parses" of the generated words.
		- The other output formats are also in this folder, including words-SIG.txt for the SIGMORPHON format.
	6. Run "Synthesize Analyzed Text with STAMP" module
		- Look in the Output folder for words-surf.txt to find the surface forms of the words.
	7. These files together constitute a pairing of parses and surface forms of the generated words.
	Use post-processing techniques (e.g. "post-processing.ipynb" in the same GitHub repository)
	to work with these output files for your custom purposes.



