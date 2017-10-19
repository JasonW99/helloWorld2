# installUbuntu
## 1. Install chrome, wps, and sogou
```bash
$ sudo dpkg -i ~/Downloads/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i ~/Downloads/wps-office_10.1.0.5707_a21_amd64.deb

$ sudo apt remove fcitx* && sudo apt autoremove
$ sudo dpkg -i ~/Downloads/sogoupinyin_2.1.0.0086_amd64.deb; sudo apt -f install
```
If installation encounter configure issue, then use
```bash
$ sudo apt -f install
```
--------------------------------------------------------------------------------------
## 2. Install pycharm 
To install PyCharm using umake, you need to have umake first. Normally, it should already be installed in your system, but if it is not, use the PPA below to get the latest stable version of umake:
```bash
$ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
$ sudo apt-get update
$ sudo apt-get install ubuntu-make
```
Once you have umake, use the command below to install PyCharm Community Edition in Ubuntu:
```bash
$ umake ide pycharm
```
To install PyCharm Professional Edition (you need license for this), you can use the command below:
```bash
$ umake ide pycharm-professional
```
To remove PyCharm installed via umake, use the command below:
```bash
$ umake -r ide pycharm
```
install location
```bash
×× [Choose installation path: /home/jw/.local/share/umake/ide/pycharm]
```
--------------------------------------------------------------------------------------
## 3. Install pip3
```bash
$ sudo apt-get install python3-pip python3-dev
```
--------------------------------------------------------------------------------------
## 4. Install tensorflow
```bash
 $ pip install tensorflow      # Python 2.7; CPU support (no GPU support)
 $ pip3 install tensorflow     # Python 3.n; CPU support (no GPU support)
 $ pip install tensorflow-gpu  # Python 2.7; GPU support
 $ pip3 install tensorflow-gpu # Python 3.n; GPU support 
```
--------------------------------------------------------------------------------------
## 5. Install Bazel
### install dependencies
Install JDK8
```bash
 $ sudo apt-get install openjdk-8-jdk
```
Install curl
```bash
 $  sudo apt install curl
```
Add Bazel distribution URI as a package source (one time setup)
```bash
 $ echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
 $ curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
```
### install Bazel
Install and update Bazel
```bash
 $ sudo apt-get update && sudo apt-get install bazel
 $ sudo apt-get upgrade bazel
```
---------------------------------------------------------------------------------------
## 6. Install gRPC
```bash
 $ sudo pip install qrpcio
 $ sudo pip3 install grpcio
```






