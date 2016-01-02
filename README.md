r3e-open-championship
=====================

Open Championship Statistics for [R3E](http://game.raceroom.com)
© 2015 by Christoph Kubisch

### About

This is a small tool that parses the raceresult file from R3E and generates a tiny database and a html report for a championship based on multiple single race events (single- or multiplayer). It is not supported nor in anyway endorsed by the creators of R3E.

The tool supports either the raceresults.txt generated by R3E or json files by the server api.

![sample output](https://github.com/pixeljetstream/r3e-open-championship/blob/master/doc/samplesm.png)

As you can see at this [full sample website](http://htmlpreview.github.io/?https://github.com/pixeljetstream/r3e-open-championship/blob/master/doc/sample.html) it generates for every race:

* Driver Standings
* Team Standings (if more than one team)
* Vehicle Standings (if more than one vehicle type)
* Best Race Lap Times
* Best Qualification Times
* Detailed Race Results

### How it works

Run the ".exe" file, it should bring up a very simple program that you keep running while doing singleplayer races in R3E.

![ui](https://github.com/pixeljetstream/r3e-open-championship/blob/master/doc/ui.png)

* The program tracks edits to "My Documents/My Games/SimBin... raceresults.txt" which contains the results of the last completed race (no matter what kind of race it was).
* Based on the content of the file a unique "championship" is created (hash based on starter-field). That means if you choose always the same starter-field config (vehicle class and number of opponents) in your single player race, it shall treat it as a single championship
* For every completed race, the results are appended to the championship file (a simple text file storing the results for every race) and a HTML file is generated with the current standings, see image above

It is an "open" championship, as none of the settings are really frozen (AI...), you can keep going and mix tracks however you want, a pseudo championship based on your single player races. Simply delete the appropriate database lua file in the "results" directory to start fresh again.

* Edit the override database key to collect multiplayer races into a custom season database, just enter a filename compatible text here. There
is no compatibility check when a race is appended, so keep organized :)

### Commandline mode

In commandline mode, the ui is not started and core functionality is exposed.

* `-addrace dataBaseFile raceresultsFile`
  Appends the race to the provided database file (no error checking whether it 
  contains drivers from the race or not).

* `-makehtml dataBaseFile htmlFile`
  Generates html results for the provided database file
  
For example:

`r3e-open-championship.exe -addrace season1.lua 201511030659.json -makehtml season1.lua season1.html`

One should prefer using luajit as startup, as it will print error outputs to console, while the above doesn't.

`luajit.exe r3e-open-championship.lua -addrace season1.lua 201511030659.json -makehtml season1.lua season1.html`

### History

Time-line for some distinct features

*  7.11.2015 - json result support to improve multiplayer usage
* 20. 6.2015 - multiplayer-friendly commandline options, and database override
* 14. 6.2015 - modified css styles a bit, allow position-based color-coding
* 13. 6.2015 - added icons for tracks and vehicles
* 16. 1.2015 - added optional description string for a championship
* 10. 1.2015 - added qual times, race results and driver standings with positions
*  9. 1.2015 - added team and car standings, as well as best laptimes
*  4. 1.2015 - first release, track multiple championship, html report for driver standings

### A few caveats

Simply do not run the app if you do races you don't want to track. If something is accidentally added somewhere you can always manually delete or edit the files and remove the last entry.
Since the tracknames are not stored in the result file (only track lengths), there needs to a mapping, which may be incomplete. Please send in tracklength-name pairings if you recgonize some are missing (then only the tracklength is printed).

### Third Party

Special thanks to **tAz-07** and **heppsan** from steam community on feedback and providing most of the track mappings.

The icons are directly linked to the official game website.

The exe and wx dll were compressed via upx, the exe automatically executes the r3e-open-championship.lua file.

* [wxLua](http://wxlua.sourceforge.net/)
* [md5.lua](https://github.com/kikito/md5.lua)
* [upx](http://sourceforge.net/projects/upx/)
* [cjson](http://www.kyne.com.au/~mark/software/lua-cjson.php)
* [luajit](http://luajit.org/)
