# Mach4-ESS-Gathered
A place to store setup and custom scripts as well as documentation spread across the internet

## Programming scripts, macros and gui

My only reason for trying to understand how to program for Mach 4 is to create a version of a manual tool change that I had in Mach 3.
I upgraded to Mach 4 when attempting to fix an issue I had with circles that I could not rule out software being the issue. It is not and was not. I probably need to rebuild my CNC to in case it has shifted over the years and caused some sort of warp that is the actual issue I am having. Not sure, maybe. I cannot do this until I have a shop and then a reason to move my CNC. Until then, I am stuck using Mach 4 in a lesser way. Might as well make it what I need it to be.

### Manual Tool Change Work Offset Macro
The mach3 2010 screenset by ger in all of the forums out there was pretty great. You have 2 touch plates. One being the moveable surface touch plate and another permanently mounted.

Before starting a multi tool job you would touch off the moveable plate. Then the tool moves to the fixed plate and touches. Gathering the z0 of the first tool and then the difference between the two locations. 

The second number is stored and recalled later.

M6 comes up in gcode and the tool moves to a tool change position.

Change tool.

Tool moves to fixed plate.

Touch off and record that position.

determine if the tool is shorter or longer by compairing the new touch location to the old one. if new < old subtract from old. Take difference and subtract from current work offset z.

if old < new take difference and add to current work offset z.

new touch position z replaces the first one and that is the new number used in the next tool change if needed.

return to last work position and start next section of gcode.


## Videos and links that help to explain how in the world this system works:

https://www.youtube.com/watch?v=TMzAT0eb3p0 - creating modules DazTheGas

https://www.youtube.com/watch?v=8PV-OlcmqH4&list=PL7IitnI6IOQAUp6rOgtcQLwz7U8E4XHvq - All of DazTheGas mach4 videos in playlist 

https://www.youtube.com/watch?v=G85p1VsD3lk - This video describes the layout and operations of how mach4 works. Not super in depth but, a great overview to understand some concepts that are never explained:



https://forum.avidcnc.com/t/mach-4-lua-capabilities/1308 - Long winded thread on avid forum to talk through making something that seems simple at the front of it:


## All of my gathered help files in one place

https://github.com/ubergeekseven/Mach4-ESS-Gathered/tree/main/Mach4HelpFiles


