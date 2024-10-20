# Please use the following instructions to run the compressors.
# Clone all repository from github:
# FQZComp: https://sourceforge.net/projects/fqzcomp/
# DSRC 2: https://github.com/lrog/dsrc
# CoGI: http://admis.fudan.edu.cn/projects/cogi.htm
# NAF: https://github.com/KirillKryukov/naf 
# GeCo3: https://github.com/cobilab/geco3
# GeCo2: https://github.com/cobilab/geco2 
# GeCo: https://github.com/cobilab/geco
# Jarvis: https://github.com/cobilab/jarvis

# FQZComp Compilation
cp Makefile Makefile2
mv Makefile2 Makefile
make

# Run
To compress:
    time ./fqz_comp -s1 -q3 ../DNA/In.fastq ../DNA/comp.fqz
	
To decompress:
    time ./fqz_comp -d ../DNA/comp.fqz ../DNA/Out.fastq
	
	time ./fqz_comp -d -X ../DNA/comp.fqz ../DNA/Out.fastq [To pass checksum failures use -X in the decompressor]
	
# Options:
-s <level>
    Specifies the size of the sequence context. Increasing this will
    improve compression on large data sets, but each increment in
    level will quadruple the memory used by the sequence compression
    steps. Further more increasing it too high may harm compression on
    small files.

    Specifying a "+" after level will use two context sizes (eg -s5+);
    a small fixed size and the <level> specified. This greatly helps
    compression of small files and also slightly helps compression of
    larger files.

    Defaults to -s3.

-q <level>
    Specifies the degree of quality compression, with a value from -q1
    to -q3.

    -q1
        Uses the previous quality value and the maximum of the two
        previous to that as a context for predicting the next value.
        Combined this adds 12 bits of context.

    -q2
        In addition to -q1, this extends the context by adding a
        single bit to indicate if the 2nd and 3rd previous qualities
        are identical to each other, as well as using 3 bits of
        context for the running-delta. (A measure of how variable a
	string of quality values are.) This is the default level.

     -q3
        As per -q2, but also adds 4 bits worth of context holding the
        position each the sequence.

The caveats and other informations in the original source. 
https://sourceforge.net/projects/fqzcomp/

# NAF Benchmark Compressor downloading linkS:
NAF: https://github.com/KirillKryukov/naf 

# Executing the Compressors:

#Run the following:
conda install naf

# clone all repository from github
git clone --recurse-submodules https://github.com/KirillKryukov/naf.git

# Change ennaf.c, unnaf.c, Makefile in ennaf and unnaf, add cpuUsage.c (Given in the folder naf_modified)

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
# Compress:
cd naf/ennaf
time ./ennaf  <Input file path> -o <Output file path> --temp-dir <Temp dir path>
# E.g. 
time ./ennaf  ../BuEb -o ../out.naf --temp-dir ../tempdir/

#Decompress:
cd naf/unnaf
time ./unnaf  <Comp file path> -o <Decom file path>
# E.g.
time unnaf  ../out.naf -o ../out

# Executing the state-of-the-art compressors GeCo, GeCo2, geCo3 and Jarvis:

# Install miniconda (https://docs.anaconda.com/miniconda/#quick-command-line-install) then run the following commands
# For GeCo2: conda install -y -c bioconda geco2
# For GeCo3: conda install -y -c bioconda geco3
# For Jarvis: conda install -y -c bioconda jarvis

# Modify geco and jarvis (modify garbage in defs.h and common.c)

# Add cpuUsage.c to the repository for Memory & CPU usage

# Modify geco(1,2,3).c and gede(1,2,3).c and Jarvis.c for Memory & CPU usage

# Make
cp Makefile.linux Makefile2.linux
mv Makefile2.linux Makefile
make

# To clean make
make clean
 
# To run
# GeCo
./GeCo -tm 1:1:0:0/0 -tm 3:1:0:0/0 -tm 6:1:0:0/0 -tm 9:10:0:0/0 -tm 11:10:0:0/0 -tm 13:50:1:0/0 -tm 18:100:1:3/10 -c 30 -g 0.9 CompressedFileName
./GeDe -v DecompressedFileName

# GeCo2
./GeCo2 -v -l <level(or mode)> CompressedFileName
./GeDe2 -v DecompressedFileName

# GeCo3
./GeCo3 -l <level> -lr <learning rate> -hs <hidden nodes> CompressedFileName
./GeDe3 DecompressedFileName

# Jarvis
./JARVIS -v -l <level> CompressedFileName
./JARVIS -v -d DecompressedFileName

# We calculate CPU usage over a period of time and then give avg usage, same for Memory usage.

# To run other compressor please use the readme file provided in the corresponding compressor folder

# To change the file format, please use the code supplied in the following link:
https://github.com/KirillKryukov/scb/tree/master/seq-tools-c.
