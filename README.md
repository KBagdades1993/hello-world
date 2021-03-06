
# Part IIB: 4B25 - Embedded Systems #
# Coursework Activity #6 #
# Kyriacos Bagdades (kb569) & Andreas Theodosiou (at694) #
# St. Edmund's College | Wolfson College #
## FINAL PROJECT GIT REPOSITORY GUIDLINES ## 
**This file contains a brief summary of the project, as well as an overview of this GitHub Repository submission**
**Because of the nature of the project, a 2nd README file was considered redundant and both students' contributions are summarized here**
### Summary ###
---
In this project the **original** aim was to create an emulator model for the MKL03Z32VFK4 MCU, and focusing specifically on its 48MHz ARM Cortex M0+ core.
The KL03 MCU, the Free-scale FRDM board based on the KL03, as well as multiple other MCUs using a Cortex M0+ core, have a wide array of applications in 
embedded systems, which are typically in energy-constrained and mobile environments, with very specific engineering goals. As such, it is paramount for developers
and engineers to be able to test and evaluate programs written for the KL03 remotely, i.e. on the emulator. The emulator was to be build in the **Sunflower Simulator** environment.
Sunflower is an execution-driven full-system hardware emulator for single- and multi-processor systems, so is ideal for this task [1]. However, Sunflower only currently 
supports two different ISAs: the Hitachi SH and the TI MSP430. Therefore, building the emulator for the Cortex M0+ would be of big value to the aforementioned stakeholders.


