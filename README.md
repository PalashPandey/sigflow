# Sigflow: Streamline Analysis Workflow for Mutational Signatures

<img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/shixiangwang/sigminer.workflow"> <img alt="Docker Automated build" src="https://img.shields.io/docker/automated/shixiangwang/sigflow"> <img alt="Docker Image Version (latest by date)" src="https://img.shields.io/docker/v/shixiangwang/sigflow?color=blue"> <img alt="Docker Image Size (latest by date)" src="https://img.shields.io/docker/image-size/shixiangwang/sigflow"> <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/shixiangwang/sigflow">

```
       .__        _____.__                 
  _____|__| _____/ ____\  |   ______  _  __
 /  ___/  |/ ___\   __\|  |  /  _ \ \/ \/ /
 \___ \|  / /_/  >  |  |  |_(  <_> )     / 
/____  >__\___  /|__|  |____/\____/ \/\_/  
     \/  /_____/  
```

**Sigflow** provides useful mutational signature analysis workflows based on R package [sigminer](https://github.com/ShixiangWang/sigminer). It can auto-extract mutational signatures,
fit mutation data to COSMIC reference signatures (SBS/DBS/INDEL) and run bootstrapping analysis for
signature fitting.

Skip the following installation step if you would like to use [Docker](https://hub.docker.com/r/shixiangwang/sigflow).

## Installation

Requirements:

- R (>3.6).
- R package [sigminer](https://github.com/ShixiangWang/sigminer).
- R package [docopt](https://cran.r-project.org/package=docopt).

Steps:

1. Install R - follow the instructions at <https://cran.r-project.org/>.
2. Install R packages, run

```r
install.packages("docopt")
install.packages("BiocManager")
BiocManager::install("sigminer", dependencies = TRUE)
```

3. Clone this repository, run

```bash
$ git clone https://github.com/ShixiangWang/sigminer.workflow
```

4. Link the R script as a executable file (command)

```bash
$ cd sigminer.workflow
$ ln -s $PWD/sigflow.R /usr/bin/sigflow  # You can choose another place instead of /usr/bin/sigflow
```

5. Try calling `sigflow`

```bash
sigflow -h
```

> Maybe you need to restart your terminal.

## Use Sigflow docker image

Use specified version (recommended way):

```bash
# docker pull shixiangwang/sigflow:version, e.g.
$ docker pull shixiangwang/sigflow:0.1
```

Current available tag versions:

- <img alt="Docker Image Version (tag latest semver)" src="https://img.shields.io/docker/v/shixiangwang/sigflow/0.1?color=blue"> <img alt="MicroBadger Layers (tag)" src="https://img.shields.io/microbadger/layers/shixiangwang/sigflow/0.1"> <img alt="Docker Image Size (tag)" src="https://img.shields.io/docker/image-size/shixiangwang/sigflow/0.1">

Version platforms:

- Sigflow 0.1 is based on Sigminer v1.0.9 in R v4.0.2

Use latest version:

```bash
$ docker pull shixiangwang/sigflow:latest
```

> The latest version uses the latest commit from GitHub, so it may have not been
> prepared or tested. **So, be careful!**

Run the docker by:

```bash
$ docker run shixiangwang/sigflow
```

See [test/test_docker.sh](test/test_docker.sh) for examples.

If you want to go into the docker terminal, run

```bash
$ docker run --rm --entrypoint /bin/bash -it shixiangwang/sigflow
```

## Updates

- 2020-07-29: release the first version of sigflow (0.1) using Docker.

## Usage

```
sigflow: Streamline Analysis Workflow for Mutational Signatures.

Author: Shixiang Wang (wangshx@shanghaitech.edu.cn)
Copyright: AFL@2020 [https://opensource.org/licenses/AFL-3.0]

Desc:
  There are several subcommands.
  ==
  extract - extract signatures by either automated or manual way.
            Of note, when you use manual way, you need to run 2 times, 
            firstly you should set --manual to get signature estimation results,
            and secondly you should set --manual --number N to get N signatures.
  ==
  fit     - fit signatures in >=1 samples.
  ==
  bt      - run bootstrap signature fitting analysis in >=1 samples.

Usage:
  sigflow extract --input=<file> [--output=<outdir>] [--mode=<class>] [--manual --number <sigs>] [--genome=<genome>] [--nrun=<runs>] [--cores=<cores>]
  sigflow fit --input=<file> [--output=<outdir>] [--mode=<class>] [--genome=<genome>]
  sigflow bt --input=<file> [--output=<outdir>] [--mode=<class>] [--genome=<genome>] [--nrun=<runs>]
  sigflow (-h | --help)
  sigflow --version

Options:
  -h --help     Show help message.
  --version     Show version.
  -i <file>, --input <file>       input file/directory path.
  -o <outdir>, --output <outdir>  output directory path [default: ./sigflow_result/].
  -m <class>, --mode <class>      extract/fit mode, can be one of SBS, DBS, ID, MAF (for three types), CN (not supported in fit subcommand) [default: SBS].
  --manual                        enable manual extraction, set -N=0 for outputing signature estimation firstly.
  -N <sigs>, --number <sigs>      extract specified number of signatures [default: 0].
  -g <genome>, --genome <genome>  genome build, can be hg19, hg38 or mm10, [default: hg19].
  -r <runs>, --nrun <runs>        run times of NMF (extract) or bootstrapping (bt) to get results [default: 30].
  -T <cores>, --cores <cores>     cores to run the program, large dataset will benefit from it [default: 1].

```

## Test

There are some example data in this repository, you can find how to test different workflows in [test/test.sh](test/test.sh).
It is time consuming to run all tests, just pick an example test similar to your task and see how it works. Before releasing a new version of `sigflow`, I would run all tests to make sure they work well.

## Citation

**sigflow: Streamline Analysis Workflow for Mutational Signatures**, *under preparation*.

If you are using **sigflow** fow now, please cite:

**Wang, Shixiang, et al. “Copy number signature analyses in prostate cancer reveal distinct etiologies and clinical outcomes” medRxiv (2020)** https://www.medrxiv.org/content/early/2020/04/29/2020.04.27.20082404

## License

This software is release under [Academic Free License ("AFL") v. 3.0](https://opensource.org/licenses/AFL-3.0)

Copyright 2020 © Shixiang Wang
