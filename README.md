# Mach4-ESS-Gathered
A place to store setup and custom scripts as well as documentation spread across the internet

## Programming scripts, macros and gui

My only reason for trying to understand how to program for Mach 4 is to create a version of a manual tool change that I had in Mach 3.
I upgraded to Mach 4 when attempting to fix an issue I had with circles that I could not rule out software being the issue. It is not and was not. I probably need to rebuild my CNC to in case it has shifted over the years and caused some sort of warp that is the actual issue I am having. Not sure, maybe. I cannot do this until I have a shop and then a reason to move my CNC. Until then, I am stuck using Mach 4 in a lesser way. Might as well make it what I need it to be.

### Manual Tool Change Work Offset Macro
The mach3 2010 screenset by ger in all of the forums out there was pretty great. You have 2 touch plates. One being the moveable surface touch plate and another permanently mounted. This allows you to use M6 to change to the next tool and resume your work without having to touch off the surface that may not be there.

My version is straight forward enough, once you get around the programming needed to do so. I have not accounted for blocking during the screen script parts. I know there is a way to do this with modules. I have yet to get into that though.

## Layout of the M6 setup tab
![alt text](https://github.com/ubergeekseven/Mach4-ESS-Gathered/blob/main/M6Files/Annotation%202023-02-18%20093639.png)

There are some extranious things on the screen still. I will be getting rid of things in the future. 
## what is needed, physically to use this setup
A plate somewhere on your machine that is in a fixed position. This is the second plate used to determine the offset z position.

I have a plate thatt is adjustable in height, on an arm. This allows me to get it out of the way during material loading if needed.
I am going to redesign this plate to be mostly printed and have an aluminum plate inset that is connected to the moveable plates outer shell. 

Currently, I sit the moveable plate against the arm to conduct. This can be problematic though and I would prefer a plate that is always connected other than the magnet to the tool.

## M6 Setup Tab - how to use
![alt text](https://github.com/ubergeekseven/Mach4-ESS-Gathered/blob/main/M6Files/Input.png)
When you run my profile you have to do some setup before starting your job:
1) open the M6 setup tab
2) On the left top there are variables to set your probing settings up. 
   - Touch Plate Thickness - used to set the thickness of the moveable plate to subtract from the probing of the surface in step 1
   - First Touch Speed - The speed when finding the first touch 
   - Second Touch Speed - to move slower after finding the plate
   - How far to move up after touching
   - How far to set the probe move to before stopping. I have disabled soft limits of the z in order to be able to call this and enabled at the end
   - 2nd Probing pre-move - after moving to the fixed plate the z axis will move this distance before starting the probing. Allows for getting to the plate faster
   
3) The plate positions section
   - you can enter the MTC position manually in machine coordinates or jog to the place you want to change your tool and press Save MTC Pos. It will move up to z0 machine pos, rapid to the MTC location and then move to the z height it is set to.
   - Fixed Plate Location in machine coordinates. The same thing works here other than it only moves to xy location because tool heights are different. You can use the 2nd Probing pre-move entry to tune this for your job.

Once you have these entered, move the first tool to the location to zero on. Could be your material. You can even use your previous probing using the avid plate if you do this already. Then you will be set at xyz zero already. Does not matter, as long as you have set your z0 for the job. I would have to modify the Probe Sequence Start script to remove the first tool touch for z0 if just using your plate is good enough.

1) Now that the plate is under the tool to zero, press probe sequence start. It will move down adn set z0.
2) The tool will then move to the top of the axis and rapid over to the fixed plate location.
3) Probing will occur here and that value will be stored in a register.

That is it. 
1) Once M6 gets called in gcode, the z will move to the top, rapid to the MTC location and wait for tool change. 
2) Then you click Cycle Start and the z will go to the top and rapid to the fixed plate.
3) this tool will be probed on the plate and this height value will be stored and will set the last touch value to this value. This will change your work offset z value so that the current position is the same value in z as the last. 
4) the z axis will go to the top, restore the settings it stored from before this all started and return to the last location when the M6 was called.
5) Then your post should turn on your spindle and go to the next section of code. 

         
## How to use the files I have provided
Move the screen file into t he screen directory.
Move the profile folder into the profiles folder.

If you want to add everything to your own screenset, you will have to get the scripts from the buttons and copy the m6 code into your m6 macro in the macros folder. 

I would test the setup as is and bring things over once you see what is goingg on in there. I will try and add more things to this github as I come up with them. I spent so much time learning how to deal with this software that I do not want to lose it and I also never want to touch it again. So it may never happen. However, modbus sounds fun. Until I actually go to do it. The journey sucks. The story after is all I care about.



## Videos and links that help to explain how in the world this system works:

https://www.youtube.com/watch?v=TMzAT0eb3p0 - creating modules DazTheGas

https://www.youtube.com/watch?v=8PV-OlcmqH4&list=PL7IitnI6IOQAUp6rOgtcQLwz7U8E4XHvq - All of DazTheGas mach4 videos in playlist 

https://www.youtube.com/watch?v=G85p1VsD3lk - This video describes the layout and operations of how mach4 works. Not super in depth but, a great overview to understand some concepts that are never explained:



https://forum.avidcnc.com/t/mach-4-lua-capabilities/1308 - Long winded thread on avid forum to talk through making something that seems simple at the front of it:


## All of my gathered help files in one place

https://github.com/ubergeekseven/Mach4-ESS-Gathered/tree/main/Mach4HelpFiles


