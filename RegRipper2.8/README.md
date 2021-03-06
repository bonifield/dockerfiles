## RegRipper 2.8 by [Harlan Carvey](https://github.com/keydet89)

### make the container
- copy the Dockerfile (and optionally sleepy.sh) to your project folder
```
docker build -t regripper .
```

### alias the container
- the path left of the colon is your LOCAL host, the right is inside the container
- adding the source statement to the alias forces the alias to re-evaluate $PWD (though you may need to run the command a second time if it errors out the first time after changing directories)
```
# vim/nano ~/.bashrc
alias rip="source ~/.bashrc && docker run --rm -v $PWD:/home/rr regripper"
# save and exit
. .bashrc
```

### use RegRipper to parse various Windows registry hives
```
rip -h
rip -r SOFTWARE -p uac
rip -r SAM -p samparse
```

### stop the container if running persistent with sleepy.sh for testing (see comments in Dockerfile)
```
docker ps | grep regrip | cut -d ' ' -f 1 | xargs docker stop
or
docker stop `docker ps | grep regrip | cut -d ' ' -f 1`
```

### TODO and known issues
- a small number of plugins produce errors in the container, which can be seen with ...regripper -l (lists all the plugins and, conveniently, errors)
