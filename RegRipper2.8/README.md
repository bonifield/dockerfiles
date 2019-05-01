### RegRipper 2.8 by [Harlan Carvey](https://github.com/keydet89)

### Making the Container
- copy the Dockerfile (and optionally sleepy.sh) to your project folder
- build the container
```
docker build -t regripper .
```
- use RegRipper to parse various hives
- note:  the path left of the colon is your LOCAL host, the right is inside the container
```
docker run --rm -v `pwd`:/home/rr regripper -r SOFTWARE -p uac
docker run --rm -v `pwd`:/home/rr regripper -r SAM -p samparse
```
- stop container if running persistent (see comments in Dockerfile)
```
docker ps | grep regrip | cut -d ' ' -f 1 | xargs docker stop
or
docker stop `docker ps | grep regrip | cut -d ' ' -f 1`
```
