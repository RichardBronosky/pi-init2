我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# Raspberry Pi Pre Init

## Purpose

A program which lets you set up a Raspberry Pi solely by writing to the /boot partition
 (i.e. the one you can write from most computers!).

This allows you to distribute a small .zip file to set up a Raspberry Pi to do anything.
 You tell the user to unzip it over the top of the Pi's boot partition -
 the system can set itself up perfectly on the first boot.

This package contains a single `run-once.sh` script that can be used to do all the setup needed.
 Alternatively, you can create a `run-once.d` and/or a `on-boot.d` directory and put multiple
 scripts in either/each. These folders will be created for you after the first boot and can be used
 at any time.

## Trying it out

- Download and write a standard [Raspbian SD card](https://www.raspberrypi.org/downloads/raspbian/),
  e.g. the [Raspbian Stretch Lite](https://downloads.raspberrypi.org/raspbian_lite_latest).
- Copy the content of this project's [boot folder](https://github.com/RichardBronosky/pi-init2/tree/master/boot)
  to the microSD card's /boot partition.
- Rename either cmdline.txt.stretch or cmdline.txt.jessie to cmdline.txt.orig (this selection will be automatic in a later update)
- Remove the SD card and put it into your Pi.

The Raspberry Pi should now boot several times.
 The first boot takes 2-5 minutes depending on your network,
 and which model of Raspberry Pi you use (I tested with model 3).

By default only a single simple change will be applied. A `/home/pi/.bash_aliases` file will be
 created with `alias ll='ls -la` in it. The `boot/run-once.sh` script includes several commented
 blocks to demonstrate how to accomplish common tasks.

# Building pi-init2

You will need `golang` installed (I'm currently using 1.7) `sudo apt install golang`. Go will need to install required packages. I have tried to make this as easy as calling `make reqs`.

There is a `Makefile` in the root of this project. Calling `make` will compile the [Go](https://golang.org/)
 source code and create `boot/pi-init2` if it doesn't exist. (Use `make clean all` to replace it.)

# How it works

This is really cool. The `cmdline.txt` specifies an `init=/pi-init2` kernel argument to use a
 custom binary in this package in place of the usual systemd init. That binary holds everything
 except for the `cmdline.txt` file (that would be a chicken-egg problem) and the `run-once.sh`
 which you will modify to script your desired setup.

 ## How/Why you should incorporate this project into your Raspberry Pi project

 If you have a project you expect someone to run on an RPi (especially if it would be the RPi's single purpose) you could provide your own `run-once.sh` script that will clone your project, configure, and install it.

# Disclaimer/Credits

This has been tested with this (what I believe to be the latest release) version of [Jessie](http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2017-07-05/) but the instructions above assume Stretch.

Credits go to the following projects:

- [pi-init2](https://github.com/gesellix/pi-init2): This is the fork of this project that I chose to base my fork off of.
- [raspbian-boot-setup](https://github.com/RichardBronosky/raspbian-boot-setup): My first project attempting to accomplish the same goal.
- [PiBakery](https://github.com/davidferguson/pibakery): A good resource to find more blocks to setup your Raspberry Pi.

Any contributions appreciated!
