# inscope
> maybe this tool already exist in go

Bored of parse shodan output for specific domains ?
inscope allows to grep only "\\.sub\\.domain\\.xyz:|\\.domain\\.xyz:"
It's like egrep -f scope.txt but adds regex to scope.txt

```sh
$ chmod +x inscope && mv inscope /usr/bin/
```

```sh
$ cat scope.txt
elastic.co
found.io
swiftype.com
elstc.co
elasticnet.co
eops.nl
elastic-cloud.com
```
```sh
$ inscope scope.txt
# grep -E "\.elastic\.co:|\.found\.io:|\.swiftype\.com:|\.elstc\.co:|\.elasticnet\.co:|\.eops\.nl:|\.elastic-cloud\.com:"
```

```sh
$ shodan search hostname:elastic.co,found.io,swiftype.com,elstc.co,elasticnet.co,eops.nl,elastic-cloud.com --fields hostnames,port --separator " " --limit 1000| awk '{print $1":"$2}' |grep -v ";"| inscope scope.txt

api.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
oss-dependencies-dev.elastic.co:443
api.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
console.us-gov-east-1.aws.elastic-cloud.com:443
api.us-gov-east-1.aws.elastic-cloud.com:443
console.us-gov-east-1.aws.elastic-cloud.com:443
jobs.elastic.co:443
```
