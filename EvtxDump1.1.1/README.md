## EvtxDump 1.1.1 by [Andreas Schuster](https://mobile.twitter.com/forensikblog?lang=en)

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
alias evtxdump="source ~/.bashrc && docker run --rm -v $PWD:/home/ed evtxdump"
# save and exit
. .bashrc
```

### use EvtxDump to parse various Windows event logs
```
evtxdump Security.evtx
```

### optional - use pretty-xml.py to beautify the output
```
evtxdump Security.evtx > Security.xml
pretty-xml.py Security.xml
```
