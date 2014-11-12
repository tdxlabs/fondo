# Fondo

Fondo is a specification for distributed, immutable, derived, addressable
data. It defines a layer for addressing data, providing a foundation for
downstream functions such as data caching, transport, discovery, and
computation. (The word "fondo" is Esperanto for "foundation".)

## Benefits

Fondo makes working with data simpler and easier. Its benefits apply to tools,
systems, communities, and the Internet.

Data tools built on top of Fondo are simpler, due to its design choices and
constraints. Fondo frees data consumers from writing unnecessary code to handle
concerns of fixed locations, mutable data, and heterogenous distributed systems
with various guarantees of availability, consistency, and partition
tolerance. Such streamlining reduces the cost of ownership of data discovery and
computation tools.

Datasets hosted on Fondo systems are easier to discover and faster to
transfer. With derived data, data consumers can make smart trade-offs between
storage size and computation time based on network or device constraints.

Communities leveraging Fondo can focus on using data quickly and confidently
without worrying about implementation details about where the data
lives. Organizations do not have to impose a small set of database technologies
in order to achieve data interoperability.

If adopted broadly, Fondo could serve as a data foundation for the Internet, by
allowing diverse systems to share data across diverse networks
efficiently. Improving data availability and reducing transfer costs will remove
barriers and spur innovation in our data-hungry world.

> By far, HTTP is the most successful "distributed system of files" ever
> deployed. Coupled with the browser, HTTP has had enormous technical and social
> impact. It has become the de facto way to transmit files across the
> internet. Yet, it fails to take advantage of dozens of brilliant file
> distribution techniques invented in the last fifteen years. (From
> [IPFS - Content Addressed, Versioned, P2P File System][ipfs])

## Design Goals

Fondo has four design goals:

1. Provide data addressability across devices and networks
2. Ensure data immutability and integrity
3. Decouple an address from location
4. Decouple an address from the distributed system properties of the underlying
   storage

These four design goals can be explained with the six following concepts.

### Addressability

Fondo is an addressability specification for data connected via a network, even
if the connection is intermittent or unreliable. This includes a broad range of
devices, including servers, databases, desktop computers, mobile devices,
network hardware, sensors, and more.

### Immutability and Integrity

Fondo's design enforces immutable values. Each addressable piece of data is
assigned a unique identifier (UID), calculated by hashing the data contents,
including metadata. Once the UID is created, neither it nor the underlying data
can be altered due to the hashing. Immutability brings many benefits to
distributed and concurrent systems, including caching and provenance.

### Decouple Location

A Fondo address is a name, not a specification of location, similar to a Uniform
Resource Name (URN), a type of Uniform Resource Identifier (URI). A Fondo system
can match data consumers with data sources based on characteristics other than
location, such as latency, availability, and cost.

### Derived Data

Values in Fondo can be derived from other values. A derived dataset may append,
combine, or transform values. In order to allow derived data, Fondo imposes a
minimal set of types using the [Transit][transit] data interchange format. Fondo
efficiently supports derivative operations in two ways. First, storage demands
can be minimized using persistent data structures. Second, derivations are
represented using code. Derived data gives consumers flexibility to trade off
storage versus computation costs while preserving data integrity.

### Decoupling Underlying Storage Guarantees

Internally, Fondo allows different underlying storage mechanisms offering
various guarantees. It allows variations in latency, network connectivity, and
time-based availability. As an example of latency, data stored in
[Amazon Glacier][glacier] may not be available for four hours. Connectivity
varies based on network topology, so Fondo consumers may prefer to use
higher-bandwidth connections. Access and performance characteristics vary over
time; for example, mobile devices may only have intermittent
connectivity. Building a shared layer that handles these diverse systems reduces
overall system complexity, a marked improvement over requiring scattered code
for coordination. Externally, Fondo offers a different set of guarantees. Since
it is an immutable layer on top of heterogeneous, distributed data stores, it
can offer high availability, durability, and partition tolerance in
practice. However, Fondo does not strictly enforce availability or durability,
because doing so would demand too much centralized control. If data consumers
require stricter guarantees, they can cache datasets locally.

## Community

We welcome community involvement of all kinds, including suggestions,
criticisms, ideas, and encouragement. We have a starting vision for the
specification, including a focus on certain key problems that Fondo will
solve. We want to transform how people address data; to that end, we hope to
attract interest from a broad base of people and organizations. At the same
time, we have a bias for action; we don't plan on running the project by
committee. We intend to get a basic spec and reference implementation ready to
kick things off. Over time, we will see who naturally gets involved; active
participants will shape our direction and evolution.

## Fondo Repositories

You are currently reading the README for the Fondo specification.

Other repositories include:

* [fondo-riak][fondo-riak]: a Fondo implementation using [Riak][riak].
* [fondo-s3][fondo-riak]: a Fondo implementation using [AWS S3][s3].

## Related Work

* [Trusty URIs][trusty-uris] by Tobias Kuhn and Michel Dumontier. "To make
  digital resources on the web verifiable, immutable, and permanent, we propose
  a technique to include cryptographic hash values in URIs. We call them trusty
  URIs and we show how they can be used for approaches like nanopublications to
  make not only specific resources but their entire reference trees
  verifiable. Digital artifacts can be identified not only on the byte level but
  on more abstract levels such as RDF graphs, which means that resources keep
  their hash values even when presented in a different format."

* [IPFS - The Permanent Web][ipfs] by Juan Benet. "IPFS is a distributed file
  system that seeks to connect all computing devices with the same system of
  files. In some ways, this is similar to the original aims of the Web, but IPFS
  is actually more similar to a single BitTorrent swarm exchanging git
  objects. IPFS could become a new major subsystem of the Internet."

## License

We have not chosen a particular license yet, although we have goals in mind, as
follows. Loosely speaking, we want Fondo to be an open standard. According to
[Wikipedia][open-standard]:

> The terms "open" and "standard" have a wide range of meanings associated with
> their usage. There are a number of definitions of open standards which
> emphasize different aspects of openness, including the openness of the
> resulting specification, the openness of the drafting process, and the
> ownership of rights in the standard.

Next, we'll clarify what we mean.

The Fondo spec will be free to use, with attribution.

We (David James and Joshua Miller) will draft the initial specification. Our
intent is to prepare a draft fairly quickly, while working on a simple reference
implementation to test out the ideas.

We want the spec to reflect currently-available research, ideas, and
technology. So, we are happy to include interested people across many fields.

We have not formalized what our community discussion and drafting process might
look like, and we may not need to do so. We want to draw on many ideas while
still preserving a bias to action. Let us know if you would like to learn more
and get involved. We'll probably start with a simple mailing list.

We have not worked out exact details of the "ownership of rights" for the
spec. Our goal is to increase chances of adoption by keeping the spec
unencumbered and free to use. At the same time, we want to guard against
fragmentation, so we may reserve some limited rights as needed.

Perhaps at some point we may move governance to an established standards
organization. We are cognizant of potential pitfalls of formal working groups
such as gridlock, splintering, or design-by-committee. Time will tell.

If you have licensing suggestions or want to get involved, please get in touch.

[fondo-riak]: https://github.com/tdxlabs/fondo-riak

[glacier]: https://aws.amazon.com/glacier

[ipfs]: https://github.com/jbenet/ipfs

[open-standard]: http://en.wikipedia.org/wiki/Open_standard

[riak]: http://basho.com/riak

[s3]: https://aws.amazon.com/s3

[transit]: https://github.com/cognitect/transit-format

[trusty-uris]:
http://2014.eswc-conferences.org/sites/default/files/papers/paper_106.pdf
