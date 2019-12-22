## Laika BOSS by [Lockheed Martin](https://github.com/lmco/laikaboss)

### this version is very basic - it does NOT easily support cloudscan, laikad, and milter

### make the container
- copy the Dockerfile to your project folder
```
docker build -t laikaboss .
```

### alias the container
- with -v, left of the colon is your LOCAL host, right is the working path INSIDE the container
- adding the source statement to the alias forces the alias to re-evaluate $PWD (though you may need to run the command a second time if it errors out the first time after changing directories)
```
# vim/nano ~/.bashrc
alias laikaboss="source ~/.bashrc && docker run --rm -v $PWD:/lb laikaboss"
# save and exit
. .bashrc
```

### use Laika BOSS to parse and analyze files
```
# run the container directly
docker run --rm -v `pwd`:/lb laikaboss YOURFILEGOESHERE.zip | jq -C . | less -r

# run via alias
laikaboss YOURFILEGOESHERE | jq -C . | less -r
```

### stop the container if it errors for some reason and does not exit and remove
```
docker ps | grep laikaboss | cut -d ' ' -f 1 | xargs docker stop
or
docker stop `docker ps | grep laikaboss | cut -d ' ' -f 1`
```
