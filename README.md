# DNF renku-project-template

A repository of base templates for new Renku projects. The next sections outline
what different files in the template are used for.

## For running interactive environments from Renkulab

`Dockerfile` - File for building a docker image that you can launch from renkulab,
to work on your project in the cloud. Template-supplied contents will allow you to
launch an interactive environment from renkulab, with pre-installed renku CLI and
software dependencies that you put into your `requirements.txt`, `environment.yml`,
or `install.R`. You can and should add to this `Dockerfile` if libraries you install
require linux software installations as well; for more information see:
 https://github.com/SwissDataScienceCenter/renkulab-docker.

`.gitlab-ci.yml` - Configuration for running gitlab CI, which builds a docker image
out of the project on `git push` to renkulab so that you can launch your interactive
 environment (don't remove, but you can modify to add extra CI functionality).

`.dockerignore` - Files and directories to be excluded from docker build (you can
  append to this list); https://docs.docker.com/engine/reference/builder/#dockerignore-file.

### Setting the version of the renku-cli

The default version of the renku CLI used in the interactive environment is
specified in the Dockerfile in a line similar to this:

```
ARG RENKU_VERSION={{ __renku_version__ | default("0.16.0") }}
```

Due to some issues building the images and uploading them to docker hub. The version of Renku was specified manually:

```
ARG RENKU_VERSION"1.8.0"
```

## For organizing project files

`data` - Initially empty directory where `renku dataset` creates subdirectories
for your named datasets and the files you add to those datasets (if you haven't
or will not be creating renku datasets, you can remove this directory).

`notebooks` - Initially empty directory to help you organize jupyter notebooks
(not a requirement, you can remove this directory).

Any folder you may want to add to the docker image should be copied in the dockerfile using: 

```
COPY folder /home/jovyan/folder
```

## For git to ignore

`.gitignore` - Files and directories to be excluded from git repository (this
  template only requires the #renku section, but the others are nice-to-haves
  for common paths to ignore).

## How to work with this template:


### Build docker image

Replace `python-minimal` by any other folder template.

```
docker build --tag user/repo:tag python-minimal
```

### Push container to docker hub

```
docker push user/repo:tag
```

### Pull container

```
docker pull user/repo:tag
```

### Run container

```
docker run -p 8888:8888 --name [Container-name] user/repo:tag jupyter lab
```

## Useful tools

- Github Desktop: https://desktop.github.com/
- Docker Desktop: https://www.docker.com/products/docker-desktop/
- Kinematic: https://github.com/docker/kitematic