# HPC-IIT-Delhi
HPC Details and Use of IIT Delhi
Get HPC Access from here https://userm.iitd.ac.in/usermanage/hpc.html

Download filezilla. Login into filezilla using:-
Hostname = hpc.iitd.ac.in
Username = mcs182012
Port = 22
Password = ********

Transfer your python and data files using filezilla drag and drop.

In linux command promt type:-
ssh mcs182012@hpc.iitd.ac.in
Then type your password and hit enter

After successful login type:-

Type:-(for first time login only)
cp /home/apps/skeleton/.bashrc  $HOME/.bashrc 
cp /home/apps/skeleton/.bash_profile $HOME/.bash_profile
ln -s $SCRATCH $HOME/scratch

Now the main work comes. You need to specify the resources you need.
Type:-
qsub -IP cse -l select=1:ncpus=8:ngpus=1:mem=24G -l walltime=6:00:00
Wait till resources are allocated...

Use cd command move to your home directory. Eg:- cd ../../../home/cse/mtech/mcs182012
You can also use scratch to operate but all the files in scratch are auto deleted.
So you need to take care of this if you are working on scratch directory.

Home directory space - 30GB
Scratch directory space - 100GB

Load python3.6 modules now...
module load compiler/python/3.6.0/ucs4/gnu/447 
module load pythonpackages/3.6.0/ucs4/gnu/447/pip/9.0.1/gnu
module load pythonpackages/3.6.0/ucs4/gnu/447/setuptools/34.3.2/gnu
module load pythonpackages/3.6.0/ucs4/gnu/447/wheel/0.30.0a0/gnu

module load apps/pythonpackages/3.6.0/tensorflow/1.9.0/gpu
module load apps/pythonpackages/3.6.0/keras/2.2.2/gpu
module load apps/pythonpackages/3.6.0/pytorch/0.4.1/gpu
module load apps/pythonpackages/3.6.0/tensorflow/1.9.0/gpu
module load apps/pythonpackages/3.6.0/torchvision/0.2.1/gpu


Download IITD Certificate from here - http://www.cc.iitd.ernet.in/certs/CCIITD-CA.crt
Transfer to filezilla using drag and drop again.

Now use the command.
export SSL_CERT_FILE=$HOME/CCIITD-CA.crt 
lynx https://proxy62.iitd.ernet.in/cgi-bin/proxy.cgi
Login using id and password.

Now set the http and https proxy....
export http_proxy=10.10.78.62:3128
export https_proxy=10.10.78.62:3128

install python3 libraries now...
pip install scipy matplotlib scikit-learn scikit-image numpy pandas --user

Alternatively HPC has a lot of libraries. Just use the command :- module avail
to list all of them.
Copy the module text you want and type :- module load YOUR-MODULE-LINK
to load the module.

Now run using python command.
python test.py

You can use the command :- qstat -u $USER
to see the status of your resources.

You can then delete any resources using the command:- qdel JOBID
JOBID is the number obtained after type qstat -u $USER

If you stopped your program in the middle of execution, then it will give CUDA OUT OF MEMORY error next time if you try to run program on gpu from the same login node.
So you need to flush the gpu.
Type:-
nvidia-smi
kill -9 PID
