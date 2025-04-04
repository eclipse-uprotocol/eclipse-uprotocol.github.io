+++
title = 'uProtocol Explainer'
date = 2025-03-28T13:40:45+01:00
+++

Communication has two important dimensions, no matter whether it involves living beings or technical systems: the message and the medium. Or, in very loose analogy, semantics and syntax.

Message/semantics concerns what is being communicated: two persons agreeing on the same words and concepts will be able to have a conversation no matter whether they use voice, text, sign language, morse code, etc. This is the content.

Medium/semantics is about how to transfer desired information: any series of symbols ('messages') can be transmitted between communicating parties, as long as they agree on the mechanism to use and are able to work with it. This is the plumbing [^1].

In the context of technical systems, the scope of alignment on message/semantics usually determines the scalability of an asset: as long as message contents are well defined, the number of communicating parties can grow and even accommodate changes in plumbing over time. Components of such a system become exchangeable and can evolve independently. That way, stability in business logic is achievable and addressable market of domain-specific offerings is grown (aka "ecosystem").

In software systems, the specific plumbing is both highly critical and surprisingly malleable: if it isn't working nothing will flow, there is a lot of it, and things continuously change and evolve. Much of the time in software product development is spent in adapting and integrating different plumbing, and it feels like new middleware is popping up left and right, almost at every opportunity [^2].

While the rest of this article will dive into the plumbing aspect, it is worth pointing out the existing open community effort for standardizing on content: the COVESA Vehicle Signal Specification (VSS) and vehicle service definition (uService) projects. In combination with the work going on in the Eclipse Foundation SDV working group, these groups are making a bona fide attempt to establish a jointly developed, community driven offering in this space.

## The SDV situation

This is also true in the context of vehicle systems and Software-Defined Vehicle (SDV) architectures, albeit with a couple of extra wrinkles. An SDV-style system comprises communication between very disparate parties: on one end is the mechatronics domain with microcontrollers deeply embedded in vehicles, ensuring that when you brake, the car brakes. On the other end there are user-facing cloud services and mobile applications that are used to remote-control vehicle functions, manage driver profiles, and much more.

These two ends of the technological spectrum bring with them an equally wide spread of requirements on the plumbing that is used, and stem from extremely diverse areas of engineering mindset. A real-time, minimal-latency in-vehicle CAN communication line is very different from a cloud-to-app protocol stack, and there exists a range of shades of grey in between these two - each associated with a certain development culture and associated implications on surrounding organization.

In short: the plumbing in the context of SDVs is complicated, on more than just the technological level.

All of the involved technology areas have evolved and built their own set of solutions to meet their requirements. There exists a range of in-vehicle physical and transport protocol options, the IoT domain brings its share of messaging and communication infrastructure, the cloud has evolved a host of options over the last 10-20 years [^3]. Yet modern vehicles and their supporting IT systems are expected to somehow make useful sense out of this and build sustained customer value on top of it all [^4].

One common reaction to a new context of requirements and changing technology players is to invent “a new thing” that solves this new challenge, perhaps even in the form of a standard that is painstakingly collecting and addressing all of the potentially relevant needs of all participants [^5]. There are scenarios where this is a valid approach. However, considering this is growing the solution landscape, it does not solve the core issue but rather aggravates it: there are a huge number of technology options that have to play together to build something of value to customers.

## Eclipse uProtocol&trade; vision

The Eclipse Foundation SDV working group has made it it's mission to contribute relevant pieces to the SDV ecosystem, and as such the concerns raised so far are at the heart of the working group. While the working group portfolio is accruing its share of excellent middleware solutions from to eCal to Zenoh, one recent project is setting out to offer an integrative approach that enables systematic and ecosystem-scale combination of specific plumbing into larger-scale solutions. This project is called Eclipse uProtocol&trade;, and has gained substantial contribution activity since it has been initially published by GM in the second half of 2023. The uProtocol&trade; approach aims to do two things differently:

It is not another middleware implementation; rather, it offers concepts and abstractions that can facilitate collaboration in existing, complex organizations (that span the whole technology spectrum, as lined out above). uProtocol&trade; is the glue that can bind together communication domains from mechatronics to cloud, by providing a common approach for bridging between a range of middleware options typically used within those domains. It works to provide ready-made integration components that allow for quick link-up of commonly used transport protocol implementations. It also defines a set of higher-level applications which provide cross-domain integration for common concerns like service discovery, data subscription and digital twin functionality [^6].

To make the uProtocol&trade; value proposition more graspable, let's consider a straightforward feature that is expected of premium vehicles today, which involves at least three very different technology domains: the smartphone vehicle companion app. Looking at contemporary examples, such apps provide a mix of near-live vehicle data display (like geo-location or current driving speed) and remote command execution (like climate control, opening trunk/doors, or managing the charging process).

