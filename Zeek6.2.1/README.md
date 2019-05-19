## [Zeek Network Monitoring Project](https://github.com/zeek/zeek)

### make the container
- copy the Dockerfile and local.bro to your project file
- note - this local.bro has more logging enabled than the default created at install time; adjust as needed before building the container
- additionally, edit other configs and copy them as needed (broctl.cfg, networks.cfg, node.cfg, etc) (see above Zeek link and read their documentation)
```
docker build -t zeek .
```

### alias the container
- the path left of the colon is your LOCAL host, the right is inside the container
- adding the source statement to the alias forces the alias to re-evaluate $PWD (though you may need to run your command a second time if it errors out immediately after changing directories)
```
# vim/nano ~/.bashrc
alias zeek="source ~/.bashrc && docker run --rm -v $PWD:/usr/local/bro/logs/current zeek"
# save and exit
. .bashrc
```

### use Zeek to generate logs from PCAP files
- note - this version is only meant to parse PCAPs and create logs, and not listen to an interface and generate logs in real-time
```
zeek somefile.pcap
```
