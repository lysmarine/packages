# Packages
In order to make lysmarine updatable as possible. 
This repo contain procedures and assets required to build and add to the lysmarine's PPA software that don't have any repository yet. 


## rtl-ais
The rtl-ais project is maintained in fork of it's original repository. 
So far, @dgiardini have kindly accepted all PR concerning debian packaging but have no repository, so we only need to clone, build and upload to launchpad 

###### Get source code
``` 
git clone --depth 1 https://github.com/dgiardini/rtl-ais/ ./rtl-ais/rtl-ais
```

###### Build and sign source package
``` 
debuild -S -sa 
```

###### upload the package to launchpad
```
dput ppa:lysmarine/upstream-projects
```

###### ** Optionally build locale package **
```
debuild -us -uc
```


## create_ap
create_ap is a dead project and have no debian package available.

###### Get the project source files 
```
wget https://github.com/oblique/create_ap/archive/v0.4.6.tar.gz
tar -xf v0.4.6.tar.gz
rm v0.4.6.tar.gz
mv create_ap-0.4.6/* createap-0.4.6/
rm -r create_ap-0.4.6
```

###### Build and sign source package
``` 
debuild -S -sa 
```

###### upload the package to launchpad
```
dput ppa:lysmarine/upstream-projects
```


## fbpanel ##
fbpanel is not maintained by it's owner anymore but there is a community around it that keep it up to date. Sadly no one have take the lead to become the next maintainer.

The lysmarine's fork of it apply the minimal amount of patches to make it still running. 

meanwhile the packaging files are maintained in this repository. 

```
git clone --depth 1 git clone https://github.com/lysmarine/fbpanel ./fbpanel/fbpanel
```




## building a package.  
To build a package you must cd into the desired package (createap in this example)  
```
cd createap-4.0.6/
```

#### Build a complete package for direct use. 
```
debuild -us -uc
```

#### Prepare a source package for launchpad.
```
debuild -S -sa 
```




## Notes: 
How to sign your changes with your GPG key ID : 
```
https://techoverflow.net/2019/06/08/how-to-fix-dput-error-58-gpgme_op_verify/
debsign -k [YOUR PGP FINGERPRINT] <filename>.changes
```


