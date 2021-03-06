[![Build Status](https://travis-ci.org/chclaus/dt.svg?branch=master)](https://travis-ci.org/chclaus/dt)
[![Go Report](https://goreportcard.com/badge/github.com/chclaus/dt)](https://goreportcard.com/report/github.com/chclaus/dt)

# dt - the dev toolbelt

The dev toolbelt is a fast and flexible tool to handle common use
cases of your daily work. Use cases you generally use some online
tools.

## Table of Contents

- [Example](#example)
- [Installation](#installation)
  * [Install via go](#installation)
  * [Install via Homebrew](#install-via-homebrew)
  * [Install via Docker](#install-via-docker)
  * [Shell Completions](#shell-completions)
- [Commands](#commands)
  * [URI](#uri-command)
  * [Base64](#base64-command)
  * [Hash](#hash-command)
  * [UUID](#uuid-command)
  * [JWT](#jwt-command)
  * [Random](#random-command)
  * [Date](#date-command)
  * [HTML](#html-command)
  * [Server](#server)
  * [Completion](#shell-completions)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

# Example
<img src="demo_v1_0_0.gif?raw=" width="672px"></img>

## Installation
If you've go installed and your `$GOPATH` is set, you can easily install
dt with:

    go get github.com/chclaus/dt

### Install via Homebrew

    brew tap chclaus/dt git@github.com:chclaus/dt.git
    brew install dt

### Install via Docker

    docker pull chclaus/dt:latest
    docker run --rm chclaus/dt:latest version

### Shell completions
If you installed the tool via homebrew and use either bash or zsh as shell, 
you don't need to worry about anything else.

If you used the native installation, you can easily create an autocompletion:

#### Bash
Write bash completion code to a file and source if from `.bash_profile`:

    dt completion --shell bash > ~/.dt_completion.sh
    printf "\n# dt bash completion\nsource '$HOME/.dt_completion.sh'" >> $HOME/.bash_profile
    source $HOME/.bash_profile

#### Zsh
Set the dt completion code for zsh to autoload on startup:

    dt completion --shell zsh > "${fpath[1]}/_dt"


## Build
To build the project you can clone the repository with...

    git clone git@github.com:chclaus/dt

... and build and install the binary with

    cd dt && go install

### Build with Docker
To build the repository with docker, do the following:

    git clone git@github.com:chclaus/dt
    cd dt
    docker build -t dt .
    docker run --rm dt version

## Commands

### URI command
- Encodes an URI to a safe representation
- Decodes an already encoded URI

### Base64 command
- Encodes a string to it's base64 representation
- Decodes a base64 string to it's plain representation

The base64 command can be used with different encodings:
- Standard, follows RFC 4648
- Standard Raw, follows RFC 4648 but with without padding
- URL, follows the alternative RFC 4648
- URL Raw, follows the alternative RFC 4648 but with without padding

### Hash command
Returns the hash representation of an input in different hash formats:
- md5
- sha1
- sha256
- sha3_256
- sha3_512
- sha512
- bcrypt

### UUID command
Returns a new random UUID. You can specify the generated UUID version:

- Version 1, based on timestamp and MAC address (RFC 4122)
- Version 2, based on timestamp, MAC address and POSIX UID/GID (DCE 1.1)
- Version 3, based on MD5 hashing of (namespace(UUID), value) (RFC 4122)
- Version 4, based on random numbers (RFC 4122)
- Version 5, based on SHA1 hashing of (namespace(UUID), value) (RFC 4122)

### JWT command
Decodes a jwt and pretty prints the resulting json. You can also pass
a secret (base64 or plain) within a file or as program argument to verify
the jwt signature.

### Random command
Generates random strings and numbers. Currently supported functions are:
- Generates a random string, based on an alphabet with a specific length.
- Generates a random string with alphanumeric letters.
- Generates a random string with a alphanumeric and special characters.
- Generates random numbers with a specific length.

### Date command
Date conversions:
- time millis to RFC 3339
- time nanos to RFC 3339
- RFC 3339 to time millis

### HTML command
Escapes and unescapes HTML
- transforms a string to an escaped html sequence
- reads a file and prints an escaped html sequence
- unescapes an escaped html sequence to it's raw representation

### Server
Starts a simple web server to serve static content. You can specify
hostname and port and must set a folder to serve.

You can also pass an option `-o` to open your default system browser
that points automatically to the served url.

## Configuration
You can configure a some default behaviors of dt to fit your needs.
Just place a file `.dt.yaml` into your home directory, you can configure
the following options:

```yaml
server:
  port: 3001
  address: 127.0.0.1
  openBrowser: true
uuid:
  namespace: cacae610-c76a-4736-90ef-0271126b4346
  version: 4
base64:
  encoding: std
random:
  algorithm: complex
  length: 20
hash:
  algorithm: bcrypt
  cost: 12
jwt:
  secret: foobar
  secretFile: /path/to/your/secret/file
  base64Secret: false
```

For more informations, please take a look in the examples directory.

## Contributing
Everyone is welcome to create pull requests for this project. If you're
new to github, take a look [here](https://help.github.com/categories/collaborating-with-issues-and-pull-requests/)
to get an idea of it.

If you've got an idea of a function that should find it's way into this
project, but you won't implement it by yourself, please create a new
issue.

Please ensure, that all contributions match the MIT license.

## License
dt (dev-toolbelt) is released under the MIT license. See [LICENSE.txt](LICENSE.txt)
