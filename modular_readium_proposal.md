# Proposal for a modular Readium-web

## This document

The purpose of this document is to propose a modular architecture for the Readium-web project, and to obtain 2 to 3 months of funding for implementation. 

## Context

### The Readium-web project
The objective of the Readium-web project was to demonstrate the EPUB 3.0 standard by deploying an open-source reader. This objective has been accomplished. A very large part of EPUB 3.0 functionality has been implemented and a version has been deployed on the Chrome store. This version currently has over 30,000 users. 

### Readium-web architecture
From a software engineering perspective, the Readium project was characterized by short iterations to quickly implement new features. At the time, little emphasis was placed on building a modular architecture that could provide a foundation for EPUB 3.0 support in other projects or to ensure the code base was accessible to interested developers.

## The state of the Readium-web project

### A desire for EPUB support
Evident Point often receives inquiries about using Readium-web as a foundation for projects incorporating EPUB 3.0 support. Developers want modular, configurable, EPUB 3 components they can deploy in their applications. Demands include library features with persistence, rendering specific, static EPUBs in a web application or simply using infrastructure components as the basis for a customized front-end. Regardless, there appears a healthy demand for EPUB software components.

### Using Readium-web as a foundation for EPUB 3.0 projects will make it _hard_ to support EPUB 3.0 on the web
I'm preaching to the choir when I say that good, accessible tool support, modular-code, and documentation are important for furthering a technology standard. The fact is, these are lacking for the Readium-web project. 

To be as direct as possible, if I were running a startup that included EPUB support in any significant way, modularizing the code base would be my first objective. Readium, in its current form, is monolithic. It cannot be easily understood, it is not documented, it has redundant code, it has some "deep" and complex bugs that are a function of its design, and it is not easy to extend. If you're familiar with the Peter Principle, it almost certainly applies to Readium. 

Anyone who builds a project on top of Readium-web without significant work will suffer from these issues for the lifetime of their application.

## The advantage of acting now

### It's cheaper
The benefit of moving on this now is essentially that I have six months of experience working with Readium. I understand the code-base, have experience with the spec, the community, and the technologies we're using. While I won't claim that you couldn't find another developer to modularize Readium in the future, I think the cost will far exceed what it will right now. This is a good time to leverage my experience with the project.

### I want this to succeed
Additionally, I now feel personally invested in the Readium project. I value the opportunity to work on an open standard, and an open-source project. I want EPUB to succeed, and I think Readium-web - as a set of stable, well-documented modules - would go a long way to advancing the standard. I would contend that a developer who cares about their project is not something to be undervalued.  

## The proposal

My proposal is to split the current Readium-web project into a set of independent modules. The current Readium library and viewer will consist of these modules and act as a demonstration of how to build a reader from the modules. Each module will be documented, with a test-suite, and documentation will be provided on the architecture of the entire project.

### Requirements

__Suggested requirements__
* Create a set of well-engineered modules that can be included in a web application to provide EPUB 3.0 support
* Support deployment of modules on the client or server, at the discretion of the user. 
* Provide documentation for the project and modules
* Provide development tools, such as a test-suite for each module
* Demonstrate the use of the modules by deploying them as part of Readium-web


__Discretionary requirements__
* Create packages to deploy a subset of EPUB functionality into popular frameworks: Rails, Django, NodeJS etc.
* Support mobile

### Readium-web module structure

I propose the following module structure (the module names are still in flux):

* epub_extraction : This module is responsible for extracting and parsing an epub. It can be used to a produce a JSON representation of the EPUB package document and associated packaging data. Deployable on either client or server.
* epub : A module that can consume a JSON representation of packaging information and provide an API for computing and obtaining information about the epub.
* epub_reader : This module is responsible for managing a set of reflowable/scrolling/fixed views, or a combination of them. It provides an API to allow for pre-rendering and pre-fetching of epub resources. This will provide much more flexibility in how and when epub content documents are loaded. By providing the ability to load resources into memory, the possibility also exists to allow for client-side search, metrics for the epub, etc. 
* epub_rendering_utilities : This module exposes an API that provides support to implement parts of the EPUB specification. This module exists more in support of other modules, but can be called directly, if required. 
* epub_fixed : A module that implements an embedded viewer for a section of (or complete), fixed layout EPUB.
* epub_reflowable : A module that implements an embedded viewer for a reflowable content document.
* epub_scrolling : A module that implements an embedded viewer for a scrolling content document.

### Work already completed

I've created a readium-refactored branch on Github, where I've done a preliminary re-organization of Readium's code into folders that represent the modules described above. I've also completed a significant refactoring of the Reflowable view code into an epub_reflowable module. Refactoring the reflowable view and its associated pagination code was likely the most difficult part of the refactoring and is now complete. 

### Proposed schedule

I propose the following schedule for modularizing Readium-web:

* 5 days for the epub_reader module
* 5 days for the epub_scrolling and epub_fixed_layout modules 
* 10 days for the epub and epub_extraction modules
* 5 days for the epub_rendering_utilities module
* 3 days for organization of the project directory
* 5 days for documentation
* 2 days for project deployment 
* 5 days cushion