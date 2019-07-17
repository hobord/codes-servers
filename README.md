# vscode on browser

It is based https://github.com/cdr/code-server

There are preinstalled extensions for each dev stack.

Tags / versions:

- golang version hobord/code-server:golang
- vuejs version hobord/code-server:vuejs
- angular version hobord/code-server:vuejs

## Examples run

```
docker run --rm -p 8443:8443 -name --privileged=true golangcode hobord/code-server:golang
```

or map some local project directory:
```
docker run --rm -p 8443:8443 -v $(pwd):/home/coder/project/src/github.com/{YOURNAME}/{PROJECTREPODIR} -name --privileged=true hobord/code-server:golang
```

## Debuggers

### Golang
  You should run the container with privileged permission ```--privileged=true``` for run debugger.

### Chrome Debugger
  Map the port 9222
  ```
  docker run --rm -p 8443:8443 -p 9222:9222 -name vuejscode hobord/code-server:vuejs

  docker run --rm -p 8443:8443 -p 9222:9222 -name angularcode hobord/code-server:angular
  ```
## Some Startup parameters

- -N, --no-auth,  Start without requiring authentication.
- -H, --allow-http, Allow http connections.
- -P, --password <value>, DEPRECATED: Use the PASSWORD environment variable instead. Specify a password for authentication.
- --disable-telemetry, Disables ALL telemetry.
- --trust-proxy, Trust the X-Forwarded-For header, useful when using a reverse proxy.