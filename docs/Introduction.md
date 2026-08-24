# Introduction

**Jog is a modular framework and ecosystem for building Roblox games with Luau.**

Jog provides a structured way to organize game logic into **Systems**, extend the framework through **Addons**, and share reusable functionality through **Packages**. It also provides tooling through the Jog Plugin to make developing with the ecosystem easier.

The goal of Jog is to make Roblox projects **modular, predictable, extensible, and easy to maintain** through a clear and opinionated architecture without unnecessarily restricting how developers build their games.

## What is Jog?

At its core, Jog manages the lifecycle and relationships between the different parts of your game.

```text
Jog Project
├── Systems
│   └── Game logic
├── Addons
│   └── Framework extensions
└── Packages
    └── Reusable libraries
```

Jog handles things such as:

* Loading and initializing Systems and Addons.
* Resolving System dependencies.
* Managing System and Addon lifecycles.
* Separating server and client logic.
* Providing shared state between modules belonging to the same System.
* Allowing Addons to extend and interact with the framework.
* Providing a consistent way to import Packages and Addons.
* Providing development tooling and IntelliSense through the Jog Plugin.

Jog is **opinionated where structure matters**, while remaining flexible in how developers implement their game. Framework conventions define how Jog discovers and manages code, while recommended conventions promote consistency and maintainability without unnecessarily restricting developers.

## Systems

**Systems are the heart of a Jog game.**

A System represents a feature or piece of game functionality. Examples include:

* `Players`
* `Inventory`
* `Combat`
* `Data`
* `Round`
* `Weapons`

Systems can depend on other Systems. Jog uses these dependencies to determine the order in which Systems are initialized and started.

```text
Inventory
    ↓
Players
```

In this example, `Players` will be initialized before `Inventory`, allowing `Inventory` to safely use it during its startup.

Systems can also contain multiple server or client modules. These modules belong to the same System and share the System's state, allowing large Systems to be separated into smaller, manageable pieces.

## Addons

**Addons extend Jog itself.**

While Systems contain the logic of your game, Addons provide reusable infrastructure and functionality that can be used across projects.

Examples include:

* Data saving
* Networking
* Analytics
* Commands
* Logging
* Debugging tools
* Developer tooling

Addons are loaded before Systems, allowing them to prepare or extend the framework before the game's Systems begin running.

Addons can also provide **bindings**, allowing them to hook into different parts of Jog's lifecycle and behavior.

This allows functionality that might traditionally be built directly into a framework to instead be implemented as an Addon.

## Packages

**Packages are standalone reusable modules.**

Unlike Systems and Addons, Packages are not managed by Jog's lifecycle. They can contain reusable Luau functionality such as:

* Libraries
* Utilities
* Data structures
* Signals
* Promises
* Other standalone modules

For example:

```text
Packages
├── SimpleSignal
├── Promise
├── Maid
└── Utility
```

A Package can be imported wherever it is needed without becoming part of the game's System architecture.

## Client and Server

Jog separates client and server functionality through conventions.

Systems can contain:

```text
MySystem
├── MySystemServer
└── MySystemClient
```

Server modules only run on the server, while client modules only run on the client.

This allows a System to contain all of the logic for a feature while keeping its execution environment clear.

Addons follow the same principle and can contain shared, server, and client modules.

## Lifecycle

Jog manages the lifecycle of Systems and Addons.

Systems generally follow:

```text
Initialize → Start → Stop
```

**Initialize** is used to prepare the System and create its state.

**Start** is used to begin runtime behavior, connect events, and interact with other Systems.

**Stop** is used to clean up resources and shut down the System.

Dependencies are resolved before the lifecycle begins, giving Systems a deterministic startup order.

## The Jog Ecosystem

Jog is designed to be more than just a framework. The **Jog Ecosystem** provides the tools, documentation, and resources surrounding the framework, making it easier to create, develop, extend, and share Jog projects.

```text
Jog Ecosystem
│
├── Jog Framework
│   └── Framework and runtime
│
├── Jog Plugin
│   └── Roblox Studio tooling
│
├── Jog Resource Manager
│   └── Resource installation and management
│
├── Jog Documentation
│   ├── Guides and references
│   └── Conventions
│
└── Jog Resources
    ├── Systems
    ├── Addons
    └── Packages
```

### Jog Framework

The **Jog Framework** is the core of the ecosystem. It provides the runtime, System architecture, Addon system, lifecycle management, dependency resolution, and other functionality required to run a Jog project.

### Jog Plugin

The **Jog Plugin** provides development tools for Roblox Studio. It assists with setting up Jog projects and provides features such as IntelliSense and other development tooling.

### Jog Resource Manager

The **Jog Resource Manager** is responsible for discovering, installing, updating, and managing resources for Jog projects.

Resources can contain Systems, Addons, Packages, or other files required by them.

### Jog Documentation

**Jog Documentation** contains the guides, references, concepts, and conventions for using and developing with Jog.

It covers both how Jog works and the recommended practices for building projects with it.

### Jog Resources

**Jog Resources** are distributable components of the Jog ecosystem.

Official resources can provide reusable Systems, Addons, and Packages maintained for Jog.

Resources may eventually be distributed through different sources, allowing developers to discover and install functionality into their projects through the Jog Resource Manager.

## Philosophy

Jog is built around a few simple ideas:

> **Systems contain game logic.**
> **Addons extend the framework.**
> **Packages provide reusable code.**
> **The runtime manages everything.**

Jog should handle the repetitive infrastructure while developers focus on building their game.

Jog provides an **opinionated architecture and set of conventions** to encourage consistency, while leaving developers free to implement their game logic however they choose within that architecture.
