<pre>This is a primary tree starting at the program main_nems (https://github.com/NOAA-EMC/NEMS/blob/develop/src/MAIN_NEMS.F90)

main_nems
+-CHECK_ESMF_PET(Check if we want ESMF PET files or not)
|
+-ESMF_Initialize(Initialize the ESMF framework, ESMF Virtual Machine, Set up the default calendar)
|
+-MPI_Get_processor_name(Get the processor host name, PROCNAME PROCNAME_LEN)
|
+-ESMF_VMGet(Extract the MPI task ID, The ESMF Virtual Machine, The local MPI task ID)
|
+-w3tagb(Print subversion version and other status information)
|
+-rusage%start(Start gathering resource usage information,MPI_COMM_WORLD,PROCNAME,PROCNAME_LEN)
|
+-ESMF_LogSet(Set up the default log, flush and trace)
|
+-ESMF_ConfigCreate(Create and load the Configure object -- contents of the Main configure file, CF_MAIN)
|
+-ESMF_ConfigLoadFile(The Configure object, The name of the configure file)
|
+-ESMF_GridCompCreate(Create the NEMS Gridded Component, create and control ATM, OCN, ICE, etc. name, configFile)
|
+-ESMF_GridCompSetServices(Register NEMS gridded component Initialize, Run and Finalize, NEMS_GRID_COMP, NEMS_REGISTER)
|
+-ESMF_TimeIntervalSet(Set up Time Step Interval in Main Clock, TIMESTEP, TIMESTEP_SEC_WHOLE, 
|                      TIMESTEP_SEC_NUMERATOR, TIMESTEP_SEC_DENOMINATOR)
+-ESMF_ConfigGetAttribute(CF_MAIN, read starting Year, Month, Day, Hour, Minute, Second)
|
+-ESMF_TimeSet(Set the Forecast Start Time, STARTTIME, YY, MM, DD, HH, MNS, SEC)
|
+-ESMF_ConfigGetAttribute(Extract Forecast Length, CF_MAIN, NHOURS_FCST, nhours_fcst)
|
+-ESMF_TimeIntervalSet(Set the Forecast Length, RUNDURATION, NSECONDS_FCST)
|
+-ESMF_ClockCreate(Create the Main Clock, CLOCK_MAIN, TIMESTEP, STARTTIME, RUNDURATION)
|
+-ESMF_StateCreate(Create the NEMS Import/Export States, NEMS_IMP_STATE, NEMS_EXP_STATE)
|
+-ESMF_GridCompInitialize(Execute the NEMS Component Initialize Step, NEMS_GRID_COMP, NEMS_IMP_STATE, 
|                         NEMS_EXP_STATE, CLOCK_MAIN, phase, userRc)
+-ESMF_GridCompRun(Execute the NEMS Component Run Step, NEMS_GRID_COMP, NEMS_IMP_STATE, 
|                         NEMS_EXP_STATE, CLOCK_MAIN, phase, userRc))
+-ESMF_ConfigGetAttribute(CF_MAIN, RUN_CONTINUE, hh_start, hh_final, Ensemble Clock Parameters)
|
+-ESMF_TimeIntervalSet(Re-set the clock after the ensemble run cycles, RUNDURATION, NHOURS_FCST)
|
+-ESMF_ClockGet(CLOCK_MAIN, CURRTIME, RUNDURATION)
|
+-ESMF_GridCompFinalize(Execute the NEMS Component Finalize Step, NEMS_GRID_COMP, NEMS_IMP_STATE, 
|                       NEMS_EXP_STATE, CLOCK_MAIN, phase, userRc)
+-ESMF_ClockDestroy(Destroy the Main Clock, CLOCK_MAIN)
|
+-ESMF_ConfigDestroy(Destroy the Main Configure Object, CF_MAIN)
|
+-ESMF_StateDestroy(Destroy the ESMF states, NEMS_IMP_STATE, NEMS_EXP_STATE)
|
+-GridCompDestroy(Destroy ESMF Grid Comp and Cpl Comp, NEMS_GRID_COMP)
|
+-ESMF_Finalize(Shut down the ESMF system)
|
+-w3tage('nems')</pre>
