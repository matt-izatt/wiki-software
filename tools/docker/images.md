# Images

The basis of any Docker image is the Dockerfile. This is a list of instructions that form a recipe for an image. When an image is built, Docker steps through the instructions in the Dockerfile and carries out the directive at each step. Directives are keywords which (usually) form the start of a new line in the Dockerfile.

## Dockerfile

### Creation

A Dockerfile is simply a file at the root of the project called Dockerfile:

```bash
touch Dockerfile
```

A .dockerignore file can also be created to exclude files and directories from Dockerfile directives:

```bash
touch .dockerignore
```

### Directives

#### FROM

The `FROM` directive usually starts a Dockerfile. It informs Docker which image should be inherited from as a basis from which to run the rest of the directives in the Dockerfile.

```
FROM base-image
```

As well as inheriting from base images, it's also possible to start a completely new Docker image which does not include any layers. This can be achieved by using the special image name `scratch`. This tells Docker it shouldn't try to inherit from any other image, but start a brand new set of layers. In fact, this is how a large number of 'standard' base images start, such as the Docker versions of Linux distributions, by starting from `scratch` and copying in all of the files that build up that distribution of Linux.

#### WORKDIR

The `WORKDIR` directive sets the working directory in the container. All `COPY` commands use this as the root unless otherwise specified.

```
WORKDIR /app
```

#### COPY

The `COPY` directive allows the copying of files from the host's local filesystem into the Docker image being built.

```
COPY package.json .
```

#### RUN

The `RUN` directive runs commands whilst building a Docker image. This is sometimes confused, when starting out with Docker, with the `CMD` directive which runs commands when the image is created as a _container_ instance.

```
RUN npm install
```

#### CMD

The `CMD` directive is usually the last directive in a Dockerfile. This informs Docker what should be run when a container instance is created from an image.

```
CMD ["npm", "start"]
```

#### EXPOSE

The `EXPOSE` directive is used as a form of documentation to tell the user which port the application would like to expose. It does not publish the port at run time. This is done with the `-p` argument to `docker run`.

#### ENV

The `ENV` directive  allows you to set environment variables inside the Dockerfile

```
ENV MY_NAME="John Doe"
ENV MY_DOG=Rex\ The\ Dog
ENV MY_CAT=fluffy
```

The environment variables set using `ENV` will persist when a container is run from the resulting image. You can view the values using `docker inspect`, and change them using `docker run --env <key>=<value>`.

### Caching

Each step in a dockerfile is cached the first time `docker build` is run. Then for subsequent runs it compares the cached files with the new files. It will then only run the steps for files that have changed onwards.&#x20;

For example in the following dockerfile `COPY package.json` on its own before `COPY . . `means that `RUN npm install` will only be run if the `package.json` has changed on the local machine.

{% code title="Dockerfile" %}
```
FROM node:15
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```
{% endcode %}



## CLI

### Build

```bash
 docker  build  --tag <iname>  <dir>
```

### List

```bash
docker  image ls
```

### Remove

```bash
docker  image rm  <iname>
```

