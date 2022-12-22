
#### [Install](https://github.com/dmfow/CheatSheets/blob/main/Python%20Virtualenv.md#install-1)
1. [Install with pip](https://github.com/dmfow/CheatSheets/blob/main/Python%20Virtualenv.md#install-with-pip)
2. [Check the version](https://github.com/dmfow/CheatSheets/blob/main/Python%20Virtualenv.md#check-the-version)

If you want to you can think of an environment as a VM (but it isn't)


## Working in it

#### Start working in the enviroment - Always do this when using it
```python
# LINUX
source thenewenvironment/bin/activate
(virtualenv_name)$

# WINDOWS
cd ~/code/py_vm
Scripts\activate
```

#### Stop using the environment
```python
deactivate
```

## Create a new

#### Create a new environment
A directory will be created where you are in the library. cd here when using it.
<br>
This is where Python packages will be installed
```python
mkdir ~/code/py_vm
cd ~/code/py_vm
virtualenv thenewenvironment
```

#### Select a specific Python version for the environment
```python
virtualenv -p /usr/bin/python3 thenewenvironment
# OR
virtualenv -p /usr/bin/python2.7 thenewenvironment
```



## Install

#### Install with pip
```python
pip3 install virtualenv
```


#### Check the version
```python
virtualenv --version
```


