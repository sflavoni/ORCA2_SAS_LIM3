# How to use ORCA2_SAS_LIM3 configuration

This is a README for NEMO users. You need to have an account on NEMO web site: .....

### Extract XIOS library via svn :
You need to extract XIOS library (to manage inputs and outputs files for NEMO code):
svn co ​http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0

### Compile XIOS library :
You need to compile XIOS (see here documentation https://forge.ipsl.jussieu.fr/ioserver/wiki/documentation)

example on CURIE french machine:   
./make_xios --arch X64\_CURIE


You can see how to extract the code nemo  here: 
https://forge.ipsl.jussieu.fr/nemo/wiki/Users/ModelInstall: 

### Extract the code NEMO via svn :
svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/branches/2015/nemo_v3_6_STABLE/NEMOGCM

### Compile NEMO :

Compile ORCA2_SAS_LIM3 directory:

cd NEMOGCM/CONFIG

./makenemo –m 'my_arch' –n ORCA2\_SAS\_LIM3 

### Input necessary files :
Input files necessary for ORCA2_SAS_LIM3 are:

[INPUTS_SAS_v3.5.tar](http://prodn.idris.fr/thredds/catalog/ipsl_public/romr005/Online_forcing_archives/catalog.html?dataset=DatasetScanipsl_public/romr005/Online_forcing_archives/INPUTS_SAS_v3.5.tar)

and 

[ORCA2_LIM_nemo_v3.7.tar](prodn.idris.fr/thredds/catalog/ipsl_public/romr005/Online_forcing_archives/catalog.html?dataset=DatasetScanipsl_public/romr005/Online_forcing_archives/ORCA2_LIM_nemo_v3.7.tar)
