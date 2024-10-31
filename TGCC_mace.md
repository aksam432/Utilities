# Installation of MACE (or custom python packages) on TGCC
The following steps can be used to install MACE MLIP package on TGCC account. Here, we adopt  a pre-built binary wheels approach to install MACE on TGCC.


## Check machine  architecture TGCC (optional)
Before proceeding with the installation, it's a good practice to verify the system architecture of your TGCC environment. This ensures compatibility with the software you intend to install.

**Command**
``` bash
uname -m
```
**Example output**
```
x86_64
```

## Check python version in TGCC
```
python3 --version
```
I use python 3.10 in TGCC. Note your version of python

# Install MACE wheel files on cluster with internet access
In your linux environment (use your IDRIS account), with same python version,  to install MACE wheel files
``` bash
mkdir mace_wheels
pip download mace-torch  --only-binary=:all:
```
The above command will download all teh wheel files required for  MACE in the `mace_wheels` directory.

**Example wheel file**

``` bash
numpy-1.26.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl

{distribution}-{version}(-{build})?-{python_tag}-{abi_tag}-{platform_tag}.whl
```
**Note that the  python version (cp310- python 3.10) and architecture are consistent with your TGCC python.**

## Copy the wheel files to TGCC and install
Copy all the wheel files to TGCC
```bash
scp -r mace_wheels/ your_username@irene-fr.ccc.cea.fr:/path/to/destination/
```

Next, make a python virtual environment
```bash
mkdir env_mace
python3.10 -m venv env_mace
source /bin/activate
```

## Install the wheel files 
```bash
cd  /path/to/mace_wheel
pip install mace_torch-0.3.4-py3-none-any.whl --no-index --find-links=.
```
`--no-index` ensures pip doesn't search in internet. 
## Verify MACE installation
``` bash
pip list
```

