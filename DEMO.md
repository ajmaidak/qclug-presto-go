You can build go with either the 'gc' go complier or 'gccgo'

I'm not going to bootstrap the compiler, we'll just get go installed via dnf: ```dnf install golang-bin```

I don't think that this is any different then downloading the go1.6.3.linux-amd64.tar.gz archive and extracting it and adding the "go" bin to your path.

It takes second to get used to GO, similar to a java "CLASSPATH" variable you need to set our GOPATH.  The GOPATH is where all your go "work" sits.  Since go is strict about convention rather then configuration nothing like a Makefile exists.  So to even get your go program to build something you have to structure your go path in the way "go" expects it to be.

I find it strange that your GOPATH must be an absolute path rather then something relative...  But hey fuck me, I'm a bad programmer.

$ mkdir -p ~/ws/gopath/{bin,src,pkg}
$ cd ~/ws/gopath
$ export GOPATH=/home/ajmaidak/ws/gopath

Ok, your first go program should exist in "src/github.com/<user>/hello"

$ mkdir -p src/github.com/ajmaidak/hello
$ vi src/github.com/ajmaidak/hello/hello.go
package main

import "fmt"

func main() {
    fmt.Printf("hello, world\n")
}

If you much up the sytle you can fix it with gofmt:

$ gofmt -w src/github.com/ajmaidak/hello/hello.go

The -w switch will re-write the file rather the write things to standard out.

Alright, lets build hello world: 

$ go install github.com/ajmaidak/hello

Assuming your GOPATH is set correctly you should get a lovely 2.3MB binary at $GOPATH/bin/hello:

$ ls -l $GOPATH/bin/hello 
-rwxr-xr-x. 1 ajmaidak ajmaidak 2366920 Aug  9 23:10 bin/hello

$ GOPATH/bin/hello 
hello, world


... Return to Typing Demo...

You get fetch remote packages via the "go get" command:

$ go get github.com/golang/example/hello

$ ls src/github.com/golang/example/hello/
hello.go

$ $GOPATH/bin/hello 
Hello, Go examples!

You can see geting the "example/hello" package from golgan brought a bunch of stuff:



[ajmaidak@antec go]$ tree
.
├── bin
│   └── hello
├── pkg
│   └── linux_amd64
│       └── github.com
│           ├── ajmaidak
│           │   └── stringutil.a
│           └── golang
│               └── example
│                   └── stringutil.a
└── src
    └── github.com
        ├── ajmaidak
        │   ├── hello
        │   │   └── hello.go
        │   └── stringutil
        │       └── reverse.go
        └── golang
            └── example
                ├── appengine-hello
                │   ├── app.go
                │   ├── app.yaml
                │   ├── README.md
                │   └── static
                │       ├── favicon.ico
                │       ├── index.html
                │       ├── script.js
                │       └── style.css
                ├── gotypes
                │   ├── defsuses
                │   │   └── main.go
                │   ├── doc
                │   │   └── main.go
                │   ├── go-types.md
                │   ├── hello
                │   │   └── hello.go
                │   ├── hugeparam
                │   │   └── main.go
                │   ├── implements
                │   │   └── main.go
                │   ├── lookup
                │   │   └── lookup.go
                │   ├── Makefile
                │   ├── nilfunc
                │   │   └── main.go
                │   ├── pkginfo
                │   │   └── main.go
                │   ├── README.md
                │   ├── skeleton
                │   │   └── main.go
                │   ├── typeandvalue
                │   │   └── main.go
                │   └── weave.go
                ├── hello
                │   └── hello.go
                ├── LICENSE
                ├── outyet
                │   ├── containers.yaml
                │   ├── Dockerfile
                │   ├── main.go
                │   └── main_test.go
                ├── README.md
                ├── stringutil
                │   ├── reverse.go
                │   └── reverse_test.go
                └── template
                    ├── image.tmpl
                    ├── index.tmpl
                    └── main.go

31 directories, 38 files


We can compile and run the "outyet" webserver:

$ vi src/github.com/golang/example/outyet/main.go
$ go install github.com/golang/example/outyet
$ $GOPATH/bin/outyet

(check out port 8080)

Try to build packer... Cry.







