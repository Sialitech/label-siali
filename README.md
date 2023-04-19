<img src="https://user-images.githubusercontent.com/12534576/192582340-4c9e4401-1fe6-4dbb-95bb-fdbba5493f61.png"/>

![GitHub](https://img.shields.io/github/license/heartexlabs/label-studio?logo=heartex) ![label-studio:build](https://github.com/heartexlabs/label-studio/workflows/label-studio:build/badge.svg) ![GitHub release](https://img.shields.io/github/v/release/heartexlabs/label-studio?include_prereleases)

[Website](https://labelstud.io/) • [Docs](https://labelstud.io/guide/) • [Twitter](https://twitter.com/labelstudiohq) • [Join Slack Community <img src="https://app.heartex.ai/docs/images/slack-mini.png" width="18px"/>](https://slack.labelstudio.heartex.com/?source=github-1)


## What is Siali Label?

<!-- <a href="https://labelstud.io/blog/release-130.html"><img src="https://github.com/heartexlabs/label-studio/raw/master/docs/themes/htx/source/images/release-130/LS-Hits-v1.3.png" align="right" /></a> -->

Siali Label is an open source data labeling tool. It lets you label data types like audio, text, images, videos, and time series with a simple and straightforward UI and export to various model formats. It can be used to prepare raw data or improve existing training data to get more accurate ML models.

- [Try out Siali Label](#try-out-label-studio)
- [What you get from Siali Label](#what-you-get-from-label-studio)
- [Included templates for labeling data in Siali Label](#included-templates-for-labeling-data-in-label-studio)
- [Set up machine learning models with Siali Label](#set-up-machine-learning-models-with-Label-Studio)
- [Integrate Siali Label with your existing tools](#integrate-label-studio-with-your-existing-tools)

![Gif of Siali Label annotating different types of data](https://raw.githubusercontent.com/heartexlabs/label-studio/master/images/annotation_examples.gif)

Have a custom dataset? You can customize Siali Label to fit your needs. Read an [introductory blog post](https://towardsdatascience.com/introducing-label-studio-a-swiss-army-knife-of-data-labeling-140c1be92881) to learn more.

## Try out Siali Label

Install Siali Label locally, or deploy it in a cloud instance. [Or, sign up for a free trial of our Enterprise edition.](https://heartex.com/free-trial).

- [Install locally with Docker](#install-locally-with-docker)
- [Run with Docker Compose (Siali Label + Nginx + PostgreSQL)](#run-with-docker-compose)
- [Install locally with pip](#install-locally-with-pip)
- [Install locally with Anaconda](#install-locally-with-anaconda)
- [Install for local development](#install-for-local-development)
- [Deploy in a cloud instance](#deploy-in-a-cloud-instance)

### Install locally with Docker
Official Siali Label docker image is [here](https://hub.docker.com/r/heartexlabs/label-studio) and it can be downloaded with `docker pull`.
Run Siali Label in a Docker container and access it at `http://localhost:8080`.


```bash
docker pull heartexlabs/label-studio:latest
docker run -it -p 8080:8080 -v $(pwd)/mydata:/label-studio/data heartexlabs/label-studio:latest
```
You can find all the generated assets, including SQLite3 database storage `label_studio.sqlite3` and uploaded files, in the `./mydata` directory.

#### Override default Docker install
You can override the default launch command by appending the new arguments:
```bash
docker run -it -p 8080:8080 -v $(pwd)/mydata:/label-studio/data heartexlabs/label-studio:latest label-studio --log-level DEBUG
```

#### Build a local image with Docker
If you want to build a local image, run:
```bash
docker build -t heartexlabs/label-studio:latest .
```

### Run with Docker Compose
Docker Compose script provides production-ready stack consisting of the following components:

- Siali Label
- [Nginx](https://www.nginx.com/) - proxy web server used to load various static data, including uploaded audio, images, etc.
- [PostgreSQL](https://www.postgresql.org/) - production-ready database that replaces less performant SQLite3.

To start using the app from `http://localhost` run this command:
```bash
docker-compose up
```

### Install locally with pip

```bash
# Requires Python >=3.7 <=3.9
pip install label-studio

# Start the server at http://localhost:8080
label-studio
```

### Install locally with Anaconda

```bash
conda create --name label-studio
conda activate label-studio
conda install psycopg2
pip install label-studio
```

### Install for local development

You can run the latest Siali Label version locally without installing the package with pip.

```bash
# Install all package dependencies
pip install -e .
# Run database migrations
python label_studio/manage.py migrate
python label_studio/manage.py collectstatic
# Start the server in development mode at http://localhost:8080
python label_studio/manage.py runserver
```

### Deploy in a cloud instance

You can deploy Siali Label with one click in Heroku, Microsoft Azure, or Google Cloud Platform:

[<img src="https://www.herokucdn.com/deploy/button.svg" height="30px">](https://heroku.com/deploy?template=https://github.com/heartexlabs/label-studio/tree/heroku-persistent-pg)
[<img src="https://aka.ms/deploytoazurebutton" height="30px">](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fheartexlabs%2Flabel-studio%2Fmaster%2Fazuredeploy.json)
[<img src="https://deploy.cloud.run/button.svg" height="30px">](https://deploy.cloud.run)


#### Apply frontend changes

The frontend part of Siali Label app lies in the `frontend/` folder and written in React JSX. In case you've made some changes there, the following commands should be run before building / starting the instance:

```
cd label_studio/frontend/
npm ci
npx webpack
cd ../..
python label_studio/manage.py collectstatic --no-input
```

### Troubleshoot installation
If you see any errors during installation, try to rerun the installation

```bash
pip install --ignore-installed label-studio
```

#### Install dependencies on Windows
To run Siali Label on Windows, download and install the following wheel packages from [Gohlke builds](https://www.lfd.uci.edu/~gohlke/pythonlibs) to ensure you're using the correct version of Python:
- [lxml](https://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml)

```bash
# Upgrade pip
pip install -U pip

# If you're running Win64 with Python 3.8, install the packages downloaded from Gohlke:
pip install lxml‑4.5.0‑cp38‑cp38‑win_amd64.whl

# Install Siali Label
pip install label-studio
```

#### Run test suite
```bash
pip install -r deploy/requirements-test.txt
cd label_studio

# postgres (assumes default postgres user,db,pass)
DJANGO_DB=default DJANGO_SETTINGS_MODULE=core.settings.label_studio python -m pytest -vv -n auto

# sqlite3
DJANGO_DB=sqlite DJANGO_SETTINGS_MODULE=core.settings.label_studio python -m pytest -vv -n auto
```


## What you get from Siali Label

![Screenshot of Siali Label data manager grid view with images](https://raw.githubusercontent.com/heartexlabs/label-studio/master/images/labelstudio-ui.gif)

- **Multi-user labeling** sign up and login, when you create an annotation it's tied to your account.
- **Multiple projects** to work on all your datasets in one instance.
- **Streamlined design** helps you focus on your task, not how to use the software.
- **Configurable label formats** let you customize the visual interface to meet your specific labeling needs.
- **Support for multiple data types** including images, audio, text, HTML, time-series, and video.
- **Import from files or from cloud storage** in Amazon AWS S3, Google Cloud Storage, or JSON, CSV, TSV, RAR, and ZIP archives.
- **Integration with machine learning models** so that you can visualize and compare predictions from different models and perform pre-labeling.
- **Embed it in your data pipeline** REST API makes it easy to make it a part of your pipeline

## Included templates for labeling data in Siali Label

Siali Label includes a variety of templates to help you label your data, or you can create your own using specifically designed configuration language. The most common templates and use cases for labeling include the following cases:

<img src="https://raw.githubusercontent.com/heartexlabs/label-studio/master/images/templates-categories.jpg" />

## Set up machine learning models with Siali Label

Connect your favorite machine learning model using the Siali Label Machine Learning SDK. Follow these steps:

1. Start your own machine learning backend server. See [more detailed instructions](https://github.com/heartexlabs/label-studio-ml-backend).
2. Connect Siali Label to the server on the model page found in project settings.

This lets you:

- **Pre-label** your data using model predictions.
- Do **online learning** and retrain your model while new annotations are being created.
- Do **active learning** by labeling only the most complex examples in your data.

## Integrate Siali Label with your existing tools

You can use Siali Label as an independent part of your machine learning workflow or integrate the frontend or backend into your existing tools.

* Use the [Siali Label Frontend](https://github.com/heartexlabs/label-studio-frontend) as a separate React library. See more in the [Frontend Library documentation](https://labelstud.io/guide/frontend.html).

## Ecosystem

| Project | Description |
|-|-|
| label-studio | Server, distributed as a pip package |
| [label-studio-frontend](https://github.com/heartexlabs/label-studio-frontend) | React and JavaScript frontend and can run standalone in a web browser or be embedded into your application. |
| [data-manager](https://github.com/heartexlabs/dm2) | React and JavaScript frontend for managing data. Includes the Siali Label Frontend. Relies on the label-studio server or a custom backend with the expected API methods. |
| [label-studio-converter](https://github.com/heartexlabs/label-studio-converter) | Encode labels in the format of your favorite machine learning library |
| [label-studio-transformers](https://github.com/heartexlabs/label-studio-transformers) | Transformers library connected and configured for use with Siali Label |


## Roadmap

Want to use **The Coolest Feature X** but Siali Label doesn't support it? Check out [our public roadmap](roadmap.md)!

## Citation

```tex
@misc{Siali Label,
  title={{Siali Label}: Data labeling software},
  url={https://github.com/heartexlabs/label-studio},
  note={Open source software available from https://github.com/heartexlabs/label-studio},
  author={
    Maxim Tkachenko and
    Mikhail Malyuk and
    Andrey Holmanyuk and
    Nikolai Liubimov},
  year={2020-2022},
}
```

## License

This software is licensed under the [Apache 2.0 LICENSE](/LICENSE) © [Heartex](https://www.heartex.com/). 2020-2022

<img src="https://user-images.githubusercontent.com/12534576/192582529-cf628f58-abc5-479b-a0d4-8a3542a4b35e.png" title="Hey everyone!" width="180" />
