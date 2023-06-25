# How-to-install-python-jupyter-in-linux

Example:- python 3.7.7
Check which partition has maximum space. Ex:- /home
```
mkdir /home/python3.7.7
cd python3.7.7
```
Download from official page desired python version
```
wget https://www.python.org/ftp/python/3.7.7/Python-3.7.7.tgz
```
unzip the file and go inside the folder
```
tar xzf Python-3.7.7.tgz
cd Python-3.7.7
```
If yum install giving error despite having internet, 
you need to update the /etc/yum.repo.d files namely app.repo, base.repo
https://access.redhat.com/articles/4238681
> The URL to each repository is listed with the repository name \
> Replace $basearch with your computer architecture, such as x86_64, as shown in the examples: \
Edit using vim:-
```
vi /etc/yum.repo.d/app.repo
```
```
[AppStream]
name=AppStream
#baseurl=http://10.32.138.81/ks/ipsm_rhel8/AppStream #this is older url
baseurl=https://cdn-ubi.redhat.com/content/public/ubi/dist/ubi8/8/x86_64/appstream/os
enabled=1
gpgcheck=0
```

In RHEL:-
```
yum install iputils gcc make zlib-devel openssl-devel libffi-devel sqlite-devel \
bzip2-devel ncurses-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
```
In Debian based system:-
```
apt install libbz2-dev sqlite3 libffi-dev libssl-dev libncurses5-dev libsqlite3-dev \
libreadline-dev libtk8.6 libgdm-dev libdb4o-cil-dev libpcap-dev xz-utils liblzma-dev libbz2-dev
```
After installing system packages, next step in installtion:-
```
./configure --enable-optimizations
make altinstall
```
To check if python installed correctly,
```
python3.7 -V
```

Command to locate installed location of python:-
```
which python3.7
# /usr/local/bin/python3.7
```

How to create a new virtualEnvironment?
```
mkdir yourEnv
virtualenv -p /path/to/python/ yourEnv (to create venv)
source yourEnv/bin/activate (to activate venv)

#below steps are helpful when you want to create a new venv using existing venv and want same packages in new one
pip freeze > req.txt (to get the packages with versions)
pip install -r req.txt
```

To use jupyter notebook
```
mkdir jupyter
```
To make jupyter use specific python version:-
```
jupyter kernelspec list
```
see the path of python3, 
go to that location 
and vi kernel.json
in argv key of json, 
give the path of desired python (output of "which python3.x" cmd)

```
export JUPYTER_RUNTIME_DIR=/path/
echo $JUPYTER_RUNTIME_DIR
```
Verify is path set using:-
```
jupyter --runtime-dir 
```
Then you can create new notebook server:-
```
nohup jupyter notebook  --allow-root  --ip 10.x.x.xx &
Ctrl+C
tail -100f nohup.out	
```
get the notebook URL and copy the url in your browser and we are good to go!!

To convert notebook file to python file:-
```
jupyter nbconvert --to script *.ipynb
```
