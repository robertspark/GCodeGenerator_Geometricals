# GCode - Generator - Python - LinuxCNC

With this python collection it is possible to create simple geometrical shapes and generate gcode.
You can use this tool set to include it into LinuxCNC AXIS.

**Tested with Python 2.7
Status October 2018 - under development **


## History:


| Version | Description |
|---------|----------------------------------------------------|
|0.1 | initial version with contour circel shape unstable version |
|0.2 | save to file implemented |
|0.3 | new contourRectange & contourHoles |
|0.4 | new contourMillHolesGrid. Milling holes on a grid |
|0.5 | new pocketRoundRectangle |
|0.6 | new contourRoundRectangle |
|0.7 | new pocketCircle |
|0.8 | new pocketRectangle |
|0.9 | new drill holes on a grid |
|0.10 | new smooth a rectangle surface in parallel lines |
|0.11 | new smooth a round surface in a spiral |
|0.12.1 | bugfix release #5, #6, #9, #12a+b |
|0.12.2 | bugfix #13, #14 |
|0.12.3 | bugfix #15, #18(close window, VersionNumber|
|0.12.4 | bugfix #10, ToolID, SpindleSpeed, SpindleDir(CW/CCW|
|0.12.5 | 0.12.5-rc1 Tool & material select implemented 
||not editable via gui, only inside json-file
||bug-fixes cutter compensation
||bug-fixes window size
||bug-fixes Mac Mojave, using ttk.<widgets> instead of TKinter|

## more details in our WIKI
[Wiki](https://github.com/mrRobot62/GCodeGenerator_Geometricals/wiki)


## Example screenshot (more details inside WIKI)
![](https://raw.githubusercontent.com/mrRobot62/GCodeGenerator_Geometricals/master/img/screenshots/V012.5-rc1.png)

## Starting from console
python main.py



# You want to implement new shapes, pockets, surfaces, ... ?
To extend functionality of this tool, there are three things to do

## (1) Extend Menu
To include your new functionality you have to extend the menu.
Open `main.py` and include your stuff here:


```
<snip>
# sub menu Contour
self.ContourMenu = Menu(self.FileMenu)
self.FileMenu.add_cascade(label="Contour", menu=self.ContourMenu)

# Contour - Arc
self.ContourMenu.add_command(label="Arc", command=self.DialogContourArc)
#--------- Insert arc shapes here ---------------------#

#------------------------------------------------------#

# sub menu Drilling
self.DrillingMenu = Menu(self.FileMenu)
self.FileMenu.add_cascade(label="Drilling", menu=self.DrillingMenu)
#--------- Insert drilling shapes here ---------------------#

#------------------------------------------------------#
<snap>
```

Implement a callback function like this:

```
<snip>
#------ Menu callbacks ----------------
    def DialogContourArc(self):
        print "DialogContourArc"
        title = "Contour Arc"
        self.myApp = ContourArc(self.app, self.master, self.frame, title)
        self.myApp.init()
        self.myApp.show()
        pass
#--------- Menu callbacks ---------------------#

#------------------------------------------------------#
<snap>
```

Do not forget to import your new python module like This `from contourArc import *` at beginning of `main.py`

## (2) Implement your new functions
Use `shapeTemplate.py`and make a copy of this file if you like to start more or less from scratch ;-). Alternative make a copy of an existing shape/pocket/... and rename it. Than start with point 1. 

Rename the copy to a approperiate filename like `pocketEveryShapeIKnow.py`

For more complex implementations, take a look into pocketXXXXX.py implementations.

Start with implementing of your code.

1. Change classname
2. Insert/copy your images into `img`folder
3. Insert path & filename in method `def init`
4. Insert your widgets in `def _frmIndividualContent(self)`
5. Insert your gcode generator functionality in `def generateGCode(self):`

**Testing:**
start main.py, if implemenation in menu.py was correct, you should see, your new
function inside menu.

Use your new function. A new window appears. Check your functionality.
With button "GCode" you can check your generated GCODE **before** you do it on your CNC. Use a GCode-Simulator like NCViewer or CAMotics to visualize and simulate your generated gcode.

If everything is ok, **than** start gcode on your CNC

## (3) give our community a chance to participate on your new implementation
upload you implementation to this github repository.
**THANKS**

## Repository status and workstream maintenance

Documentation review: 3 November 2026. This is repository-local status, not an upstream release or deployment acceptance.

### Purpose and function

Easy and simple to use gcode generator written in python, GCode generation with Python

### Current objective

Maintain a clearly documented local copy for authorised evaluation/development, preserving upstream attribution and distinguishing local changes from upstream capabilities.

### Progress and evidence

This is a fork of mrRobot62/GCodeGenerator_Geometricals. Existing upstream documentation and attribution are retained. Local customisation, upstream parity, build success and runtime/hardware acceptance have not been verified in this documentation review.

### Next steps and roadmap

1. Confirm the next owner-approved outcome and reconcile this default branch with the workstream's actual source, test evidence and deployed version.
2. Compare with the upstream project before updating and use an appropriate disposable/non-live test setup.
3. Keep completed/in-progress/blocked work and next actions current here. Broader feature priorities remain for the owning workstream to agree; this update does not invent a feature commitment.

### Documentation chain

Read this README first, then the existing records and source/example entry points below. Listed paths were observed on the inspected default branch; source folders are not test results.

No separate root roadmap/handover was present. Maintain the objective and next actions here until a dedicated, linked record is needed.

- [Upstream repository](https://github.com/mrRobot62/GCodeGenerator_Geometricals)

### Standing instruction for every workstream

Every agent, developer or project workstream maintaining this repository must automatically keep this README current with its purpose/function, agreed objective, dated progress, blockers, roadmap/next actions and links to authoritative records. Update it when these facts materially change, at meaningful milestones and before handback, interruption or completion; do not wait for a separate owner reminder.

Read applicable project instructions, preserve concurrent work and existing attribution/licences, and distinguish source commits from deployed versions and verified results. Link requirements, design, handover, validation and recovery records when they exist rather than creating conflicting copies. If a fact is unknown, say so and identify the next verification action. Check affected links, publish authorised changes and verify the remote commit before claiming completion.

Keep credentials, private infrastructure/access routes, private datasets and confidential material out of public documentation. This instruction does not grant new access, replace project-specific authority or approve untested hardware/live operations. Retain detailed historical evidence in project records/version history rather than an ever-growing README log.
