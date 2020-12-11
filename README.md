# Packages
In order to make lysmarine updatable as possible. 
This repo contain procedures and assets required to build and add to the lysmarine's PPA software that don't have any repository yet. 

First, make sure you have the required dependencies :
```
sudo apt-get install build-essential devscripts lintian
```

## lxpanel-gtk3

###### Get source code
```
wget https://launchpad.net/~mati75/+archive/ubuntu/lubuntu-testing/+sourcefiles/lxpanel/0.10.0-2+ppa2/lxpanel_0.10.0-2+ppa2.debian.tar.xz
7z x ./lxpanel_0.10.0-2+ppa2.debian.tar.xz
tar -xf ./lxpanel_0.10.0-2+ppa2.debian.tar

```

###### Build and sign source package
```
sudo apt install gtk-doc-tools intltool libasound2-dev libiw-dev  libmenu-cache-dev libwnck-dev libfm-gtk-dev libxml2-dev libkeybinder-dev libindicator-dev
sudo apt install libgtkd-3-dev libwnck-3-dev libcurl4-gnutls-dev libkeybinder-3.0-dev

cd ./lxpanel-gtk3/lxpanel-gtk3
```
Replace this line: in /debian/rules
```
dh_auto_configure -- --enable-man --with-plugins=all,-netstat,-pager,-weather --disable-silent-rules --enable-indicator-support --enable-gtk3
```

```
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
dput ppa:lysmarine/upstream-projects ../kplex_1.4.1_source.changes 
```





## kplex

###### Get source code
```
git clone  https://github.com/FredericGuilbault/kplex.git ./kplex/kplex
pushd ./kplex/kplex ; git checkout Feature/debianPackage ; popd 
```

###### Build and sign source package
```
cd ./kplex/kplex
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
dput ppa:lysmarine/upstream-projects ../kplex_1.4.1_source.changes 
```



## rtl-ais
The rtl-ais project is maintained in fork of its original repository. So far, @dgiardini have kindly accepted all PR concerning debian packaging but have no repository, so we only need to clone, build and upload to launchpad 

###### Get source code
```
git clone --depth 1 https://github.com/dgiardini/rtl-ais/ ./rtl-ais/rtl-ais
```

###### Build and sign source package
```
cd ./rtl-ais/rtl-ais
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **

```

###### upload the package to launchpad
```
dput ppa:lysmarine/upstream-projects ../rtl-ais*_source.changes 
```
dput ppa:lysmarine/rtl-ais <source.changes> 


## create_ap
create_ap is a dead project and have no debian package available.

###### Get the project source files 
```
git clone --depth 1 https://github.com/oblique/create_ap/ ./createap/createap/
cp -r ./createap/debian ./createap/createap/
```

###### Build and sign source package
```
cd ./createap/createap/
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
```

###### upload the package to launchpad
```
dput ppa:lysmarine/upstream-projects ../createap_*-ppa2_source.changes 
```



## fbpanel ##
fbpanel is not maintained by it's owner anymore but there is a community around it that keep it up to date. Sadly no one have take the lead to become the next maintainer.

The lysmarine's fork of it apply the minimal amount of patches to make it still running. 

meanwhile the packaging files are maintained in this repository. 

```
git clone --depth 1 https://github.com/lysmarine/fbpanel ./fbpanel/fbpanel
cp -r ./fbpanel/debian ./fbpanel/fbpanel/
```

###### Build and sign source package
```
cd ./fbpanel/fbpanel/
debuild -S
#dpkg-buildpackage -rfakeroot -b -uc -us # ** Optionally build locale package **
```

###### upload the package to launchpad
```
dput ppa:lysmarine/upstream-projects ../fbpanel_7.0.12_source.changes
```



## Notes: 
How to manually sign your changes with your GPG key ID : 
```
https://techoverflow.net/2019/06/08/how-to-fix-dput-error-58-gpgme_op_verify/
debsign -k [YOUR PGP FINGERPRINT] <filename>.changes
```

## Debugging. 

If something fail on launchpad, you should receive an email with the logs of the build process. 
From what I found the build process on launchpad looks like this 
```
dpkg-source -x  *.dsc
tar -xf gcc-4.9.2.tar.xz
tar -xf gdc-20141020.tar.xz
```


