---
title: Core Concepts
---

Abstract Syntax Tree
-----------------

The way analysed source code is represented in the static analyser so that it can be queried for useful information. [Learn more »](abstract-syntax-tree.md)

Scope
-----------------

The Scope object can be used to get more information about the code, like types of variables, or current file and namespace. [Learn more »](scope.md)

Type System
-----------------

PHPStan's type system is a collection of classes implementing the common `PHPStan\Type\Type` interface to inform the analyser about relationships between types, and their behaviour. [Learn more »](type-system.md)

Trinary Logic
-----------------

Many methods in PHPStan do not return a two-state boolean, but a three-state `PHPStan\TrinaryLogic` object. [Learn more »](trinary-logic.md)

Reflection
-----------------

PHPStan has its own reflection layer for asking about functions, classes, properties, methods, and constants. [Learn more »](reflection.md)

Dependency Injection & Configuration
-----------------

Dependency injection controls the way how extension objects are constructed for usage by PHPStan. [Learn more »](dependency-injection-configuration.md)
