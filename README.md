# Golang

## Required
- Working Go installation
   - use the latest stable version listed here: [golang.org: Downloads](https://golang.org/dl/)
- Editor/IDE for Go

## General
- Do not start a new task before you finished the one before.
- Put this project in a Git repository.
- Each step should be at least one separate commit.
- Do not commit binaries.
- Go code can be formatted with `go fmt`
- When you finished the tasks, zip up the entire Git repository and mail it back to us.

## Tasks
1. Build a go program.
   * Create a folder with the file `go.mod` containing `module training`
   * Create a `main.go` which outputs "Hello World" https://gobyexample.com/hello-world
   * Compile your program with `go build`
2. Build a Go service with an HTTP endpoint which returns the requested path.
   * `curl http://127.0.0.1:3333/xxx` should return `xxx` (https://golang.org/pkg/net/http/)
   * `xxx` should be replaceable by any random characters. Any URL should work!
   * Create an HTTP route with `http.NewServeMux()`
   * Attach a `HandleFunc` to it
   * And start it with `http.ListenAndServe(...)`
3. Write a test which verifies that the response is correct.
   * https://golang.org/pkg/net/http/httptest/ is a great help to write HTTP test cases
   * Create file named `main_test.go` and put the function `func TestShowRequestPathSimpleTest(t *testing.T) {...}` in there
   * Write a test with `httptest.NewRequest()` and `httptest.NewRecorder()` which checks if the returned value is correct
   * If the path is not correct call `t.Error("test failed with path "+path)`
   * The path should be a generated random string
   * Run the tests with `go test`
4. Write a `Makefile` with the following content:
   ```
   export CGO_ENABLED=0
   export GO111MODULE=on
   
   build:
	     go build -o www
   ```
   * What does each line do?
   * What do you expect to happen if you type `make`?
   * Extend the `Makefile` with the targets:
     - `test` should run `go test`
     - `run`  should compile `main.go` to a file named `www` and run it
5. Add a new HTTP endpoint `http://127.0.0.1:3333/prime/xxx`
   * The endpoint should return the x-th prime number:
     - http://localhost:3333/prime/18 => 61
   * Use a primitive algorithm which just divides by smaller numbers to check if the number is prime. 
   * Write a test case for this.
6. Build a Docker container which runs your Go service
   * Create a `Dockerfile` from `alpine:latest`
   * Build the `Dockerfile` with `docker build -t www .` and run it
   * Extend the `Makefile` with the targets:
     - `docker-build`
     - `docker-run` should run in foreground
   * let it run
7. Optimize the speed of the prime finder
   * measure the time which is needed to find the 10000th prime
   * speed it up by at least 10x by optimizing the algorithm
   * speed it up by at least an additional 10x by further optimizing the algorithm
   * try to speed it up by using more CPU cores
   * bonus: implement a Go benchmark comparing the different optimisations
   * make these improvements in separate commits
