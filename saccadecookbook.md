---
layout: page
title: "Saccade Cookbook"
permalink: https://marcvanwanrooij.github.io/tutorials/saccade
---


PANDA tutorial, for students and coworkers: a recipe to calibrate, detect, and analyze saccades

Easily calibrate, detect, and analyze saccades with PandA. For a more detailed description, visit the other saccade sections, starting with the introduction.

Calibration
First you have to calibrate (see also saccade calibration) by training an artificial neural netwok to learn the relationship between measured voltages and head orientation:

pa_calibrate
(choose the calibration dat-file in the pop-up menu, usually ending in 0000). Then you can calibrate (and low-pass filter) the data-files, by using the button in the pa_calibrate interface (this will calibrate ALL dat-files with the .net-file you got from the pa_calibrate-procedure).

Detection
Then you have to detect (see also saccade detection) with:

 pa_sacdet
(choose an experimental hv-file, usually ending with numbers 0001 and up).

Parameters
Obtain all movement parameters, such as end-point location, reaction time, peak velocity.

 pa_sac2mat
(these will be saved in a mat-file)
Analysis
Finally, you can start some high-level analysis (see also saccade analysis) After all these obligatory steps, you can actually start analyzing the data. This usually involves custom-made analysis functions, suited for your experiment. First you have to load the data:

 load MW-RG-2011-03-02-0001
You will now have a Sac- and a Stim-matrix. The Sac-matrix contains all the movement parameters, the Stim-matrix all the stimulus parameters. You can combine them into a single matrix, containing in each column a relevant parameter, and each row containing a single saccade.

 SupSac = pa_supersac(Sac,Stim,XX,YY);
Note that the XX and YY should be numbers describing the type of stimulus, and the number of that type of stimulus in the trial, e.g.

 SupSac = pa_supersac(Sac,Stim,1,2);
for the second (YY=2) stimulus of type 1 (XX=1, usually an LED) in a trial, or

 SupSac = pa_supersac(Sac,Stim,2,1);
for the first (YY=1) stimulus of type 2 (XX=2, usually a sound) in the trial (you have to check what number is assigned to which stimulus type, by typing:

 help pa_readcsv
in the trial information of the LOG-matrix, line 5).
To plot target location versus response location :

 plot(SupSac(:,23),SupSac(:,8),’k.’);
or

pa_plotloc(SupSac);
