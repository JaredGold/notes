# Protobuf

Proto is a file type that can be converted to any language. It is used to create schemas and force data to be returned in a very language neutral way. It is similar to JSON but specifically schema and type specific. Protobuf takes the file following the schema you design and then breaks it down to binary before sending it through the wire. This minimizes the size of the file as all of the uneeded junk is removed.

## Proto Format

The way we create a proto schema file there are some important aspects to remember.

First line we write `syntax =` then the proto version we are using `proto3;`

Followed we can create the schema using the term `message` followed by the name of that message, we then open it up with curly brackets where we will fill it with the data types it takes.

Inside of the `message` we can define the structure on each line. It will look like `data-type name = pos` or `string fName = 1` which implies there will be a `fName` variable of type `string` and it will be the first element in the message.

Example Proto Message:

```protobuf
syntax = "proto3";

message Employee {
	int32 id = 1;
	string name = 2;
	float salary = 3;
}
```

If we want an **Array** of messages we create another message but use the keyword `repeated` followed by the `type` then the `name` and the `position`, which looks like `repeated Employee employees = 1;`

```protobuf
message Employees {
	repeated Employee employees = 1;
}
```

## How to implement in other languages

In order to compile the proto file we have to use the `protoc` or protocompiler. You give it the language you want it to output. It will generate exactly what is needed. This is what makes it language neutral as apposed to language agnostic. 

To download the Proto Compiler visit [here](https://github.com/protocolbuffers/protobuf/releases)

After downloading the protoc you can run it in terminal by browsing to protoc and running it as normal `./protoc` followed by `--js_out=` for javascript out or `--go_out=` for Go etc. After the `=` we follow it with `import_style=commonjs,binary:. employees.proto` to do it in golang we use `protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/file-name.proto` or similar. (Found in docs)

## Create data

First we need to assign the schema in our file (`js`) using `import ./schema/directory` thenwe can use it to create data.

To create an employee we would do the below (in javascript).

```js
const jared = new Schema.Employee();
jared.setId(1);
jared.setName("Jared");
jared.setSalary(13.12);

console.log("My name is " + jared.getName());

const employees = new Schema.Employees();
employees.addEmployees(jared)
```



## Serializing

In order to take advantage of Protobuf after creating our employees or data we then need to serialise the file to make it binary. We do this (in js?) using `name.serializeBinary()` and to desearlize `name.deserializeBinary(data)`.