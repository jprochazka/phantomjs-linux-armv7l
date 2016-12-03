# PhantomJS 2.1.1 - Scriptable Headless WebKit
## Built for Linux armv7l.

This deployment was built on a fresh Raspbian Jessie Lite 2016-11-25 running on a Raspberry Pi Raspberry Pi 2 Model B. The operating system was fully up to date at the time of the build which was started on December 1st, 2016. It was built using the instructions located on the official PhantomJS website. The following are the commands which were used to build this deployment package.

### Build Steps

Install the packages needed to build PhantomJS using apt-get.
```
sudo apt-get install build-essential g++ flex bison gperf ruby perl \
  libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
  libpng-dev libjpeg-dev python libx11-dev libxext-dev 
```
Obtain the source code needed to build PhantomJS using Git.
```
git clone git://github.com/ariya/phantomjs.git
cd phantomjs
git checkout 2.1.1
git submodule init
git submodule update
```
I changed the next command in order to get a good compile without any out of memory errors. By limiting the jobs to one processor things were apparently slowed down enough that the Raspberry Pi 2 Model B was able to keep up while swapping out memory thus allowing for a build which did not encounter any out of memory errors. This made for a VERY LONG compile time measurable in hours but resulted in a good build.
```
python build.py -j 1
```
The final step was to package the files.
```
./deploy/package.sh
```
The archive loccated on the release page are the untouched results of the build.