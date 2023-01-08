# Using a debugger with Go from VS Code

A debugger can often be a very helpful piece of software to use.

At some point I will link to or write a good guide to using one, but for now, here are some command lines that were useful for remote debugging inside a docker image:

1. Run your docker container exposing port 2345: `docker run -it --rm -v $(pwd):$(pwd) --workdir $(pwd) -p 127.0.0.1:2345:2345 golang:1.19.4-alpine3.17`
2. Install `dlv`, the debugger: `go install github.com/go-delve/delve/cmd/dlv@latest`
3. Build your Go code with debugging support: `CGO_ENABLED=0 go build -gcflags "all=-N -l" -o ./app`
4. Start your program under the debugger: `dlv --listen=:2345 --headless=true --log=true --log-output=debugger,debuglineerr,gdbwire,lldbout,rpc --accept-multiclient --api-version=2 exec ./app`
5. In VS Code, Start Debugging, set up a run configuration pointing at 127.0.0.1:2345

References:

* https://github.com/golang/vscode-go/wiki/debugging
* https://github.com/golang/vscode-go/wiki/debugging#remote-debugging
