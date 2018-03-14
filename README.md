# ORCA2_SAS_LIM3
How to use ORCA2_SAS_LIM3 configuration

This is a README for NEMO users. You need to have an account on NEMO web site: .....


You need to extract XIOS library (to manage inputs and outputs files for NEMO code):
svn co ​http://forge.ipsl.jussieu.fr/ioserver/svn/XIOS/trunk xios-2.0

You need to compile xios (see here documentation https://forge.ipsl.jussieu.fr/ioserver/wiki/documentation)

example on CURIE french machine:   
./make_xios --arch X64\_CURIE

You can see how to extract the code nemo here: 
https://forge.ipsl.jussieu.fr/nemo/wiki/Users/ModelInstall: 

Extract the code NEMO via svn:

svn --username 'mylogin' co http://forge.ipsl.jussieu.fr/nemo/svn/branches/2015/nemo\_v3\_6_STABLE/NEMOGCM

Compile ORCA2\_SAS\_LIM3 directory:

cd NEMOGCM/CONFIG

./makenemo –m 'my_arch' –n ORCA2\_SAS\_LIM3 

- comment compiler SAS (OPA ; LIM ; SAS ; NST ?? + compiler OASIS + XIOS)
- inputs nécessaires (short description et nom des inputs + emplacement dans la namelist ?)

