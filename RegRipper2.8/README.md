## RegRipper 2.8 by [Harlan Carvey](https://github.com/keydet89)

### make the container
- copy the Dockerfile (and optionally sleepy.sh) to your project folder
```
docker build -t regripper .
```

### use RegRipper to parse various Windows registry hives
- note:  the path left of the colon is your LOCAL host, the right is inside the container
```
docker run --rm -v `pwd`:/home/rr regripper -r SOFTWARE -p uac
docker run --rm -v `pwd`:/home/rr regripper -r SAM -p samparse
```

### stop the container if running persistent (see comments in Dockerfile)
```
docker ps | grep regrip | cut -d ' ' -f 1 | xargs docker stop
or
docker stop `docker ps | grep regrip | cut -d ' ' -f 1`
```
