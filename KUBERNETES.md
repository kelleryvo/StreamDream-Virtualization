kubectl exec $POD_NAME env

kubectl exec -ti $POD_NAME bash

Show Debug Log:
```
pred='process matches ".*(ocker|vpnkit).*"
  || (process in {"taskgated-helper", "launchservicesd", "kernel"} && eventMessage contains[c] "docker")'
/usr/bin/log stream --style syslog --level=debug --color=always --predicate "$pred"
```

curl -k https://localhost:6443/api/v1/node

kubectl --context docker-for-desktop get nodes