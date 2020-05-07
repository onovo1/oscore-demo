## oscore-edhoc-demo
These are the instructions to install and run the OSCORE EDHOC client and OSCORE EDHOC server in Ubuntu

### Install Rust in Ubuntu:

Rust is installed and managed by the rustup tool. 

```console
$ sudo apt update
$ sudo apt upgrade

$ curl https://sh.rustup.rs -sSf | sh
```
The installation script automatically adds Rust to your system path after your next login. If you need to use Rust immediately without restarting terminal you can add Rust to path manually.
If you are planning to use Add environment variable:

```console
$ source $HOME/.cargo/env
```

Now you can verify the version of Rust installed in your Ubuntu.

```console
$ rustc --version 
```
Rust program needs to be complied before running the file. So you need to install build-essentials


```console
$ sudo apt install build-essential
```

### Running the client 

Go to the client folder and compile the project: 

```console
$ cargo build
```

And run it:

```console
$ ./target/debug/client
```

### Running the server 

Go to server folder and compile the project:

```console
$ cargo build
```
And run it:

```console
$ ./target/debug/server
```

