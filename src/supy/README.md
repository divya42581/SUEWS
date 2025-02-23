# SuPy

**This project is now merged into [SUEWS](https://github.com/UMEP-dev/SUEWS).**


---------

[![Python Version Support Status](https://img.shields.io/pypi/pyversions/supy.svg)](https://pypi.org/project/supy)
[![Latest Version Status](https://img.shields.io/pypi/v/supy.svg)](https://pypi.org/project/supy)
[![Downloads](https://pepy.tech/badge/supy)](https://pepy.tech/project/supy)
[![Launch Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/UMEP-dev/SuPy/main)

[![Documentation Status](https://readthedocs.org/projects/supy/badge/?version=latest)](https://supy.readthedocs.io/en/latest/?badge=latest)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2574404.svg)](https://doi.org/10.5281/zenodo.2574404)



[**SU**EWS](https://suews-docs.readthedocs.io) that speaks **Py**thon

## Installation

SuPy requires 64-bit `python` 3.7+ and can be installed with `pip` in command line prompt:


```shell
python3 -m pip install supy --upgrade
```

## Quick Demo

Once installed, `supy` can be quickly started to get [SUEWS](https://suews-docs.readthedocs.io) simulations done:

```python {cmd}
import supy as sp
import matplotlib.pyplot as plt

#load sample data
df_state_init, df_forcing = sp.load_SampleData()
grid = df_state_init.index[0]

#run supy/SUEWS simulation
df_output, df_state_end = sp.run_supy(df_forcing, df_state_init)

#plot results and save figure
res_plot = df_output.SUEWS.loc[grid, ['QN', 'QF', 'QS', 'QE', 'QH']]
ax=res_plot.loc['2012 6 4':'2012 6 6'].resample('30T').mean().plot()
plt.show()
ax.figure.savefig('sample_plot.png')
```

The above code will produce a plot of surface energy balance components as follows:

![sample plot](./sample_plot.png)

## Tutorial

Please check out [more SuPy tutorials here!](https://supy.readthedocs.io/en/latest/tutorial/tutorial.html)

## Installation of the development version of SuPy

The development version `supy` includes both the `supy` wrapper and its kernel `supy-driver` - the calculation kernel written in Fortran.

All below is supposed to be in a directory named `supy-dev` - which however you can change.


1. Get both the source code of SUEWS and SuPy

the development version of SuPy.

``` shell
# get the source code of SUEWS and SuPy
git clone --recurse-submodules git@github.com:UMEP-dev/SUEWS.git

git clone git@github.com:UMEP-dev/SuPy.git

```

2. Set up the [conda environment](https://conda.io/docs/user-guide/tasks/manage-environments.html)


```shell
conda env create -f SuPy/env.yml
conda activate supy

```

3. Install the dev version of SuPy

```shell

pip install -e SuPy/src

```


4. Compile the kernel `supy-driver`

```shell
cd SUEWS/supy-driver
make dev

```

Here you can check if `supy-driver` is installed correctly:

```shell
pip show supy-driver
```
note the `location` field in the output, which should point to the local `supy-driver` directory.


Note: after installing the development version of `supy-driver`, you might get the warning about incompatibility, which you can ignore and carry on. However, in case of any issue, please report it [here](https://github.com/UMEP-dev/SuPy/issues/new?assignees=&labels=&template=issue-report.md).



5. Check the version info of installed supy

```shell
pip show supy
```
note the `location` field in the output, which should point to the local `supy` directory.
