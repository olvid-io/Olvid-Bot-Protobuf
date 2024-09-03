# Olvid Daemon gRPC API

## Introduction

Welcome to the Olvid Daemon gRPC API repository, part of the Olvid bots framework. If you're new here, consider starting with our [Quickstart guide](https://github.com/olvid-io/Olvid-Bot-Quickstart).

**Note**: The usage of this framework is a paying feature. You can use this repository to deploy and test the framework's possibilities, but if you want to use it without limitations, please contact the Olvid team at [bot@olvid.io](mailto:bot@olvid.io).

This repository contains `.proto` files describing gRPC services implemented by the Olvid daemon. You can compile these files in any language using `protoc` or `[buf](https://buf.build/)` to interact with a daemon instance.

If you're unsure about what you're doing, we recommend starting with our higher-level [Python library](https://github.com/olvid-io/Olvid-Bot-Python-Client) to interact with the Olvid daemon.

## Project Structure

Our project is organized around three types of services:

* **Command Service**: Similar to a REST API, this service allows you to request data from the daemon (e.g., List, Get), update data (e.g., Update, Delete), or run specific operations (e.g., send a message, introduce contacts to one another).
* **Admin Service**: Equivalent to the Command API, but requires a client key with admin permissions to use methods.
* **Notification Service**: Subscribe to notifications and receive messages whenever an event occurs (e.g., a message is received, you joined a group).

## Entities

Our services are organized around entities that represent Olvid concepts. These concepts are similar to those found in your Olvid application.

You can think of the daemon as your Olvid mobile application, accessible via an API.

Here's a list of the main entities:

* **Identity**: a Profile in your Olvid application. (Almost) all other entities are grouped by identity (e.g. you can only access your current identity messages, discussions, ...) 
* **Client** Key: a key used to connect to daemon. Any client will need one to authenticate. Client keys are associated with a specific identity except admin client keys that can specify the identity they want to use.  
* **Contact**: another Olvid identity you met. 
* **Group**: a collection of one or more users sharing a discussion.
* **Discussion**: regroups messages exchanged with a contact or a group.
* **Message**: always related to a discussion. Can be inbound or outbound.
* **Attachment**: a file attached to a message. Can be inbound or outbound.
* **Storage**: a way to persist data you need. Backup resilient, element will remain associated to the same identity or discussion after a backup even if ids changes. 
* **Invitation**: represents requests and / or responses to meet new contacts or join groups.

For each entity, you'll find one or more protobuf messages that define it in a file named `entity_name.proto` within the [datatypes](./olvid/daemon/datatypes/v1) module.

## Services

For main entities (e.g., Identity, Discussion, Message), you'll find a Command and a Notification service. Each service implements RPC methods to manage these entities and receive notifications whenever an event related to them occurs.

Some methods are implemented in every command services, for example List and Get methods. Some other methods and notifications are more specific to the entity.
