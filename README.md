# MUD @desc ANSI
Create ASCII/ANSI art and export to **.asc** and **.ans** files as well as ready-to-use MUD/MUSH/MUX/MOO **@description**

This software is mainly an aid to make MUD/MUSH/MUX/MOO games fancy looking by adding not just a simple text description (**@desc**) to each room, but to create an ASCII/ANSI art and show it as the description of the room so that the users have a graphical presentation of the game scene using only their ANSI-capable terminals.
Certainly the created ASCII/ANSI art can be saved as a simple file too.

There are two kinds of ANSI art You are able to create with this software:
- Colorized ASCII art, that is basically an ASCII art pimped up with colors
- Multicolored pixel art that is rather a rough representation of a picture

In the below chart You can find a summary about the basic differences between them.

Subject | Colorized ASCII art | ANSI Pixel art
----------|--------------------------|-------------------
Colors | Limited to 16 FG and 8 BG colors, although BG often left black | Even without 256c ANSI terminal support, using only 16 colors it can go up to theoretical 640 colors, taking out repetitions it gives You 273 different colors
The graphics | Comprehensive even without colors (viewed in ASCII mode) as the art is represented by the characters themselves, the coloring just makes it more fancy | Can not be viewed in ASCII mode, as it only gives You a meaningless pattern of grey-ish squares
Creation | As a conclusion of above, the ASCII art is drawn first, then it can be colorized to make it fancy and save as ANSI | Most probably it is converted from an image format that has palette support ("Indexed Mode" in Gimp). Hand drawing from scratch is painful. Just fine cosmetics on existing ANSI art is recommended
Required Charset | Simple ASCII charset (0-127) is enough to represent any graphics | Unicode or similar charset is required as "25% - 50% - 75% - 100% filled hatch" character is used to mix colors, creating a fake "multi-color" feeling
MUD capability | Appropriate for MUD as only basic ASCII characters are used | Most probably inappropriate for MUD as it requires UTF-8 or UTF-16, most MUDs don't support BG color, and **@desc** tends to be too long to display the whole art

So let's check how the above two are supported by this software:

-----

## Colorized ASCII art

![Screenshot](https://github.com/oliverbacsi/MUDdescANSI/blob/master/help/Col_ASCII.png)

You have two options to start with:

* Either with a blank ASCII art:
> Menu --> File --> New drawing

* Or importing an existing ASCII art to colorize it:
> Menu --> File --> Load ASCII

During ANSI art editing it is recommended to use the right sidebar of the main window for selecting between the 16 FG colors, optionally between the 8 BG colors, and You can specify the drawing character in the bottom-right corner text field (the first character is used for drawing).
Do not use any of the hatch buttons, they will put UTF-8 characters into Your ASCII art.
It is recommended to set up the software to edit all attributes separately: Uncheck the following box:
> Menu --> Preferences --> [ ] Left click to set all attributes at once

This case the main editor window works like following:
- *Left click*: Change only the FG color of the clicked character to the currently active FG color, and leave everything else intact
- *Right click*: Change only the BG color of the clicked character to the currently active BG color, and leave everything else intact
- *Middle click*: Change only the Face of the clicked character to the currently active drawing character (text field in bottom-right corner), and leave all colors intact

This enables You with a fine and precise editing capability of Your ANSI art.

-----

## ANSI Pixel art

![Screenshot](https://github.com/oliverbacsi/MUDdescANSI/blob/master/help/ANSI_pix.png)

Forget about setting drawing characters or FG/BG colors. Use one of the multi-colored palettes to pick a color, and the software will select the appropriate FG/BG color and Unicode "Hatch" character for You to use. Don't change FG/BG color or drawing character manually unless You really want to. Just select a color and draw the pixel.
Therefore it is recommended to set up the software to edit all attributes at once: Check the following box:
> Menu --> Preferences --> [X] Left click to set all attributes at once

This avoids You having to click each editor cell 3 times: Left click, Right click, Middle click. A simple left click will draw the cell to the desired color:
- *Left click*: Change FG color, BG color, and change the character face to the appropriate Hatch

####It is recommended to use one of the two multi-color picker palettes:

**1) The RGB color picker:**
> Menu --> Tools --> RGB color picker

This will show You a second window with three color grids. Each grid represents how the current drawing color would be fine-tuned if one of the color components (red/green/blue) was left intact and the other two changed between min and max. You will see only discrete colors rather than a continuous color gradient as the 16 FGs, the 8 BGs, and the 25% Hatch opacity steps will only give You certain color combinations. Any color picking will change all 3 grids as the new color will be represented how it would look like fine-tuned.

**2) The 273 color palette:**
> Menu --> Tools --> 273 color picker

A simple square of 16 FG x 8 BG x 5 Hatch color combinations showing all possible colors in one picker window. The above multiplication gives You 640, but these are in reality 273 different colors, as for example all below combinations will give You cyan color:
- BG = cyan , Char = Space , FG = can be any of the 16
- FG = cyan , Char = 100% full hatch , BG = can be any of the 8
- FG = cyan , BG = cyan , Char = can be any percent Hatch
- BG = blue , FG = green , Char = 50% hatch
- BG = green , FG = blue , Char = 50% hatch
- etc...

-----

## Other controls of the software

Under the main editing window there is a small text field: You can optionally enter the MUD room description here, this will be appended after the ANSI art in the @description.

There is a possibility to specify if the software should return the attributes to normal at each end-of-line, or leave the color attributes as they are. Both can have advantages and disadvantages.
Not turning off color attributes at "EOL" might result that a colored bar is drawn to the right edge of the screen as the "Carriage Return" character will have its own color attribute as well.
Turning off color attributes at "EOL" might result that You have to turn the same attributes on again at the beginning of the line unnecessarily, making the @desc grow like hell...
> Menu --> Tools --> Preferences --> [X] Reset color to normal at each EOL

In case You are using the software for ASCII/ANSI art only and don't need the MUD room description under the ASCII/ANSI, then either don't fill the Description cell under the drawing area, or You can configure the software to output the Description only to MUD/MOO files but not for ASCII/ANSI:
> Menu --> Tools --> Preferences --> [ ] Export @desc row for ASCII and ANSI too

In the File menu You can Load an existing drawing, Save Your current drawing, or start a New one where You have to specify the width and height only. Drawings are saved as *.dat* files in the "data/" folder.
In the same menu You can import existing ASCII art to colorize. This will be looked up in the "imports/" folder as *.asc* or *.txt* files as default.
When finished working You can export to result from the File menu. Check the results in the "exports/" folder as *.asc , .ans , .mux , .moo* files. The *.mux* files have the single-line syntax with "%r%h" style coloring. The *.moo* files are exported to be able to copy into the client window as multi-line editing in "notedit / say" style.

-----

## BUGS and Still to do:

- [ ] Background color support for MUD?
- [ ] Some more comprehensive GUI would be better
- [ ] Some in-line help window would be desirable
- [X] Last EOL character is read back from *.dat* files into the @desc field unneccessarily
- [X] Similarly to ASCII import it would be nice to have ANSI file import as well (convert back *.ans* to *.dat*), so that users could load ANSI art from someone else to work on further
- [X] MUD descriptions are collapsing leading spaces, so may be worth to push out the first attribute tag to the start of the line
- [X] Need to escape the backslash and double-quote with a backslash in MUD descriptions...
