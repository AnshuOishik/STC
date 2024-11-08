# Please use the following instructions to run the compressors.
# Clone all repository from github:
# FQZComp: https://sourceforge.net/projects/fqzcomp/
# DSRC 2: https://github.com/lrog/dsrc; (Result): https://calc.biokirr.com/sequence-compression-benchmark/ 
# CoGI: http://admis.fudan.edu.cn/projects/cogi.htm; (Result): https://github.com/cobilab/jarvis
# NAF: https://github.com/KirillKryukov/naf 
# GeCo: https://github.com/cobilab/geco
# GeCo2: https://github.com/cobilab/geco2 
# GeCo3: https://github.com/cobilab/geco3
# Jarvis: https://github.com/cobilab/jarvis
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# The code and other details for the compressors (FQZComp, GeCo, GeCo2, GeCo3, and Jarvis) were obtained from the following link: https://github.com/AnshuOishik/GraSS.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# NAF
# Executing the Compressors:
# Run the following:
conda install naf

# Clone all repository from github
git clone --recurse-submodules https://github.com/KirillKryukov/naf.git

# Please change ennaf.c, unnaf.c, Makefile in ennaf and unnaf, add cpuUsage.c (Given in the folder naf_modified)

# To install the required software, if not installed. Use the following command: 
sudo apt install git gcc make diffutils perl

# Make
make

# for clean install 
make clean

# In naf folder create a tempdir using: 
mkdir tempdir

# To Run
# run ennaf and unnaf using these command (inside ennaf dir and unnaf dir respectively)
# To compress:
cd naf/ennaf
time ./ennaf  <Input file path> -o <Output file path> --temp-dir <Temp dir path>
# E.g. 
time ./ennaf  ../BuEb -o ../out.naf --temp-dir ../tempdir/

# To decompress:
cd naf/unnaf
time ./unnaf  <Comp file path> -o <Decom file path>
# E.g.
time unnaf  ../out.naf -o ../out
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
# We calculate CPU usage over a period of time and then give average usage; the same is true for memory usage.
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Contacts 
Please send an email to <subhankar.roy07@gmail.com> if you experience any issues.
