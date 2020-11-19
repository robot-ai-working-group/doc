# set up gym-robotics(mujoco) on linux

## enviroment
* Ubuntu 18.04LT

```bash
# install libraries
apt-get install libffi
apt-get install gcc-6
apt-get install patchelf
apt-get install libglu1-mesa-dev mesa-common-dev
#
# python
pyenv install 3.7.5
pyenv global 3..7.5
#
# pyhon modules
pip install --upgrade pip
pip install --upgrade setuptools
#
# mujoco
wget https://www.roboti.us/download/mujoco200_linux.zip
cd ~/Downloads
unzip mujoco200_linux.zip
mv mujoco200_linux ~/.mujoco/mujoco200
mv mjkey.txt ~/.mujoco # get the license key at the site, https://www.roboti.us/license.html
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/{username}/.mujoco/mujoco200/bin
source ~/.bashrc
#
# mujoco-py
mkdir ~/Documents/repo
cd ~/Documents/repo
git clone https://github.com/openai/mujoco-py.git
cd mujoco-py
pip install -r requirements.txt
pip install -r requreiments-dev.txt
python setup.py install
```