Both of these functionalities require data and commands to flow from embedded domains in vehicles, via in-vehicle high-compute devices, vehicle infotainment/connectivity systems, cloud service backends, to the smartphone app, and vice versa. Each of these steps likely involves at least one distinct transport protocol, plus a number of data management, processing and storage entities. Each of these comes with their own APIs and programming model, all of which are constantly evolving.

Contrast this to the need of developers of business ("domain") applications: they have to interact with services at the far end of this chain that likely live in a technological context far removed from their own. The product lifecycle, operations organization and engineering processes of this far-away endpoint are very different compared to their own. More often than not, even the meaning of terms and concepts as used by these groups will differ sufficiently to create roadblocks (compare the message/semantics theme that this article started out with).

This is the space that uProtocol&trade; aims to address by providing a unified way to define, locate and address services and data sources all across this landscape. uProtocol&trade; adapters and gateways introduce a global addressing mechanism for services, a common source of truth for API endpoints, and the glue components necessary to enable data and command flow across domain boundaries. While uProtocol&trade; picks up and involves implementations of established concepts like pub/sub network subscription management or digital-twin-style data caches, it is designed to decouple business API definitions from the specific technology used in any one specific domain, as well as be integrative of whichever protocols are used in a specific solution scenario.

The upshot of all this is that uProtocol&trade; enables developers to interact with data sources and API endpoint the same way, no matter where on the technology map they operate. Within a uProtocol&trade; service mesh, invocation and data access works identically from one in-vehicle service to another, from vehicle to cloud, from cloud to vehicle, from app to vehicle, and so on. These shared concepts and API definitions (aka 'programming model') can provide a common ground for alignment between developer teams from diverse areas. uProtocol&trade; aims to help bridge technology and organizational boundaries.

## uProtocol&trade; project status

The uProtocol&trade; project has attracted one of the fastest-growing developer communities in the Eclipse SDV working group. Within a few months, a comparably diverse set of contributions have started to flow in, already beginning to visibly shape and extend the foundations of a potential uProtocol&trade;-enabled ecosystem. uProtocol&trade; is already illustrating its potential to be an integration force and a rallying point for a lot of open-source SDV components.

Notably, the core specification and API definitions are being evolved and improved, a number of new programming language libraries (SDKs) are being built (currently uProtocol&trade; support exists for Java, C++, Rust, Python and Kotlin), and the first wave of protocol adapters is being worked on, linking up Android Binder, Eclipse Zenoh and MQTT brokers. In 2024 we saw the uProtocol&trade; service fabric introduced to one or more of the Eclipse SDV Blueprint projects as a publicly visible proof point and showcase. This has been made very obvious at the 2025 Q1 Eclipse SDV Community Event, where more than half the presentations involved some form of integration or connection with uProtocol&trade;.

To help further this goal, more uProtocol&trade; adapters and bridges to specific automotive technologies are required. For an open-source community this quickly becomes a challenge as traditional automotive protocol stacks are usually proprietary and/or protected by some form of prohibitive IP regulations. For example, the uProtocol&trade; vision would massively benefit from a close integration with AUTOSAR® communication infrastructure like SOME/IP, which represents a relevant part of the service-oriented communication community in the embedded automotive world. The IP policies attached to these specifications make publication of open-source implementations a challenging and time-consuming endeavour. There is a little light at the end of this tunnel, with the AUTOSAR® consortium working on Rust bindings for the AUTOSAR Adaptive stack, which might gift us with a set of interface specifications that are published under a true Open Source license, finally enabling system interconnects to be made in the Open Source technology space.

[^1]: Of course these two dimensions do influence each other: restrictions of the medium will inform how messages are phrased and used, while requirements of the messages will determine which medium is going to be useful.

[^2]: Software engineers really embrace McLuhan's view that The Medium is the Message, which is suggesting that "[...] a communication medium itself, not the messages it carries, should be the primary focus of study."

[^3]: Even though we might not have called it 'the cloud' back then.

[^4]: 'Sustained' being the operative word here. One can aim to build the product that is perfect for one short moment in time - but that feat has to be replicated for 10 other product lines in parallel, and then repeated for all of these 2 years down the line with when the next generation product is due. And then all of this variety has to be maintained for 10+ years of operation, with potentially many millions of units sold...

[^5]: This is why we have so many standards

[^6]: With this scope it should be clear that uProtocol&trade; is not trying to be the answer to every specialist use case along the way - certain things (e.g. realtime critical communication within one subdomain of a vehicle) are better solved with existing, specialized and localized approaches.

&nbsp;
