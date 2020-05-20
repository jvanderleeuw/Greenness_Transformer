# How To Use This Template
This document describes how to use this transformer template to use the algorithms provided in the algorithm_rgb.py file.

## Assumptions
It is assumed that:
- you are generating a Docker image containing the algorithms and that you have Docker installed on your computer
- are familiar with GitHub template repositories, or know how to use `git`

## Steps to take
The following steps can be taken to develop these algorithms for inclusion into a processing pipeline.

1. [Setup](#setup): Click the `Use this template` button in GitHub to make a copy of this repository (or run `git clone`)
2. [Definitions](#definitions): Fill in and modify the definitions in the algorithm_rgb.py file
3. [Test](#test): Run the `testing.py` script to run algorithms and validate the results
4. [Generate](#generate): Run `generate.py` to create a Dockerfile
5. [Docker](#build_docker): Create a Docker image for the algorithms and publish it
6. [Finishing](#finishing): Finish up your development efforts

### Setup your repo <a name="setup"/>
The first thing to do is to create a copy of this repository has a meaningful name and that you are able to modify.
In GitHub this is easy, browse to this [repository](https://github.com/AgPipeline/template-rgb-plot) and click the `Use this template` button.
You will be led through the steps necessary to create a clone in a location of your choosing.

If you are not on GitHub, you will need to setup your `git` environment and clone the repository.

### Fill in your definitions <a name="definitions" />
To fill in the needed definitions, first open the `algorithm_rgb.py` file in your favorite editor.

If you are modifying your existing code, you should consider updating the version number definition: `VERSION`.
It's assumed that [Semantic Version numbers](https://semver.org/) will be used, but any methodology can be used.

Fill in the algorithm definitions with the creator(s) of the algorithm: `ALGORITHM_AUTHOR`, `ALGORITHM_AUTHOR_EMAIL`, `ALGORITHM_NAME`, and `ALGORITHM_DESCRIPTION`.
Multiple names for `ALGORITHM_AUTHOR` and multiple emails for `ALGORITHM_AUTHOR_EMAIL` are supported.
It's best if only one algorithm name is used, but call it what you want.
The safest algorithm naming convention to use is to convert any white-space or other characters to periods (.) which allows different systems to more-easily change the name, if needed.

Next fill in the citation information that will be used in the generated CSV file: `CITATION_AUTHOR`, `CITATION_TITLE`, and `CITATION_YEAR`.
Be sure to enter the citation information accurately since some systems may expect exact matches.

The names of the variables are used to determine the number of returned values your algorithm produces: `VARIABLE_NAMES`.
Enter each variable name for each returned value, in the order they are returned, separated by a comma.
Be sure to enter them accurately since some systems may expect exact matches.
It is considered an error to have a mismatch between the number of variables names and the number of returned values.

A CSV file suitable for ingestion to [BETYdb](https://www.betydb.org/) is generated depending upon the value of the `WRITE_BETYDB_CSV` variable.
Setting this value to `False` will suppress the generation of this file by default.

A CSV file suitable for ingestion to [TERRA REF Geostreams](https://docs.terraref.org/user-manual/data-products/environmental-conditions) is generated depending upon the value of the `WRITE_GEOSTREAMS_CSV` variable.
Setting this value to `False` will suppress the generation of this file by default.

Be sure to save your changes.

### Add your algorithm <a name="algorithm" />
Open the `testing.py` file in an editor, if it is not open already.

There should be a line in the file containing `calc_val = algorithm_rgb.calculate(np.rollaxis(pix, 0, 3))`. Currently the calculate
function is being used as the algorithm. Change the word "calculate" within this statement to the function that you would like to run
(e.g. excess_red). Functions are located in the algorithm_rgb.py file

Open the `algorithm_rgb.py` file if it isn't opened already.

Modify the rest of the file as necessary if there are additional import statements, functions, classes, and other code needed by your algorithm.

Be sure to save your changes.

### Test your algorithm <a name="test" />
A testing script named `testing.py` is provided for testing your algorithm.
What isn't provided in the template repository are the plot-level RGB images to test against.
It's expected that you will either provide the images or use a standard set that can be downloaded from [Google Drive](https://drive.google.com/file/d/1xWRU0YgK3Y9aUy5TdRxj14gmjLlozGxo/view?usp=sharing).

The testing script requires `numpy` and `gdal` to be installed on the testing system.

The testing script expects to have either a list of source plot image files, or a folder name, or both specified on the command line.

For example, if your files reside in `/user/myself/test_images` the command to test could be the following:
```./testing.py /user/myself/test_images```

### Generate the docker build command file <a name="generate" />
Now that you have created your algorithm and tested it out to your satisfaction, it's time to make a Docker image so that it can run as part of a workflow.

To assist in this effort we've provided a script named `generate.py` to produce a file containing the Docker commands needed.
Running this script will not only produce a Docker command file, named `Dockerfile` but also two other files that can be used to install additional dependencies your algorithm needs.
These two other files are named `requirements.txt` for additional Python modules and `packages.txt` for other dependencies.

To generate these files, just run `generate.py`.

If your algorithm has additional python module dependencies, edit `requirements.txt` and add the names of the modules.
The listed modules will then be installed as part of the Docker build process.

If there are other dependencies needed by your algorithm, add them to the `packages.txt` file.
The packages listed will be installed using `apt-get` as part of the Docker build process.

### Create the Docker image <a name="build_docker" />
Now that you have generated your `Dockerfile` and specified any Python modules and other packages needed by your algorithm, you are ready to create a Docker image of your algorithm.

A sample Docker build command could be: ```docker build -t my_algorithm:latest ./```
Please refer to the Docker documentation for additional information on building a docker image.

Once the image is built, you can run it locally or push it to an image repository, such as [DockerHub](https://hub.docker.com/).
Please note that there may be naming requirements for pushing images to a repository.

**Testing the Docker image**
Using the same image setup as used when [testing your algorithm](#test), a sample command line to run the image could be:
```docker run --rm -it -v `pwd`:/mnt --entrypoint bash my_algorithm:latest```

Breaking apart this command line, we have the following pieces:
- `docker run` tells Docker to run an instance of the image (specified later in the command)
- `--rm` tells Docker to remove the container (an image instance) when it's completed
- `-it` tells Docker to start a container, add a stdin stream, and add a terminal driver
- `-v` tells Docker to bind mount a volume. Volumes enable data to be saved and shared between containers. They
are directories or files that exist as normal directories and files on the host filesystem
- ``pwd`:/mnt`` specifies the *current working directory* path is to be made available as */mnt* in the container
- `--entrypoint bash` overrides the default entrypoint and defines a container with bash as the environment used to run the container
- `my_algorithm:latest` is the image to run (the running image is known as a *container*)

At this point, you should see a prompt that starts with "extractor". From here we mount the testing.py file and the image file folder:
```/mnt/testing.py /mnt/images```

- `"mnt/testing.py` specifies that we want to mount the testing.py file
- `"/mnt/images"` specifies to mount the images folder where the plot-level image files are located

After pressing enter, you should see the results of the calculation on all of the image files specified. 

### Finishing up <a name="finishing" />
Now that you've tested the algorithms, there's a few more things to take care of:

1. Make sure you've checked in your changes into source control; you don't want to lose all that hard work!
2. Update the README.md file, filling out the sections with information on your algorithm; others will want to know so they can use it!
3. Submit any requests to our ticketing system on GitHub:  https://github.com/AgPipeline/computing-pipeline/issues/new/choose

