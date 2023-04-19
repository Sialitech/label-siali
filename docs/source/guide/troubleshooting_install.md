---
title: Troubleshooting Install and upgrade Siali Label
short: Troubleshoot Install 
tier: opensource
order: 103
section: "Install"
meta_title: Troubleshoot Install and Upgrade
meta_description: "Siali Label documentation: Troubleshoot Install and upgrade Siali Label." 
---

## Run the latest version of Siali Label

Many bugs might be fixed in patch releases or maintenance releases. Make sure you're running the latest version of Siali Label by upgrading your installation before you start Siali Label. 


## Errors about missing packages

If you see errors about missing packages, install those packages and try to install Siali Label again. Make sure that you run Siali Label in a clean Python environment, such as a virtual environment.

For Windows users the default installation might fail to build the `lxml` package. Consider manually installing it from [the unofficial Windows binaries](https://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml). If you are running Windows 64-bit with Python 3.8 or later, run `pip install lxml‑4.5.0‑cp38‑cp38‑win_amd64.whl` to install it. 


## Errors from Siali Label 

If you see any other errors during installation, try to rerun the installation.

```bash
pip install --ignore-installed label-studio
```

## OpenBLAS blas_thread_init: pthread_create failed for thread X of Y: Operation not permitted

Upgrade Docker Engine to the latest available version(>= [20.10.12](https://docs.docker.com/engine/release-notes/#201012)).

