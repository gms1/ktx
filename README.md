# ktx

## Overview

Managing kubeconfig files can become tedious when you have multiple clusters and contexts to switch between. `ktx` aims to reduce friction caused by switching between various configurations.

`ktx` takes the approach of modifying the `KUBECONFIG` environment variable to select the desired config.
`ktx-config` can be used to configure a default, by managing a symbolic link ~/.kube/config which points to the desired config.

## Getting Started

### Prerequisites

* Your are suing bash.

### Install

```sh
wget -O ~/.ktx https://raw.githubusercontent.com/gms1/ktx/refs/heads/master/ktx

# Add this to your "${HOME}/".bash_profile (or similar)
source "${HOME}"/.ktx

# Reload your shell
exec bash
```

### Usage

Once `ktx` is installed you can use it as auto-complete:

```sh
# useful to see what clusters you have in ${HOME}/.kube/
gms@sirius:~$ ktx <tab><tab>
alpha    beta     delta    epsilon  gamma    NONE
gms@sirius:~$ ktx-config <tab><tab>
alpha    beta     delta    epsilon  gamma    NONE
gms@sirius:~$ ktx-print-configs
  beta
  gamma
  alpha
  epsilon
  delta

# set default config
gms@sirius:~$ ktx-config beta
gms@sirius:~$ ls -l ~/.kube/config
lrwxrwxrwx 1 gms gms 4 Dez  1 14:40 /home/gms/.kube/config -> beta
gms@sirius:~$ ktx-config
beta

# set config
gms@sirius:~$ ktx gamma
gms@sirius:~$ echo $KUBECONFIG
/home/gms/.kube/gamma
gms@sirius:~$ ktx-config
gamma
gms@sirius:~$ ktx-print-configs
* gamma
  beta (default)
  alpha
  epsilon
  delta

# reset config
gms@sirius:~$ ktx NONE
gms@sirius:~$ echo $KUBECONFIG

gms@sirius:~$ ktx-config
beta
gms@sirius:~$ ktx-print-configs
* beta (default)
  gamma
  alpha
  epsilon
  delta
```

# Pronunciation Guide

`ktx` is pronounced as "k thanks"
