#Custom application

JDemetra+ is designed as a modular application so that, if a feature is missing, it could be added later on.  

Still, there are some use cases where JDemetra+ is not adapted.  
You migth also need to integrate JDemetra+ features into an existing application.

Depending on your needs and constraints, you can use one of the following options.

##Inside Java ecosystem

The simpliest way to use JDemetra+ is to stay inside the **Java ecosystem**.  
By doing so, you will benefit from the platform tools and the homogeneity of the language.

###1. Extend/Modify JDemetra+

JDemetra+ is a modular application whose behaviors and capabilities can be extended or modified by plugins.

###2. Create from scratch

If JDemetra+ doesn't meet your requirements, it is still possible to create a new application from scratch by using the [jdemetra-core](https://github.com/jdemetra/jdemetra-core) libraries.

##Outside Java ecosystem

JDemetra+ engine can be used in **other languages and platforms**.  
To do so, you need to choose one of the following interoperability strategies.

###1. Language interoperability

####1.1 Source code conversion

The code source of JDemetra+ is freely available. So, it is possible to convert it into another language using an automatic tool or by hand.  
While beeing technicaly feasible, it represents a lot of work and therefore is not promoted.

- Pros:
	- _might_ lead to best performances
	- follows target language paradigms  
- Cons: 
	- represents huge work
	- is difficult to keep in sync with the original code

####1.2 Byte code convertion

The compilation of the Java code produces an [intermediate byte code](https://en.wikipedia.org/wiki/Java_bytecode) which is executed by a [virtual machine](https://en.wikipedia.org/wiki/Java_virtual_machine).  
This specific byte code can be automaticaly translated into other byte codes (like .NET using [IKVM](https://en.wikipedia.org/wiki/IKVM.NET)) or directly into native code.

- Pros: 
	- is easy to use
	- is automatic  
- Cons: 
	- is slightly less performant
	- adds some memory overhead
	- mixes different language paradigms

###2. Inter-process communication (IPC)

[Inter-process communication (IPC)](https://en.wikipedia.org/wiki/Inter-process_communication) is a set of techniques for the **exchange of data among multiple threads in one or more processes**.
Processes may be running on one or more computers connected by a network.

If those processes are executed on to same computer, they are said to be executed locally, otherwise remotely.

The use of **remote processes** brings more flexibility. It is indeed possible to upgrade the processes separately.
They can even be implemented in different languages/platforms. Unfortunatly, remoting comes with some issues such as additional latency, network failures and several overheads.
It might also pose a threat to confidential data.

####2.1 Command-line interface

Most languages/platforms are able to execute a command on the operating system shell. 
Therefore, it is possible to call the JDemetra+ engine through a [command-line](https://github.com/nbbrd/jdemetra-cli) and parse its result back to the caller.

- Pros:
	- is easy to use
	- works with almost all languages/platforms
	- does not pose a threat to confidential data
- Cons:
	- is subject to performance penalties due to process initialisation and result parsing
	- is less flexible since the commands must be available somewhere in the OS

####2.2 Web service

[Web services](https://en.wikipedia.org/wiki/Web_service) (and more specificaly [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)) are currently the most versatile way to create an IPC.
It is available in almost all languages/platforms. It is a mature technology.
It is performant enough to fulfil most use cases.
The security aspect is already taken care by several libraries and [protocols](https://en.wikipedia.org/wiki/HTTPS). 

- Pros:
	- is easy to use
	- works with almost all languages/platforms
	- is flexible
- Cons:
	- is subject to performance penalties due to serialization and network issues
	- might pose a threat to confidential data
	
_Note that it is possible to run a web service locally. This removes the network issues and the confidentiality threats but also reduces flexibility._
	
####2.3 Remote procedure call (RPC)

This represents several technologies. Some are old and mature like [Corba](https://en.wikipedia.org/wiki/CORBA) and [RMI](https://en.wikipedia.org/wiki/Java_Remote_Method_Invocation). Some are new and promising like [gRPC](http://www.grpc.io/).  
In the Microsoft .NET ecosystem, [Remoting](https://en.wikipedia.org/wiki/.NET_Remoting) offers RPC facilities on the Windows platform. It has been superseded by [WCF](https://en.wikipedia.org/wiki/Windows_Communication_Foundation).

Each solution differ from integration with several languages and from availability of tools. 
For example, WCF is easy to code and maintain but is also limited to the .NET ecosystem.
On the other hand, other solutions might be more interoperable but might also require more plumbing. 

_Note that web services are often considered as a specific RPC._ 

####2.4 Local IPC

This represents several technologies that are often specific to an operating system such as Microsoft's [COM](https://en.wikipedia.org/wiki/Component_Object_Model) and Linux [D-Bus](https://en.wikipedia.org/wiki/D-Bus).  

_Note that these technologies are often also usable for remoting_.
