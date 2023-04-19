---
title: Start Siali Label
type: guide
tier: opensource
order: 110
order_enterprise: 99
meta_title: Start Commands for Siali Label
meta_description: Documentation for starting Siali Label and configuring the environment to use Siali Label with your machine learning or data science project. 
section: "Install"

---

After you install Siali Label, start the server to start using it. 

```bash
label-studio start
```

By default, Siali Label starts with an SQLite database to store labeling tasks and annotations. You can specify different sources and target storage for labeling tasks and annotations using Siali Label UI or the API. See [Database storage](storedata.html) for more.


## Command line arguments for starting Siali Label

You can specify a machine learning backend and other options using the command line interface. Run `label-studio --help` to see all available options, or refer to the following tables.

Some available commands for Siali Label provide information or start the Siali Label server:

| Command |  Description |
| --- | ---- |
| `label-studio` | Start the Siali Label server. |
| `label-studio -h` `label-studio --help` | Display available command line arguments. |
| `label-studio init <project_name> <optional_arguments>` | Initialize a specific project in Siali Label. |
| `label-studio start <project_name> --init <optional_arguments>` | Start the Siali Label server and initialize a specific project. |
| `label-studio reset_password` | Reset the password for a specific Siali Label username. See [Create user accounts for Siali Label](signup.html). |
| `label-studio shell` | Get access to a shell for Siali Label to manipulate data directly. See documentation for the Django [shell-plus command](https://django-extensions.readthedocs.io/en/latest/shell_plus.html). |
| `label-studio version` | Show the version of Siali Label and then terminates.
| `label-studio user --username <email>` | Show the user info with token.

The following command line arguments are optional and must be specified with `label-studio start <argument> <value>` or as an environment variable when you set up the environment to host Siali Label:

| Command line argument | Environment variable | Default | Description |
| --- | ---- | --- | ---- |
| `-b`, `--no-browser` | N/A | `False` | Do not automatically open a web browser when starting Siali Label. |
| `-db` `--database` | `LABEL_STUDIO_DATABASE` | `label_studio.sqlite3` | Specify the database file path for storing labeling tasks and annotations. See [Database storage](install.html#Database_storage). |
| `--data-dir` | `LABEL_STUDIO_BASE_DATA_DIR` | OS-specific | Directory to use to store all application-related data. |
| `-d` `--debug` | N/A | `False` | Enable debug mode for troubleshooting Siali Label. |
| `-c` `--config` | `CONFIG_PATH` | `default_config.json` | Deprecated, do not use. Specify the path to the server configuration for Siali Label. |
| `-l` `--label-config` | `LABEL_STUDIO_LABEL_CONFIG` | `None` | Path to the label configuration file for a specific Siali Label project. See [Set up your labeling project](setup.html). |
| `--ml-backends` | N/A | `None` | Command line argument is deprecated. Specify the URLs for one or more machine learning backends. See [Set up machine learning with your labeling process](ml.html). |
| `--sampling` | N/A | `sequential` | Specify one of sequential or uniform to define the order for labeling tasks. See [Set up task sampling for your project](start.html#Set_up_task_sampling_for_your_project) on this page. |
| `--log-level` | N/A | `ERROR` | One of DEBUG, INFO, WARNING, or ERROR. Use to specify the logging level for the Siali Label server. |
| `-p` `--port` | `LABEL_STUDIO_PORT` | `8080` | Specify the web server port for Siali Label. Defaults to 8080. See [Run Siali Label on localhost with a different port](start.html#Run-Label-Studio-on-localhost-with-a-different-port) on this page. |
| `--host` | `LABEL_STUDIO_HOST` | `''` | Specify the hostname to use to generate links for imported labeling tasks or static loading requirements. Leave empty to make all paths relative to the root domain. For example, specify `"https://77.42.77.42:1234"` or `"http://ls.example.com/subdomain/"`. See [Run Siali Label with an external domain name](start.html#Run-Label-Studio-with-an-external-domain-name) on this page. |
| `--cert` | `LABEL_STUDIO_CERT_FILE` | `None` | Deprecated, do not use. Certificate file to use to access Siali Label over HTTPS. Must be in PEM format. See [Run Siali Label with HTTPS](start.html#Run-Label-Studio-with-HTTPS) on this page. | 
| `--key` | `LABEL_STUDIO_KEY_FILE` | `None` | Deprecated, do not use. Private key file for HTTPS connection. Must be in PEM format. See [Run Siali Label with HTTPS](start.html#Run-Label-Studio-with-HTTPS) on this page. |
| `--initial-project-description` | `LABEL_STUDIO_PROJECT_DESC` | `''` | Specify a project description for a Siali Label project. See [Set up your labeling project](setup.html). |
| `--password` | `LABEL_STUDIO_PASSWORD` | `None` | Password to use for the default user. See [Set up user accounts](signup.html). |
| `--username` | `LABEL_STUDIO_USERNAME` | `default_user@localhost` | Username to use for the default user. See [Set up user accounts](signup.html). |
| `--user-token` |  `LABEL_STUDIO_USER_TOKEN` | Automatically generated. | Authentication token for a user to use for the API. Must be set with a username, otherwise automatically generated. See [Set up user accounts](signup.html).
| `--agree-fix-sqlite` | N/A | `False` | Automatically agree to let Siali Label fix SQLite issues when using Python 3.6–3.8 on Windows operating systems. | 
| N/A | `LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED` | `False` | Allow Siali Label to access local file directories to import storage. See [Run Siali Label on Docker and use local storage](start.html#Run_Label_Studio_on_Docker_and_use_local_storage). |
| N/A | `LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT` | `/` | Specify the root directory for Siali Label to use when accessing local file directories. See [Run Siali Label on Docker and use local storage](start.html#Run_Label_Studio_on_Docker_and_use_local_storage). |

### Set environment variables
How you set environment variables depends on the operating system and the environment in which you deploy Siali Label. 

In *nix operating systems, you can set environment variables from the command line or with an environment setup file. For example:
```bash
export LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true
```

!!! note
    If you are using docker, you can write all your [environment variables into the `.env`](https://docs.docker.com/compose/env-file/) file.
    
    
    
On Windows, you can use the following syntax:
```bash
set LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true
```

To check if you set an environment variable successfully, run the following on *nix operating systems:
```bash
echo $LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED
```

Or the following on Windows operating systems:
```bash
echo %LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED%
```

## Run Siali Label on localhost with a different port

By default, Siali Label runs on port 8080. If that port is already in use or if you want to specify a different port, start Siali Label with the following command:
```bash
label-studio start --port <port>
```

For example, start Siali Label on port 9001:
```bash
label-studio start --port 9001
```

Or, set the following environment variable:
```
LABEL_STUDIO_PORT = 9001
```

## Run Siali Label on Docker with a different port

To run Siali Label on Docker with a port other than the default of 8080, use the port argument when starting Siali Label on Docker. For example, to start Siali Label in a Docker container accessible with port 9001, run the following: 
```bash
docker run -it -p 9001:8080 -v $(pwd)/mydata:/label-studio/data heartexlabs/label-studio:latest label-studio
```

!!! attention "important"
    As this is a non-root container, the mounted files and directories must have the proper permissions for the `UID 1001`.

Or, if you're using Docker Compose, update the `docker-compose.yml` file that you're using to expose a different port for the NGINX server used to proxy the connection to Siali Label. For example, this portion of the [`docker-compose.yml`](https://github.com/heartexlabs/label-studio/blob/master/docker-compose.yml) file exposes port 9001 instead of port 80 for proxying Siali Label:
```
...
nginx:
    image: nginx:latest
    ports:
      - 9001:80
    depends_on:
      - app
...
```

## Run Siali Label on Docker with a host and sub-path

To run Siali Label on Docker with a host and sub-path, just pass `LABEL_STUDIO_HOST` env variable with sub-path to docker/docker-compose:
```
LABEL_STUDIO_HOST=http://localhost:8080/foo docker-compose up -d
```

## Expose a local Siali Label instance outside using ngrok

Sometimes it's useful to have the LabelStudio instance you're running on your local machine to be reachable over the internet.

One way to do that is to use [ngrok](https://ngrok.io/), a reverse proxy that allows you to expose your instance to the Internet.

1. Install `ngrok`: [Follow the official ngrok guidelines](https://ngrok.com/download)
2. Authenticate the `ngrok` if this is your first time running it (the token can be obtained from [Ngrok dashboard](https://dashboard.ngrok.com/get-started/setup)): `ngrok config add-authtoken <Your token>`
3. Start `ngrok` and point it at Siali Label: `ngrok http --host-header=rewrite 8080`
4. Copy the `Forwarding` URL `ngrok` displays. e.g.: `https://xx-xx-xx-xx.eu.ngrok.io`
5. Pass this url to Siali Label upon startup: 

```bash
# python instance
LABEL_STUDIO_HOST=https://xx-xx-xx-xx.eu.ngrok.io label-studio start
```

```bash
# docker container
docker run -it -e LABEL_STUDIO_HOST=https://xx-xx-xx-xx.eu.ngrok.io -p 8080:8080 -v <yourvolume>:/label-studio/data heartexlabs/label-studio:latest
```

!!! attention "important"
    As this is a non-root container, the mounted files and directories must have the proper permissions for the `UID 1001`.

```bash
# docker-compose
LABEL_STUDIO_HOST=https://xx-xx-xx-xx.eu.ngrok.io docker-compose up -d
```

6. Open the ngrok URL in browser to make sure you see your instance
7. Done


## Run Siali Label on Docker and use Local Storage

To run Siali Label on Docker and reference persistent local storage directories, mount those directories as volumes when you start Siali Label and specify any environment variables you need.

The following command starts a Docker container with the latest image of Siali Label with port 8080 and an environment variable that allows Siali Label to access local files. In this example, a local directory `./myfiles` is mounted to the `/label-studio/files` location. 
```bash
docker run -it -p 8080:8080 -v $(pwd)/mydata:/label-studio/data \
--env LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true \ 
--env LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT=/label-studio/files \ 
-v $(pwd)/myfiles:/label-studio/files \
heartexlabs/label-studio:latest label-studio
```

!!! attention "important"
    As this is a non-root container, the mounted files and directories must have the proper permissions for the `UID 1001`.

By specifying the environment variable `LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT=/label-studio/files`, Siali Label only scans this directory for local files. It's highly recommended to explicitly specify a `LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT` path to secure the volume access from the Docker container to your local machine.

Place files in the specified source directory (`./myfiles` in this example) and reference that directory when you set up [local storage](storage.html#Local_storage). For more information about using volume mounts in Docker, see the [Docker documentation on volumes](https://docs.docker.com/storage/volumes/).  

If you're using Docker Compose, specify the volumes in the Docker Compose YAML file and add the relevant environment variables to the app container. For more about specifying volumes in Docker Compose, see the volumes section of the [Docker Compose file documentation](https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes).


## Run Siali Label with HTTPS

To run Siali Label with HTTPS and access the web server using HTTPS in the browser, use NGINX or another web server to run HTTPS for Siali Label.  


## Run Siali Label on the cloud using Heroku
To run Siali Label on the cloud using Heroku, specify an environment variable so that Siali Label loads. 

```
LABEL_STUDIO_HOST
```

If you want, you can specify a different hostname for Siali Label, but you don't need to.

To run Siali Label with Heroku and use PostgreSQL as the [database storage](storedata.html), specify the PostgreSQL environment variables required as part of the Heroku environment variable `DATABASE_URL`. For example, to specify a PostgreSQL database hosted on Amazon:
```
DATABASE_URL = postgres://username:password@hostname.compute.amazonaws.com:5432/dbname
```
Then you can specify the required environment variables for a PostgreSQL connection as config variables. See [Database storage](storedata.html).

Our Heroku manifest uses [postgresql addon](https://elements.heroku.com/addons/heroku-postgresql) out of the box.
Please notice that the storage capacity is limited.

[<img src="https://www.herokucdn.com/deploy/button.svg" height="30px">](https://heroku.com/deploy?template=https://github.com/heartexlabs/label-studio/tree/master)

Please notice that all uploaded data via import will be lost after a dyno replace since [filesystem is ephemeral](https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem).
Using S3 storage is recommended.

<!--
## Run Siali Label on the cloud using a different cloud provider
To run Siali Label on the cloud using a cloud provider such as Google Cloud Services (GCS), Amazon Web Services (AWS), or Microsoft Azure, 
-->


## Run Siali Label with an external domain name

If you want multiple people to collaborate on a project, you might want to run Siali Label with an external domain name. 

To do that, use the `host` parameter when you start Siali Label. These parameters ensure that the correct URLs are created when importing resource files (images, audio, etc) and generating labeling tasks.   

There are several possible ways to run Siali Label with an external domain name.
 
- Replace the `host` parameter in the file which you specified with `--config` option. If you don't use `--config` then edit `label_studio/utils/schema/default_config.json` in the Siali Label package directory.
- Specify the parameters when you start Siali Label: `label-studio start --host http://your.domain.com/ls-root`.
- Specify the parameters as environment variables `HOST` especially when setting up Docker: `HOST=https://your.domain.com:7777`. 

Or, you can use environment variables:
```
LABEL_STUDIO_HOST = https://subdomain.example.com:7777
```

You must specify the protocol for the domain name: `http://` or `https://`

If your external host has a port, specify the port as part of the host name. 


## Set up task sampling for your project 

When you start Siali Label, you can control the order in which tasks are exposed to annotators for a specific project.  

For example, to create a project with sequential task ordering for annotators:
```bash
label-studio start <project_name> --sampling sequential
```

The following table lists the available sampling options: 

| Option | Description |
| --- | --- | 
| sequential | Default. Tasks are shown to annotators in ascending order by the `id` field. |
| uniform | Tasks are sampled with equal probabilities. |
| prediction-score-min | Tasks with the minimum average prediction score are shown to annotators. To use this option, you must also include predictions data in the task data that you import into Siali Label. |

You can also use the API to set up sampling for a specific project. Send a PATCH request to the `/api/projects/<project_id>` endpoint to set sampling for the specified project. See the [API reference for projects](/api#operation/projects_partial_update). 

Individual annotators can also control the order in which they label tasks by adjusting the filtering and ordering of labeling tasks in the Siali Label UI. See [Set up your labeling project](setup.html).
