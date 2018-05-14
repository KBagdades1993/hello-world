
# Part IIB: 4B25 - Embedded Systems #
# Coursework Activity #6 #
# Kyriacos Bagdades (kb569) & Andreas Theodosiou (at694) #
# St. Edmund's College | Wolfson College #
## FINAL PROJECT GIT REPOSITORY GUIDLINES ## 
** This file contains a brief summary of the project, as well as an overview of this GitHub Repository submission**
### Summary ###
---
In this project the **original** aim was to create an emulator model for the MKL03Z32VFK4 MCU, and focusing specifically on its 48MHz ARM Cortex M0+ core.
The KL03 MCU, the Free-scale FRDM board based on the KL03, as well as multiple other MCUs using a Cortex M0+ core, have a wide array of applications in 
embedded systems, which are typically in energy-constrained and mobile environments, with very specific engineering goals. As such, it is paramount for developers
and engineers to be able to test and evaluate programs written for the KL03 remotely, i.e. on the emulator. The emulator was to be build in the **Sunflower Simulator** environment.
Sunflower is an execution-driven full-system hardware emulator for single- and multi-processor systems, so is ideal for this task [1]. However, Sunflower only currently 
supports two different ISAs: the Hitachi SH and the TI MSP430. Therefore, building the emulator for the Cortex M0+ would be of big value to the aforementioned stakeholders.
The individual part of the work of both students {(*kb569*[2] & *(at694)*[3]}, was part of a **joint project** and the tasks were divided to form two individual work streams. 
Given the limited time frame assigned to this project (20h or work + 5h report-writing), as well as the team members' experience level, a full emulator 
was not deemed possible. Instead the focus was on developing a model for the ARM Cortex M0+ core, its memory unit and bus architecture, as well as the defining 
ARMv6-M Architecture which it is based upon. Additionally, the register & stack definition for the KL03 would also be implemented, along with the external memory element 
and the necessary network interfaces & communication media interconnecting the elements. In terms of work breakdown, I was assigned on modeling the ARM ISA on sunflower, 
along with the external memory element of the KL03, its register definitions and stack location. 

Reasearch
---
The initial part of the work involved reading through the sunflower manual, the Cortex M0+ and ARMv6-M reference manuals to gather the knowledge of how the simulator operated 
and what edits were necessary. Additionally, the *source code* of the sunflower simulator was studied extensively in parallel with the Hitachi SH7708 Series processor datasheet and
Super-H SH3 family Software Manual. This part was crucial in understanding the principles behind the implementation so that . 

Practial Work
---
The focus of the work will be on the development of a prototype MKL03Z32VFK4 micro-controller emulator, specifically its Cortex-M0+ core, SPI peripherals, and memory sub-system, as a full emulator was deemed not feasible within the time-frame given.
This will be done on the Sunflower simulator platform, and will be a structured process, starting by first defining the ISA and emulation of the Cortex-M0+. The individual project will form part of a joint project with another student (at694). 
EDIT: Due course, it was found that the amount of work was not feasible within the project timeframe and as such the work was restructed as follows: The focus would be on ensuring the correct pipeline was implemented for the Cortex M0+ ARM ISA, which
 is the **ARM v6-m.** From the sunflower repository as found in https://github.com/physical-computation/sunflower-simulator. 
>>>>>>> f9a9de105fcdaf54c1b7756189bb6f560cd09cab


Deliverables --> This Repository
---
#References#
1. Phillip Stanley-Marbell and Diana Marculescu. “Sunﬂower: Full-system, Embedded, Microarchitecture Evaluation”. In *Proceedings of the 2nd International Conference on High Performance Embedded Architectures and Compilers. HiPEAC’07*. Ghent, Belgium: Springer-Verlag, pp. 168–182. ISBN: 978-3-540-69337-6.
2. Kyriacos Bagdades (email: kb569@cam.ac.uk).
3. Andreas Theodosiou (email: at694@cam.ac.uk).