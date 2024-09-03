# Olvid Daemon gRPC API

## I. Introduction
This repository is part of the Olvid bots framework. If you are lost you might start here: [Quickstart](https://github.com/olvid-io/Olvid-Bot-Quickstart)

Note that the usage of this framework is part of Olvid's paying features. You can use this repository to deploy and test framework possibilities, but if you want to use it without limitations, please contact the Olvid team at [bot@olvid.io](mailto:bot@olvid.io).

This repository contains .proto files describing grpc services implemented by Olvid daemon.
You can compile these files in any language using `protoc` to interact with a daemon instance.

If you're unsure about what you're doing, we recommend starting with our higher-level Python library to interact with the Olvid daemon.

## II. Project Structure

We have three kind of services:
- **Command service**: as in a REST api request data to daemon (List, Get, ...), update data (Update, delete, ...), or run specific operation (ex: introduce a contact to another).
- **Admin service**: equivalent to command api, but you need a client key with admin permissions.
- **Notification service**: subscribe to a notification and receive a message every time something happen (ex: a message have been received).

## III. Entities

Services are organized around entities representing olvid concepts.
All these concepts are really close from entities as you will find in your Olvid application.
You can imagine a daemon as your Olvid mobile application that can be used within an api.

Here is a list of main entities:
- identity
- invitation
- attachment 
- client_key 
- contact 
- discussion 
- group 
- message 
- storage 

For each entity you will find or more protobuf messages to define it in a file named `entity_name.proto` in [datatypes](./olvid/daemon/datatypes/v1) module. 

## IV. Services
For main entities (identity, discussion, message, ...) you will find a command and a notification service.
Each service implements rpc (methods) to manage them and be notified every time an event related to this entity happen.

Methods might be unique but some are implemented regularly.
For example most service implements a List and a Get method.
