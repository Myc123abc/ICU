# ICU Design

## Locales

Locales IDs are composed of language, country, and variant information.

## Data-driven Services

Data-driven services often use resource bundles for locale data. These services map a key to data. The resources are designed not only to manage system locale information but also to manage application-specific or general services data. ICU supports string, numeric, and binary data types and can be structured into nested arrays and tables.

This results in the following:
- Data used by the services can be built at compile time or runtime.
- For efficient loading, system data is pre-compiled to .dll files or files that can be mapped into memory.
- Data for services can be added and modified without source code changes.

## Threading Model and Open and Close Model

When you use a service such as collaction, the client opens the service using an ID, typically a locale. This service allocates a small chunk of memory used for the state of the service, with pointers to shared, read-only data in support of that service. In C++ call `createInstance()`. ICU uses the open and close metaphor in C because it is more familiar to C programmers.

### Thread-Safe const APIs

Service objects can be thread-safe as long as of the threads are using only const APIs. For non-const use, you must use the clone function to create a copy of the service you want and then pass this copy to the second thread.

### Freezable

An object that typically starts out mutable can be set up and then "frozen", which make it immutable and thus usable concurrently because all non-const APIs are disabled. A frozen object can never be "Thawed".

### Clone & Open

Clone oeprations are designed to be much faster than reopening the service with initial parameters and copying the source's state.

## Cloning Customization

For some services, ICU supplies registraction. You can register a customized open service under an ID; keeping a copy of that service even after you close the orignal. A client in that thread or in other threads can recreate a copy of the service by opening with that ID.

ICU may cache service instances. Therefore, registraction should be done during startup, before opening services by locale ID.

While you still might have multiple copies of data tables, it is faster to create a service from a registered ID than it is to create a service from rules.

These registrations are not persistent; once your program finishes ICU flushes all the registractions. To work around the lack of persistent registration, query the service for the parameters used to create it and then store those parameters in a file on a disk.

### Per-Client Locale ID & Per-Thread Locale ID

Setting a per thread locale ID, and then not passing the locale ID as a parameter during processing. It might result in ICU being requested to constantly open, use, and then close service objects. Instead, it is recommended that locale IDs be associated with each client be stored with other per-client data, along with any service objects that client might use. If operations involving a single client are short-lived, it might be more efficient to keep a pool of service objects, organized according to locale.

## Memory Usage

ICU4C APIs are designed to allow separate heaps for its libraries vs. the application. This is archieved by providing funcitons to allocate and release objects owned by ICU4C using only ICU4C library functions.

## Initialization and Termination
