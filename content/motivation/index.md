---
date: 2023-10-01T04:14:54-08:00
description: "Why do we need uProtocol?"
title: "Why do we need this?"
---
The automotive industry[^1] faces a number of challenges related to software communication:

* In-vehicle communication is largely inherited from legacy architectures that were mostly based on CAN networks. In addition to mechatronics software for which the existing infrastructure was developed, vehicles now include multiple powerful SoCs that run massive amounts of software. This software requires new communications mechanisms.
* Vehicles are now connected to the cloud and other devices like mobile phones. These communication links need to recover from loss of connection and provide secure data transmission, imposing additional requirements on the communications framework.
* Access to vehicle data from the cloud and sharing of this data in the cloud, drives yet other requirements such as scaling and reliability.
* Despite having varying requirements, all above requirements aim at transferring the same vehicle-related data, and end up being served by the same software components running that produce the data.
* Defining specific communication patterns for each and every _environment_ results into redundant work, unnecessary complexity and potential incompatibilities.

Eclipse uProtocol&trade; addresses these challenges by providing a small number of communication patterns, exposed via a consistent set of programming APIs which are available across the whole vehicle eco-system (in-vehicle ECUs, cloud and mobile). This approach enables seamless communication between applications and services, regardless of where they are deployed. Using uProtocol, application developers can focus on implementing differentiating functionality, rather than the low-level plumbing necessary to access relevant services they require. On the other hand, service providers can implement their service once for all consumers, wherever they are hosted.

Multiple communication mechanisms have been developed over the years, each solving specific problems: SOME/IP for in-vehicle inter-ECU communication, MQTT for IoT-to-Cloud communication, Linux IPC variants for intra-SoC communication, Binder for Android IPC etc. A connected vehicle system will require multiple of these systems, creating the challenge of bridging them together. Rather than trying to develop yet another, _more universal_ protocol, uProtocol's approach is to _map_ its APIs to existing frameworks, and ensure interoperability across them. This approach enables to use and combine multiple communication frameworks, while ensuring consistent end-to-end communication between software components.

An example topology covering in- and off-vehicle communication using multiple communication protocols is provided below:

{{< figure src="topology.drawio.svg" alt="Example Topology based on uProtocol" class="image-with-margin" >}}

[^1]: None of these challenges are specific to the automotive sector. Instead, other industries like defense, rail and aviation all face similar issues.
