# Packages
In order to make lysmarine updatable as possible. 
This repo contain procedures and assets required to build and add to the lysmarine's PPA software that don't have any repository yet. 

First, make sure you have the required dependencies :
```
sudo apt-get install build-essential devscripts lintian
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