The individual part of the work of both students {(*kb569*[2] & *(at694)*[3]}, was part of a **joint project** and the tasks were divided to form two individual 
work streams. A reference on the **work-split** is included below, and in both individual reports. 
Given the limited time-frame assigned to this project (20h or work + 5h report-writing), as well as the team members' experience level, a full emulator 
was not deemed possible. *Initial focus*: Develop a model for the ARM Cortex M0+ core, its memory unit and bus architecture, as well as the
 defining ARMv6-M Architecture which it is based upon. Additionally, the register & stack definition for the KL03 would also be implemented, along with 
the external memory element and the necessary network interfaces & communication media interconnecting the elements. 

#### Scope Update ####
Due to time constraints and after multiple discussions with the module leader, it was decided that even the reduced workload (after Submission #5) was not
feasible in the given timeframe. As such, the aims of the work were re-evaluated to essentially include the instruction decode (ID) and execute (EX) for the
target architecture (Arm v6-M) and perform the integration with sunflower. For a demonstration, it was agreed that if time allowed and the emulator did compile, 
a short program in c would be written, and using the executable's obj-dump, the minimal set of instructions would be encoded, to showcase that the compilation in
sunflower did execute properly. 

The contents of the practical work are found below and in more detail in the **individual reports**. The decoding was achieved fully, bar the implementation of 
the 32-bit Thumb instruction set &rarr; all instructions in the 16-bit encoding are decoded correctly. The relevant register definitions, state variables and
instruction sets (e.g. in little-endian-arm-v6-m.h, instr-arm-v6-m.h) were **fully** defined, again bar 32-bit encoding. A simple program in c was generated and
the object file dump revealed which instructions (from the ARM v6-M ; A cross compiler was used) were needed. The implementation of the functions in op-arm-v6-m.c 
(the execution stage) was not completed due to time constraints, but the outline is there and can be easily completed (9 functions were implemented). Finally, the 
pipeline stage of ID-> EX was only implemented for 1 instruction format, to showcase completeness in the report. Further work is needed in this, and the rest of the neglected 
areas of the pipeline to complete the emulator. 

### Research ###
---
The initial part of the work involved reading through the Sunflower manual [1], the Cortex M0+ and ARMv6-M reference manuals to gather the knowledge of how the simulator operated 
and what edits were necessary. Additionally, the *source code* of the sunflower simulator was studied extensively in parallel with the Hitachi SH7708 Series processor datasheet and
Super-H SH3 family Software Manual. This part was crucial in understanding the principles behind the implementation in Sunflower. 

### Practical Work ###
---
The practical goals were described above: Building an emulator for the ARM Cortex M0+ core, specifically its Arm v6-M ISA, focusing on ID and EX. 
This was to be done on the Sunflower simulator platform, and would be a structured process, involving research, reverse engineering of existing architectures (SuperH, MP430) and creation of necessary files in sunflower. 
Due course, it was found that the amount of work was not feasible within the project timeframe and as such the work was restructured as follows: The focus would be on ensuring the correct pipeline was implemented for
the **ARM v6-M** for the sunflower simulator, whose native repository is as found in https://github.com/physical-computation/sunflower-simulator
.


The AMR v6-M ISA uses Thumb Instructions (32 & 16 bit). In this implementation, the focus was only on the 16-bit Thumb instruction set.
The implications of this were discussed in the individual reports. The list of altered files needed for the implementation of the emulator is given in the
deliverables section below. The details are found in the individual reports. 
The demonstration involved the creation of a simple c-program that performed a limited functionality routine. In this case, it was a summation of 5 
numbers in an array. The compiler was set 
to compile for the Arm v6-M ISA. An executable was generated and its obj-dump contents were used to identify which instructions were needed in the program.
This was to reduce the amount of work in execution scripts so that to account for the limited time. 
The initial aim was to implement all of the required instructions in op-arm-v6-M.c 
but time constraints did not allow for full implementation. In the reports, an example of a pipeline flow as implemented is described, showcasing how all
the different parts of the code are interconnected. For reference, refer to the ARM v6-M Architecture Reference Manual [4] and the Cortex M0+ Technical Reference manual [5].


### Deliverables --> This Repository ###
---
In this repository, the whole sunflower simulator folder is found (as forked from https://github.com/phillipstanleymarbell/sunflower-simulator). Within the existing code base, the following programs have been added **(new)**:
- decode-arm-v6-m.c : **full implementation - excluding 32-bit Thumb set**
- regs-arm-v6-m.h : **full implementation - for little endian**
- little-endian-arm-v6-m.h : **full implementation - excluding 32-bit Thumb set**
- pipeline-arm-v6-m.h : **full implementation**
- regaccess-arm-v6-m.c : **full implementation - of reg_read, reg_set**
- instr-arm-v6-m.h : **full implementation - excluding 32-bit Thumb set**
- decode-arm-v6-m.h : **full implementation - excluding 32-bit Thumb set**
- op-arm-v6-m.c : **Incomplete implementation - only 9 functions implemented**
- pipeline-arm-v6-m.c : **Incomplete implementation - File virtually untouched, only the ID-> EX push of the SHIFT instruction format was done**


Additionally, source code files native in Sunflower were also edited to aid implementation:
- bit.h : **full implementation - new bit-fields added. May be revisited for 32-bit IS** 
- machine-arm-v6-m.h : **Variable/structure Definitions - Further Work needed**
- main.h : **Variable/structure Definitions - Further Work needed**

Refer to the individual reports for more details on the above. 

* **Note**: The README.md (this), summarizing the project and describing the deliverables. 
### Work Split and Time management ###
---
In the initial two submissions (Items #2 and #5) the split of work was well-defined. However, due to time constraints and the continuous 
change of the scope of work, in practise the split of work changed significantly between different areas throughout the project. It can be confirmed, that
both students contributed in all parts of the code, and all parts of the research, but inevitably different focus was placed in different areas. Comments are also 
in the reports. 
A programming method followed throughout was:
- One student did the bulk of the research on one aspect (say instruction formats) and comprised pseudo code for the implementation (say for decode-arm-v6-M).
- The other student cross referenced the sunflower implementation and used the prepared pseudocode to write the actual file in c.
This method allowed the group to maximise efficiency and time management. 


#Time#


A note on time has to be included. The guidelines for the time to be spent on the project was **25 hours &rarr; 20 h for the Work and 5 h for report writing (approx.).**
In practise this was far exceeded. It is estimated that at least **45-50 hours** were spent on the work and **8-10** for the report writing and submission. This note is included
to explain as to why the emulation was not fully completed, and also as reference for future projects aiming to peform a similar task.  

### References ###
---
1. Phillip Stanley-Marbell and Diana Marculescu. “Sunﬂower: Full-system, Embedded, Microarchitecture Evaluation”. In *Proceedings of the 2nd International Conference on High Performance Embedded Architectures and Compilers. HiPEAC’07*. Ghent, Belgium: Springer-Verlag, pp. 168–182. ISBN: 978-3-540-69337-6.
2. Kyriacos Bagdades (email: kb569@cam.ac.uk).
3. Andreas Theodosiou (email: at694@cam.ac.uk).
4. ARM. (2007). ARMv6-M Architecture Reference Manual, 1–1138. https://doi.org/ARM DDI 0406C.c
5. Limited, A. R. M. (2012). Cortex -M0 + Revision: r0p1- Technical Reference Manual
