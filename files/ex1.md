---
permalink: /ex1/
---

# Task 1: Download Source Code and get familiar
Login to FRAM: - ssh login@fram.sigma2.no

Download NorESM code from : https://github.com/NorESMhub/NorESM
```
git clone https://github.com/NorESMhub/NorESM NorESM
cd NorESM
git checkout tags/release-noresm2.0.2 -b noresm
./manage_externals/checkout_externals
```
It download the code mentioned in Externals.cfg and checkout the mentioned tags
Open Externals.cfg and get bit familiar with it
Just go through the SourceCode and get a bit familiar with it. Use query_config, for checking a few compsets and grids.

Task 2: Create following experiment
Compset - N1850frc2  grid - f19_tn14 ;  project = nn9560k
use create_newcase
Change env_mach_pes.xml for total 128 processors counts
ATM=96, CPL=96, OCN=32,WAV=96,GLC=96,ICE=50,ROF=1,LND=45
Decide ROOTPE block by yourself

./case.setup
./case.build
Change env_run.xml – set it for 1 month
./case.submit

Task 3: bitwise reproducibility
Create the following  two different experiments: We will execute first experiment for 2 months and then second one for 1+1 months and check if they are bit-wise reproducible.

Compset - NOINY  grid - T62_tn14 project = nn9560k ; execute it for 2 months;

Change env_mach_pes.xml for total 128 processors counts

./case.setup
./case.build
 Change env_run.xml – set it for 2 months
 ./case.submit

Now, the second experiment is exactly the same as the first one. same compset and grid and processors count; clone of previous experiment.
Use create_clone to create it
set JOB_WALLCLOCK_TIME = 0:29:00 in env_batch.xml in subgroup case.run
Build and execute it for 1 month. 
once it completed then, execute is again for 1 month by putting CONTINUE_RUN =TRUE in env_run.xml and submit again
Taks 4: changing namelist parameter
Make change in user_nl_cam and check namelist in run folder after submitting
Do it in Task-2:
clubb_gamma_coef = 0.26 in user_nl_cam

Task 5: writing intermediate restart files and SAVE in archive
Do it in case 3:
Execute it for 3 more months and save output every months
REST_OPTION=nmonths
REST_N=1
DOUT_S_SAVE_INTERIM_RESTART_FILES=TRUE

Test 6: set a branch run 
Take data from : /cluster/work/users/agu002/archive/N1850frc2_f19_tnx1v4_workshop
Create a clone from Task 2 and setup branch run 
And execute it for 1 month

