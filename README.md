# BlueZero plugin for V-REP

### Compiling

1. Install required packages for [v_repStubsGen](https://github.com/fferri/v_repStubsGen): see v_repStubsGen's [README](external/v_repStubsGen/README.md)
2. Checkout and compile
```sh
$ git clone --recursive https://github.com/fferri/v_repExtBlueZero.git
$ cmake .
$ cmake --build .
```

### Compiling protobuf messages

In order to generate Lua code for protobuf messages, you need lua, luarocks, python and protobuf-compiler. Refer to your package manager about how to install these packages.

You also need 'protobuf' luarock:

```sh
$ luarocks install protobuf
```

Compiling a message:

```sh
$ protoc \
    --lua_out=. \
    --plugin=$HOME/.luarocks/lib/luarocks/rocks-5.1/protobuf/1.1.1-0/protoc-plugin/protoc-gen-lua \
    file.proto
```

Alternatively, you can use docker image federicoferri/lua-protobuf:

```sh
$ docker pull federicoferri/lua-protobuf
```

and compile messages with:

```sh
$ docker run \
    --mount type=bind,source=$PWD,target=/work \
    --workdir=/work \
    lua-protobuf:latest \
    protoc \
        --lua_out=. \
        --plugin=/usr/local/lib/luarocks/rocks/protobuf/1.1.1-0/protoc-plugin/protoc-gen-lua \
        file.proto
```

