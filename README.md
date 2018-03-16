# ORCA2\_SAS\_LIM3

ORCA2\_SAS\_LIM is a demonstrator of the SAS ( Stand-alone Surface module ) based on ORCA2_LIM configuration. It runs only the sea ice module but needs the ocean code to initalize the domain, scale factors etc.

### Download and compile XIOS library (inputs and outputs for NEMO)  
Documentation: <https://forge.ipsl.jussieu.fr/ioserver/wiki/documentation>  

~~~sh
mkdir XIOS  
svn co ​http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk XIOS  

cd XIOS  
./make_xios --arch 'your-compiler' --jobs 8
~~~

### Download and compile NEM0
Documentation: <https://forge.ipsl.jussieu.fr/nemo/wiki/Users/ModelInstall> 

~~~sh
svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/branches/2017/dev_merge_2017

cd dev_merge_2017/NEMOGCM/CONFIG
./makenemo –m 'your-compiler' –n ORCA2_SAS_LIM3 -j 4
~~~

### Run ORCA2\_SAS\_LIM3
Go the exec directory:

~~~sh
cd ORCA2_SAS_LIM3/EXP00
~~~

Get the input files for atmospheric forcing [here] (<http://prodn.idris.fr/thredds/catalog/ipsl_public/romr005/Online_forcing_archives/catalog.html?dataset=DatasetScanipsl_public/romr005/Online_forcing_archives/ORCA2_LIM_nemo_v3.7.tar>)

Get the input files for oceanic forcing (surface velocity, sst, sss & ssh) here: [link] (<http://prodn.idris.fr/thredds/catalog/ipsl_public/romr005/Online_forcing_archives/catalog.html?dataset=DatasetScanipsl_public/romr005/Online_forcing_archives/INPUTS_SAS_v3.5.tar>)  


Run the simulation:  

~~~sh
poe ./opa -procs 32
~~~

### How to change your simulation set up  

* You can change your simulation length etc in namelist\_cfg  

~~~fortran
!-----------------------------------------------------------------------
&namrun        !   parameters of the run
!-----------------------------------------------------------------------
   nn_it000    =       1   !  first time step
   nn_itend    =    5475   !  last  time step (std 5475)
~~~

* You can change the ocean fields used to force the ice from below  

You can either read an ocean state

~~~fortran
!-----------------------------------------------------------------------
&namsbc_sas    !   Stand-Alone Surface boundary condition
!-----------------------------------------------------------------------
   l_sasread   = .true.    !  =T Read the above fields in a file, =F initialize to 0. in sbcssm.F90
~~~

Or have constant values defined in SAS_SRC/sbcssm.F90

~~~fortran
   l_sasread   = .false.    !  =T Read the above fields in a file, =F initialize to 0. in sbcssm.F90
~~~

* You can change the atm. fields used to force the ice from above

~~~fortran
!-----------------------------------------------------------------------
&namsbc_blk   !   namsbc_blk  generic Bulk formula                      (ln_blk =T)
!-----------------------------------------------------------------------
~~~

* You can change your simulation ice parameters in namelist\_ice\_cfg  

~~~fortran
!------------------------------------------------------------------------------
&nampar         !   Generic parameters
!------------------------------------------------------------------------------
   jpl              =   5             !  number of ice  categories
~~~

_Note: The namelists read by the code are the reference namelists "namelist\_ref" overwritten by the configuration namelists "namelist\_cfg"_

* You can change your outputs in file\_def\_nemo-lim.xml  

~~~xml
<file_group id="5d" output_freq="5d"  output_level="10" enabled=".TRUE.">  <!-- 5d files -->
   <file id="file21" name_suffix="_icemod" description="ice variables" enabled=".true." >
      <field field_ref="icethic"          name="sithic" />
   </file>
</file_group>
~~~