# Outfox OS #

## Setting up your machine ##
In order to build OFOS, you must be running a 64bit Linux distribution. Google recommends using
Ubuntu for this, and all of their instructions apply to Ubuntu.  You can follow the instructions
for preparing the machine for building [here](https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment).

Once your machine has all of the dependencies needed, return here and follow the rest of the instructions
to download the OFOS project.

## Grabbing the source ##

[Repo](http://source.android.com/source/developing.html) is a tool provided by Google that
simplifies using [Git](http://git-scm.com/book) in the context of the Android source.

### Installing Repo ###

```bash
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/.bin
$ PATH=~/.bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo

# Make Repo executable
$ chmod a+x ~/.bin/repo
```

### Initializing Repo ###

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE
$ cd WORKSPACE

# Install Repo in the created directory
# Use a real name/email combination, if you intend to submit patches
$ repo init -u https://github.com/OutfoxOs/android -b marshmallow
```

### Initializing Experimental Repo ###

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE
$ cd WORKSPACE

# Install Repo in the created directory
# Use a real name/email combination, if you intend to submit patches
$ repo init -u https://github.com/OutfoxOs/android -b experimental
```


### Downloading the source tree ###

This is what you will run each time you want to pull in upstream changes. Keep in mind that on your
first run, it is expected to take a while as it will download all the required Android source files
and their change histories.

```bash
# Let Repo take care of all the hard work
#
# The -j# option specifies the number of concurrent download threads to run.
# 4 threads is a good number for most internet connections.
# You may need to adjust this value if you have a particularly slow connection.
$ repo sync -j4
```

#### Syncing specific projects ####

In case you are not interested in syncing all the projects, you can specify what projects you do
want to sync. This can help if, for example, you want to make a quick change and quickly push it
back for review. You should note that this can sometimes cause issues when building if there is
a large change that spans across multiple projects.

```bash
# Specify one or more projects by either name or path

# For example, enter OutfoxOs/android_frameworks_base or
# frameworks/base to sync the frameworks/base repository

$ repo sync PROJECT
```

## Building ##

The bundled builder tool `./rom-build.sh` handles all the building steps for the specified device
automatically. As the device value, you just feed it with the device codename (for example,
'hammerhead' for the Nexus 5).

```bash
# Go to the root of the source tree...
$ cd WORKSPACE
# ...and run the builder tool.
$ ./rom-build.sh DEVICE
```

