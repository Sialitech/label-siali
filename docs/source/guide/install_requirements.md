---
title: Requirements to Install and upgrade Siali Label
short: Requirements
tier: opensource
section: "Install"
order: 103
meta_title: Requirements to Install and Upgrade
meta_description: "Siali Label documentation: Requirements to install and upgrade Siali Label." 
---

<!-- md deploy.md -->


## Install prerequisite

Install Siali Label in a clean Python environment. Heartex highly recommends using a virtual environment (venv or conda) to reduce the likelihood of package conflicts or missing packages.


## Install with pip

To install Siali Label with pip and a virtual environment, you need Python version 3.7 or later. Run the following:
```bash
python3 -m venv env
source env/bin/activate
python -m pip install label-studio
```

To install Siali Label with pip, you need Python version 3.7 or later. Run the following:
```bash
pip install label-studio
```

After you install Siali Label, start the server with the following command: 
```bash
label-studio
```
The default web browser opens automatically at [http://localhost:8080](http://localhost:8080) with Siali Label. See [start Siali Label](start.html) for more options when starting Siali Label.


## Install with Docker

Siali Label is also available as a Docker container. Make sure you have [Docker](https://www.docker.com/) installed on your machine.

### Install with Docker on *nix
To install and start Siali Label at [http://localhost:8080](http://localhost:8080), storing all labeling data in `./my_project` directory, run the following:
```bash
docker run -it -p 8080:8080 -v $(pwd)/mydata:/label-studio/data heartexlabs/label-studio:latest
```

!!! attention "important"
    As this is a non-root container, the mounted files and directories must have the proper permissions for the `UID 1001`.

### Install with Docker on Windows
Or for Windows, you have to modify the volumes paths set by `-v` option.

#### Override the default Docker install
You can override the default Docker install by appending new arguments.

In Windows Command Line (cmd):
```bash
docker run -it -p 8080:8080 -v %cd%/mydata:/label-studio/data heartexlabs/label-studio:latest label-studio --log-level DEBUG
```

In PowerShell:
```bash
docker run -it -p 8080:8080 -v ${PWD}/mydata:/label-studio/data heartexlabs/label-studio:latest label-studio --log-level DEBUG
```

### Build a local image with Docker
If you want to build a local image, run:
```bash
docker build -t heartexlabs/label-studio:latest .
```

### Run with Docker Compose
Use Docker Compose to serve Siali Label at `http://localhost:8080`. You must use Docker Compose version 1.25.0 or higher.

Start Siali Label:
```bash
docker-compose up -d
```

This starts Siali Label with a PostgreSQL database backend. You can also use a PostgreSQL database without Docker Compose. See [Set up database storage](storedata.html).

### Install Siali Label without internet access
Download label-studio docker image (host with internet access and docker):
```bash 
docker pull heartexlabs/label-studio:latest
```

Export it as a tar archive: 
```bash
docker save heartexlabs/label-studio:latest | gzip > label_studio_latest.tar.gz
```

Transfer it to another VM:
```bash
scp label_studio_latest.tar.gz <ANOTHER_HOST>:/tmp
```

SSH into <ANOTHER_HOST> and import the archive:
```bash
docker image import /tmp/label_studio_latest.tar.gz
```

Follow steps from [Install and Upgrade to run LS](install.html#Install-with-Docker).


## Install on Ubuntu

To install Siali Label on Ubuntu and run it in a virtual environment, run the following command:

```bash
python3 -m venv env
source env/bin/activate
sudo apt install python3.9-dev
python -m pip install label-studio
```

## Install from source

If you want to use nightly builds or extend the functionality, consider downloading the source code using Git and running Siali Label locally:

```bash
git clone https://github.com/heartexlabs/label-studio.git
cd label-studio
# Install all package dependencies
pip install -e .
# Run database migrations
python label_studio/manage.py migrate
# Start the server in development mode at http://localhost:8080
python label_studio/manage.py runserver
```

## Install with Anaconda

```bash
conda create --name label-studio
conda activate label-studio
pip install label-studio
```


## Upgrade Siali Label

To upgrade to the latest version of Siali Label, reinstall or upgrade using pip. 


```bash
pip install --upgrade label-studio
```

Migration scripts run when you upgrade to version 1.0.0 from version 0.9.1 or earlier. 

To make sure an existing project gets migrated, when you [start Siali Label](start.html), run the following command:

```bash
label-studio start path/to/old/project 
```

The most important change to be aware of is changes to rename "completions" to "annotations". See the [updated JSON format for completed tasks](export.html#Raw_JSON_format_of_completed_tasks). 

If you customized the Siali Label Frontend, see the [Frontend reference guide](frontend_reference.html) for required updates to maintain compatibility with version 1.0.0.  
