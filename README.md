# ClusterVMS

ClusterVMS is a distributed, modular, scalable, composable, and flexible Video Management System (a.k.a. NVR or CCTV system).

There are many open source NVR/CCTV/VMS solutions, because every installation has different demands. The main goal of ClusterVMS is to provide a flexible framework that can meet ANY use case, so instead of creating a whole new system, developers can just make a new ClusterVMS component, and users can put together an installation with Alice's awesome UI, Bob's high-tech motion detector, and Charlie's toenail recognition system.

As of April 2025, ClusterVMS is still very early in development, and lacks critical features like recording, and a lot of polish. However, it can at show live camera streams with very low latency and little load on the server, and additional features are in the works.


## Philosophy

ClusterVMS embraces the Unix philosophy, often summarized as "do one thing and do it well", and combines it with modern cloud computing ideas.

* Each component should do one task.
* Infrastructure should be abstracted to reduce dependencies.
* APIs should be simple and easy to use.
* Cybersecurity *must* be taken seriously. (Warning: while we are designing with security in mind, we are prioritizing getting the system working, so many security features are lacking)
* Power comes not from individual programs, but from the relationships between them.
* Put the user in charge, and make it easy for them to customize the system.
* Keep It Simple, Stupid: A simple system is easier to understand and to modify.
	* A flexible design is a simple design which doesn't stand in the way, not a complicated design that has to change for every new feature.
	* General example: Rather than unique interfaces for interacting with hardware, querying processes, et cetera, Unix treats most things as files, so a program that can read a traditional file can also read from a hardware device, query system status, et cetera.
	* ClusterVMS example: rather than enumerating all supported storage methods and providing various structs holding the details for each, ClusterVMS treats storage locations as URLs. To add a new storage method (e.g. git lfs), ONLY the components that need to store or retrieve that data need to understand the URL.


## What Sets ClusterVMS Apart
* Multiple distributions to support different use cases
* Distributed and horizontally scalable architecture so you don't need one big server that handles all the cameras.
* Every component is swappable. You're not stuck with one UI, or detection algorithms that don't fit your use case, or even a camera manager that can't handle 10,000,000 cameras or run on [your soldering iron](https://pine64.com/product/pinecil-smart-mini-portable-soldering-iron/).
* Transcoding is avoided unless necessary (e.g. if you opt to resize the video or insert timestamps) to greatly reduce latency and server-side resource consumption.
* (TODO) Supports multi-site installations, so a single pane of glass can show information from sites spread across the world (and recordings can be distributed across the sites in case someone tries to tamper/destroy evidence)


## Goals
* Put the power in the hands of the user.
* Flexibility to support any use case.
* Ease of development for new developers to create custom components without having to know the ins and outs of the entire system. This will (hopefully) lead to an extensive ecosystem of components to choose from.
* Scalability to support massive multi-site installations, or tiny single-camera setups on resource-constrained hardware.
* Make it easy for technical and non-technical end users to configure the system to fit their needs.
* Security (unlike many cameras themselves...)


## Expected Use Cases
* Businesses: it takes a lot of cameras to properly cover a commercial location vs a house, so a scalable solution like ClusterVMS is a must
* OEMs and system integrators: ClusterVMS's modularity and extensibility makes it a good starting point for a customized VMS which can be integrated into an NVR. Custom features can be added while keeping an open source core, reducing overall development effort.
* Custom solutions: Some use cases have special requirements that aren't met by any existing software. ClusterVMS can provide core components and an overall framework for special use scenarios that would otherwise require writing a system from scratch.
* Home labs/tinkering: Flexible configuration allows ClusterVMS to run on whatever hardware you have, and integrate with your existing storage/monitoring/management infrastructure.
* Anything else: ClusterVMS aims to fit virtually any use case, so if it DOESN'T fit your use case, tell us, and we'll see if we can make it fit.


## Standard Architecture

At its core, ClusterVMS itself is just an API, so the system architecture may vary greatly between systems. While the standard architecture is built around containers and micro-services, it's perfectly valid to set up a ClusterVMS system that runs on bare metal, or VMs, or FPGAs, or other infrastructure. Components could also be combined, e.g. a component could serve as both a motion detector and a re-streamer if necessary for performance or other reasons.

A typical ClusterVMS installation has two types of components:
* Low-level components, like video stream forwarders, detection algorithms, and recorders, which receive simple instructions and typically operate on a single stream or camera.
* Higher-level "managers" which control the low-level components and provide an integrated API for viewing and controlling the system.


## License

Each component of ClusterVMS is licensed independently, and third-party components may even be proprietary. Currently, most components are dual-licensed under MIT and Apache licenses, but we may eventually move some components to the GPL.

We are committed to FOSS. While it's possible we *may* eventually create a paid/proprietary component, we'd like to avoid it, and in any case, it would be an optional add-on, or a long-term-support version, or something of that nature, which does not interfere with our free/open source mission.

