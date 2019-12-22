## Laika BOSS by [Lockheed Martin](https://github.com/lmco/laikaboss)

### this version is very basic - it does NOT easily support cloudscan, laikad, and milter

### make the container
- copy the Dockerfile to your project folder
```
docker build -t laikaboss .
```

### alias the container in .dockerfunc
- with -v, left of the colon is your LOCAL host, right is the working path INSIDE the container
- add the following to your home location's .dockerfunc (or create new if it does not exist)
```
#!/bin/bash
laikaboss(){
	docker run --rm -v $PWD:/lb laikaboss "$@"
}

# save and exit, then run
# . .dockerfunc
```

### use Laika BOSS to parse and analyze files
```
# run the container directly
docker run --rm -v `pwd`:/lb laikaboss YOURFILEGOESHERE.zip | jq -C . | less -r

# run via function name (alias)
laikaboss YOURFILEGOESHERE | jq -C . | less -r
```

### stop the container if it errors for some reason and does not exit and remove
```
docker ps | grep laikaboss | cut -d ' ' -f 1 | xargs docker stop
or
docker stop `docker ps | grep laikaboss | cut -d ' ' -f 1`
```
