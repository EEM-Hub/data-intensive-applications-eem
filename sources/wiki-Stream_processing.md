---
source: https://en.wikipedia.org/wiki/Stream_processing
fetched: 2026-06-19
---

Computer programming paradigm 

In [computer science](./Computer_science), **stream processing** (also known as **event stream processing**, **data stream processing**, or **distributed stream processing**) is a [programming paradigm](./Programming_paradigm) which views [streams](./Stream_(computing)), or sequences of events in time, as the central input and output objects of [computation](./Computation). Stream processing encompasses [dataflow programming](./Dataflow_programming), [reactive programming](./Reactive_programming), and [distributed](./Distributed_computing) [data processing](./Data_processing).[[1]](./Stream_processing#cite_note-1) Stream processing systems use [streaming algorithms](./Streaming_algorithm) to trace [parallel processing](./Parallel_computing) for data streams. The [software stack](./Solution_stack) for these systems includes components such as [programming models](./Programming_model) and [query languages](./Query_language), for expressing computation; [stream management systems](./Data_stream_management_system), for distribution and [scheduling](./Scheduling_(computing)); and hardware components for [acceleration](./Hardware_acceleration) including [floating-point units](./Floating-point_unit), [graphics processing units](./Graphics_processing_unit), and [field-programmable gate arrays](./Field-programmable_gate_array).[[2]](./Stream_processing#cite_note-2)

 

The stream processing paradigm simplifies parallel software and hardware by restricting the parallel computation that can be performed. Given a sequence of data (a *stream*), a series of operations (*[kernel functions](./Compute_kernel)*) is applied to each element in the stream. Kernel functions are usually [pipelined](./Pipeline_(computing)), and optimal local on-chip memory reuse is attempted, in order to minimize the loss in bandwidth, associated with external memory interaction. *Uniform streaming*, where one kernel function is applied to all elements in the stream, is typical. Since the kernel and stream abstractions expose data dependencies, compiler tools can fully automate and optimize on-chip management tasks. Stream processing hardware can use [scoreboarding](./Scoreboarding), for example, to initiate a [direct memory access](./Direct_memory_access) (DMA) when dependencies become known. The elimination of manual DMA management reduces software complexity, and an associated elimination for hardware cached I/O, reduces the data area expanse that has to be involved with service by specialized computational units such as [arithmetic logic units](./Arithmetic_logic_unit).

 

During the 1980s stream processing was explored within [dataflow programming](./Dataflow_programming). An example is the language [SISAL](./SISAL) (Streams and Iteration in a Single Assignment Language).

 

## Applications

 

Stream processing is essentially a compromise, driven by a data-centric model that works very well for traditional DSP or GPU-type applications (such as image, video and [digital signal processing](./Digital_signal_processing)) but less so for general purpose processing with more randomized data access (such as databases). By sacrificing some flexibility in the model, the implications allow easier, faster and more efficient execution. Depending on the context, [processor](./Central_processing_unit) design may be tuned for maximum efficiency or a trade-off for flexibility.

 

Stream processing is especially suitable for applications that exhibit three application characteristics:[*[citation needed](./Wikipedia:Citation_needed)*]

 
- **Compute intensity**, the number of arithmetic operations per I/O or global memory reference. In many signal processing applications today it is well over 50:1 and increasing with algorithmic complexity.
- **Data parallelism** exists in a kernel if the same function is applied to all records of an input stream and a number of records can be processed simultaneously without waiting for results from previous records.
- **Data locality** is a specific type of temporal locality common in signal and media processing applications where data is produced once, read once or twice later in the application, and never read again. Intermediate streams passed between kernels as well as intermediate data within kernel functions can capture this locality directly using the stream processing programming model.

 

Examples of records within streams include:

 
- In graphics, each record might be the vertex, normal, and color information for a triangle;
- In image processing, each record might be a single pixel from an image;
- In a video encoder, each record may be 256 pixels forming a macroblock of data; or
- In wireless signal processing, each record could be a sequence of samples received from an antenna.

 

For each record we can only read from the input, perform operations on it, and write to the output. It is permissible to have multiple inputs and multiple outputs, but never a piece of memory that is both readable and writable. 

 We could discuss weeks on whatever this can be considered generally true by pointing out the implications of the exact wording.  

## Code examples

 

By way of illustration, the following code fragments demonstrate detection of patterns within event streams. The first is an example of processing a data stream using a continuous [SQL](./SQL) query (a query that executes forever processing arriving data based on timestamps and window duration). This code fragment illustrates a JOIN of two data streams, one for stock orders, and one for the resulting stock trades. The query outputs a stream of all Orders matched by a Trade within one second of the Order being placed. The output stream is sorted by timestamp, in this case, the timestamp from the Orders stream.

 
```
SELECT DataStream
   Orders.TimeStamp, Orders.orderId, Orders.ticker,
   Orders.amount, Trade.amount
FROM Orders
JOIN Trades OVER (RANGE INTERVAL '1' SECOND FOLLOWING)
ON Orders.orderId = Trades.orderId;

```
 

Another sample code fragment detects weddings among a flow of external "events" such as church bells ringing, the appearance of a man in a tuxedo or morning suit, a woman in a flowing white gown and rice flying through the air. A "complex" or "composite" event is what one infers from the individual simple events: a wedding is happening.

 
```
WHEN Person.Gender EQUALS "man" AND Person.Clothes EQUALS "tuxedo"
FOLLOWED-BY
  Person.Clothes EQUALS "gown" AND
  (Church_Bell OR Rice_Flying)
WITHIN 2 hours
ACTION Wedding

```
 

## Comparison to prior parallel paradigms

 

Basic computers started from a sequential execution paradigm. Traditional [CPUs](./Central_processing_unit) are [SISD](./Single_instruction,_single_data) based, which means they conceptually perform only one operation at a time.
As the computing needs of the world evolved, the amount of data to be managed increased very quickly. It was obvious that the sequential programming model could not cope with the increased need for processing power. Various efforts have been spent on finding alternative ways to perform massive amounts of computations but the only solution was to exploit some level of parallel execution. The result of those efforts was [SIMD](./Single_instruction,_multiple_data), a programming paradigm which allowed applying one instruction to multiple instances of (different) data. Most of the time, SIMD was being used in a [SWAR](./SWAR) environment. By using more complicated structures, one could also have [MIMD](./Multiple_instruction,_multiple_data) parallelism.

 

Although those two paradigms were efficient, real-world implementations were plagued with limitations from memory alignment problems to synchronization issues and limited parallelism. Only few SIMD processors survived as stand-alone components; most were embedded in standard CPUs.

 

Consider a simple program adding up two arrays containing 100 4-component [vectors](./Vector_(geometric)) (i.e. 400 numbers in total).

 

### Conventional, sequential paradigm

 
```
for (int i = 0; i < 400; i++) {
    result[i] = source0[i] + source1[i];
}

```
 

This is the sequential paradigm that is most familiar. Variations do exist (such as inner loops, structures and such), but they ultimately boil down to that construct.

 

### Parallel SIMD paradigm, packed registers (SWAR)

 See also: [Vector_processor § Vector_reduction_example](./Vector_processor#Vector_reduction_example) 
```
// for each vector
for (int elem = 0; elem < 100; elem++) {
    vectorSum(result[elem], source0[elem], source1[elem]);
}

```
 

This is actually oversimplified. It assumes the instruction `vector_sum` works. Although this is what happens with [instruction intrinsics](./Intrinsic_function), much information is actually not taken into account here such as the number of vector components and their data format. This is done for clarity.

 

You can see however, this method reduces the number of decoded instructions from *numElements * componentsPerElement* to *numElements*. The number of jump instructions is also decreased, as the loop is run fewer times. These gains result from the parallel execution of the four mathematical operations.

 

What happened however is that the packed SIMD register holds a certain amount of data so it's not possible to get more parallelism. The speed up is somewhat limited by the assumption we made of performing four parallel operations (please note this is common for both [AltiVec](./AltiVec) and [SSE](./Streaming_SIMD_Extensions)).

 

### Parallel stream paradigm (SIMD/MIMD)

 
```
// This is a fictional language for demonstration purposes.
elements = array streamElement([number, number])[100]
kernel = instance streamKernel("@arg0[@iter]")
result = kernel.invoke(elements)

```
 

In this paradigm, the whole dataset is defined, rather than each component block being defined separately. Describing the set of data is assumed to be in the first two rows. After that, the result is inferred from the sources and kernel. For simplicity, there's a 1:1 mapping between input and output data but this does not need to be. Applied kernels can also be much more complex.

 

An implementation of this paradigm can "unroll" a loop internally. This allows throughput to scale with chip complexity, easily utilizing hundreds of ALUs.[[3]](./Stream_processing#cite_note-3)[[4]](./Stream_processing#cite_note-4) The elimination of complex data patterns makes much of this extra power available.

 

While stream processing is a branch of SIMD/MIMD processing, they must not be confused. Although SIMD implementations can often work in a "streaming" manner, their performance is not comparable: the model envisions a very different usage pattern which allows far greater performance by itself.

 

It has been noted that when applied on generic processors such as standard CPU, only a 1.5x speedup can be reached.[[5]](./Stream_processing#cite_note-5) By contrast, ad-hoc stream processors easily reach over 10x performance, mainly attributed to the more efficient memory access and higher levels of parallel processing.[[6]](./Stream_processing#cite_note-6)

 

Although there are various degrees of flexibility allowed by the model, stream processors usually impose some limitations on the kernel or stream size. For example, consumer hardware often lacks the ability to perform high-precision math, lacks complex indirection chains or presents lower limits on the number of instructions which can be executed.

 

## Research

 
|  | This sectionfocuses too much on specific examples.Please helpimprove itby adding sources thatevaluate within broader context. Relevant discussion may be found on thetalk page.(February 2023)(Learn how and when to remove this message) |
| --- | --- |

 

[Stanford University](./Stanford_University) stream processing projects included the Stanford Real-Time Programmable Shading Project started in 1999.[[7]](./Stream_processing#cite_note-7)
A prototype called Imagine was developed in 2002.[[8]](./Stream_processing#cite_note-8)
A project called Merrimac ran until about 2004.[[9]](./Stream_processing#cite_note-9) [AT&T](./AT&T) also researched stream-enhanced processors as [graphics processing units](./Graphics_processing_unit) rapidly evolved in both speed and functionality.[](https://en.wikipedia.org/wiki/Stream_processing#endnote_GPUasSTREAM) Since these early days, dozens of stream processing languages have been developed, as well as specialized hardware.

 

### Programming model notes

 

The most immediate challenge in the realm of parallel processing does not lie as much in the type of hardware architecture used, but in how easy it will be to program the system in question in a real-world environment with acceptable performance. Machines like Imagine use a straightforward single-threaded model with automated dependencies, memory allocation and [DMA](./Direct_memory_access) scheduling. This in itself is a result of the research at MIT and Stanford in finding an optimal *layering of tasks* between programmer, tools and hardware. Programmers beat tools in mapping algorithms to parallel hardware, and tools beat programmers in figuring out smartest memory allocation schemes, etc. Of particular concern are MIMD designs such as [Cell](./Cell_(microprocessor)), for which the programmer needs to deal with application partitioning across multiple cores and deal with process synchronization and load balancing.

 

A drawback of SIMD programming was the issue of [array-of-structures (AoS) and structure-of-arrays (SoA)](./Array-of-structures_(AoS)_and_structure-of-arrays_(SoA)). Programmers often create representations of enitities in memory, for example, the location of a particle in 3D space, the colour of the ball and its size as below:

 
```
 // A particle in a three-dimensional space.
struct Particle {
    double x; 
    double y;
    double z;

    // 8 bit per channel, say we care about RGB only
    unsigned byte color[3];
    float size;
    // ... and many other attributes may follow...
};

```
 

When multiple of these structures exist in memory they are placed end to end creating an [arrays](./Array_data_structure) in an *[array of structures](./Array_of_structures)* (AoS) topology. This means that should some algorithm be applied to the location of each particle in turn it must skip over memory locations containing the other attributes. If these attributes are not needed this results in wasteful usage of the CPU cache. Additionally, a SIMD instruction will typically expect the data it will operate on to be contiguous in memory, the elements may also need to be [aligned](./Data_structure_alignment). By moving the memory location of the data out of the structure data can be better organised for efficient access in a stream and for SIMD instructions to operate one. A *[structure of arrays](./Structure_of_arrays)* (SoA), as shown below, can allow this.

 
```
struct Particle {
    double* x; 
    double* y;
    double* z;

    unsigned byte* colorRed; 
    unsigned byte* colorBlue;
    unsigned byte* colorGreen;

    float* size;
};

```
 

Instead of holding the data in the structure, it holds only pointers (memory locations) for the data. Shortcomings are that if multiple attributes to of an object are to be operated on they might now be distant in memory and so result in a cache miss. The aligning and any needed padding lead to increased memory usage. Overall, memory management may be more complicated if structures are added and removed for example.

 

For stream processors, the usage of structures is encouraged. From an application point of view, all the attributes can be defined with some flexibility.
Taking GPUs as reference, there is a set of attributes (at least 16) available. For each attribute, the application can state the number of components and the format of the components (but only primitive data types are supported for now). The various attributes are then attached to a memory block, possibly defining a *stride* between 'consecutive' elements of the same attributes, effectively allowing interleaved data.
When the GPU begins the stream processing, it will *gather* all the various attributes in a single set of parameters (usually this looks like a structure or a "magic global variable"), performs the operations and *scatters* the results to some memory area for later processing (or retrieving).

 

More modern stream processing frameworks provide a FIFO like interface to structure data as a literal stream. This abstraction 
provides a means to specify data dependencies implicitly while enabling the runtime/hardware to take full advantage of that 
knowledge for efficient computation. One of the simplest[*[citation needed](./Wikipedia:Citation_needed)*] and most efficient[*[citation needed](./Wikipedia:Citation_needed)*] stream processing modalities to date for C++, 
is [RaftLib](./RaftLib), which enables linking independent [compute kernels](./Compute_kernel) together as a data flow graph using C++ stream operators. As an example:

 
```
import <raft>;
import <raftio>;

import std;

using String = std::string;

using RaftKernel = raft::kernel;
using RaftKernelStatus = raft::kstatus;
using RaftMap = raft::map;
using RaftPrint = raft::print;

class HelloWorld : public RaftKernel {
public:
    HelloWorld() {
        output.addPort<String>("0"); 
    }

    virtual RaftKernelStatus run() {
        output["0"].push("Hello World\n");
        return raft::stop; 
    }
};

int main(int argc, char* argv[]) {
    // instantiate print kernel
    RaftPrint<String> p;

    // instantiate hello world kernel
    HelloWorld hello;

    // make a map object
    RaftMap m;

    // add kernels to map, both hello and p are executed concurrently
    m += hello >> p;

    // execute the map
    m.exe();

    return 0;
}

```
 

### Models of computation for stream processing

 

Apart from specifying streaming applications in high-level languages, models of computation (MoCs) also have been widely used as [dataflow](./Dataflow) models and process-based models.

 

### Generic processor architecture

 

Historically, CPUs began implementing various tiers of memory access optimizations because of the ever-increasing performance when compared to relatively slow growing external memory bandwidth. As this gap widened, big amounts of die area were dedicated to hiding memory latencies. Since fetching information and opcodes to those few ALUs is expensive, very little die area is dedicated to actual mathematical machinery (as a rough estimation, consider it to be less than 10%).

 

A similar architecture exists on stream processors but thanks to the new programming model, the amount of transistors dedicated to management is actually very little.

 

Beginning from a whole system point of view, stream processors usually exist in a controlled environment. GPUs do exist on an add-in board (this seems to also apply to Imagine). CPUs continue do the job of managing system resources, running applications, and such.

 

The stream processor is usually equipped with a fast, efficient, proprietary memory bus (crossbar switches are now common, multi-buses have been employed in the past). The exact amount of memory lanes is dependent on the market range. As this is written, there are still 64-bit wide interconnections around (entry-level). Most mid-range models use a fast 128-bit crossbar switch matrix (4 or 2 segments), while high-end models deploy huge amounts of memory (actually up to 512 MB) with a slightly slower crossbar that is 256 bits wide. By contrast, standard processors from [Intel Pentium](./Intel_Pentium) to some [Athlon 64](./Athlon_64) have only a single 64-bit wide data bus.

 

Memory access patterns are much more predictable. While arrays do exist, their dimension is fixed at kernel invocation. The thing which most closely matches a multiple pointer indirection is an *indirection chain*, which is however guaranteed to finally read or write from a specific memory area (inside a stream).

 

Because of the SIMD nature of the stream processor's execution units (ALUs clusters), read/write operations are expected to happen in bulk, so memories are optimized for high bandwidth rather than low latency (this is a difference from [Rambus](./Rambus) and [DDR SDRAM](./DDR_SDRAM), for example). This also allows for efficient memory bus negotiations.

 

Most (90%) of a stream processor's work is done on-chip, requiring only 1% of the global data to be stored to memory. This is where knowing the kernel temporaries and dependencies pays.

 

Internally, a stream processor features some clever communication and management circuits but what's interesting is the *Stream Register File* (SRF). This is conceptually a large cache in which stream data is stored to be transferred to external memory in bulks. As a cache-like software-controlled structure to the various [ALUs](./Arithmetic_logic_unit), the SRF is shared between all the various ALU clusters. The key concept and innovation here done with Stanford's Imagine chip is that the compiler is able to automate and allocate memory in an optimal way, fully transparent to the programmer. The dependencies between kernel functions and data is known through the programming model which enables the compiler to perform flow analysis and optimally pack the SRFs. Commonly, this cache and DMA management can take up the majority of a project's schedule, something the stream processor (or at least Imagine) totally automates. Tests done at Stanford showed that the compiler did an as well or better job at scheduling memory than if you hand tuned the thing with much effort.

 

There is proof; there can be a lot of clusters because inter-cluster communication is assumed to be rare. Internally however, each cluster can efficiently exploit a much lower amount of ALUs because intra-cluster communication is common and thus needs to be highly efficient.

 

To keep those ALUs fetched with data, each ALU is equipped with local register files (LRFs), which are basically its usable registers.

 

This three-tiered data access pattern, makes it easy to keep temporary data away from slow memories, thus making the silicon implementation highly efficient and power-saving.

 

### Hardware-in-the-loop issues

 
|  | This sectionmay beconfusing or unclearto readers.Please helpclarify the section. There might be a discussion about this onthe talk page.(January 2008)(Learn how and when to remove this message) |
| --- | --- |

  In a revision (as of 07:40, 8 January 2008) an user noted this was considered not relevant. Since those issues are slightly covered in the references, it seems they are. Most of the statements here can be inferred from the references while others are simply involved in using PCIe transactions (so referencing them here doesn't seem a wise idea) &#x2D; keeping the tag anyway to gain more attention.  

Although an order of magnitude speedup can be reasonably expected (even from mainstream GPUs when computing in a streaming manner), not all applications benefit from this. Communication latencies are actually the biggest problem. Although [PCI Express](./PCI_Express) improved this with full-duplex communications, getting a GPU (and possibly a generic stream processor) to work will possibly take long amounts of time. This means it's usually counter-productive to use them for small datasets. Because changing the kernel is a rather expensive operation the stream architecture also incurs penalties for small streams, a behaviour referred to as the *short stream effect*.

 

[Pipelining](./Instruction_pipeline) is a very widespread and heavily used practice on stream processors, with GPUs featuring pipelines exceeding 200 stages. The cost for switching settings is dependent on the setting being modified but it is now considered to always be expensive. To avoid those problems at various levels of the pipeline, many techniques have been deployed such as "über shaders" and "texture atlases". Those techniques are game-oriented because of the nature of GPUs, but the concepts are interesting for generic stream processing as well.

 

## Examples

 
|  | This section has multiple issues.Please helpimprove itor discuss these issues on thetalk page.(Learn how and when to remove these messages)This sectionmay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(January 2026)(Learn how and when to remove this message)This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Stream processing"–news·newspapers·books·scholar·JSTOR(January 2026)(Learn how and when to remove this message)(Learn how and when to remove this message) |  | This sectionmay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(January 2026)(Learn how and when to remove this message) |  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Stream processing"–news·newspapers·books·scholar·JSTOR(January 2026)(Learn how and when to remove this message) |
| --- | --- | --- | --- | --- | --- |
|  | This sectionmay be too technical for most readers to understand.Pleasehelp improve ittomake it understandable to non-experts, without removing the technical details.(January 2026)(Learn how and when to remove this message) |
|  | This sectionneeds additional citations forverification.Please helpimprove this articlebyadding citations to reliable sourcesin this section. Unsourced material may be challenged and removed.Find sources:"Stream processing"–news·newspapers·books·scholar·JSTOR(January 2026)(Learn how and when to remove this message) |

 
- The [blitter](./Blitter) in the Commodore [Amiga](./Amiga) is an early (circa 1985) graphics processor capable of combining three source streams of 16 component bit vectors in 256 ways to produce an output stream consisting of 16 component bit vectors. Total input stream bandwidth is up to 42 million bits per second. Output stream bandwidth is up to 28 million bits per second.
- Imagine,[[10]](./Stream_processing#cite_note-10) headed by [William Dally](./Bill_Dally) of [Stanford University](./Stanford_University), is a flexible architecture intended to be both fast and energy efficient. The project, originally conceived in 1996, included architecture, software tools, a [very-large-scale integration](./Very-large-scale_integration) (VLSI) and a development board, was funded by [DARPA](./DARPA), [Intel](./Intel) and [Texas Instruments](./Texas_Instruments).
- Another [Stanford](./Stanford) project, called Merrimac,[[11]](./Stream_processing#cite_note-11) is aimed at developing a stream-based supercomputer.[*[as of?](./Wikipedia:Manual_of_Style/Dates_and_numbers#Chronological_items)*] Merrimac intends to use a stream architecture and advanced interconnection networks to provide more performance per unit cost than cluster-based scientific computers built from the same technology.
- The Storm-1 family from [Stream Processors, Inc](./Stream_Processors,_Inc), a commercial spin-off of Stanford's Imagine project, was announced during a feature presentation at [International Solid-State Circuits Conference](./International_Solid-State_Circuits_Conference) (ISSCC) 2007. The family contains four members ranging from 30 GOPS to 220 16-bit GOPS (billions of operations per second),[*[jargon](./Wikipedia:Manual_of_Style#Technical_language)*] all fabricated at [TSMC](./TSMC) in a 130 nanometer process. The devices target the high end of the [digital signal processor](./Digital_signal_processor) (DSP) market including [video conferencing](./Video_conferencing), [multifunction printers](./Multifunction_printer) and digital [video surveillance](./Video_surveillance) equipment.
- [GPUs](./GPU) are widespread, consumer-grade stream processors[](https://en.wikipedia.org/wiki/Stream_processing#endnote_GPUasSTREAM) designed mainly by [AMD](./AMD) and [Nvidia](./Nvidia). Various generations to be noted[*[according to whom?](./Wikipedia:Manual_of_Style/Words_to_watch#Unsupported_attributions)*] from a stream processing point of view:

- Pre-R2xx/NV2x: no explicit support for stream processing. Kernel operations were hidden in the [application programming interface](./API) (API) and provided too little flexibility for general use.
- R2xx/NV2x: kernel stream operations became explicitly under the programmer's control but only for vertex processing (fragments were still using old paradigms). No branching support severely hampered flexibility but some types of algorithms could be run (notably, low-precision fluid simulation).
- R3xx/NV4x: flexible branching support although some limitations still exist on the number of operations to be executed and strict recursion depth, as well as array manipulation.
- R8xx: Supports append/consume buffers and atomic operations. This generation is the state of the art.[*[peacock prose](./Wikipedia:Manual_of_Style/Words_to_watch#Puffery)*] What does this mean? It means it's a TODO. Remember we should track functionalities here rather than performance improvements. 

- [AMD FireStream](./AMD_FireStream) brand name for product line targeting HPC
- [Nvidia Tesla](./Nvidia_Tesla) brand name for product line targeting HPC
- The [Cell processor](./Cell_processor) from STI, an alliance of [Sony Computer Entertainment](./Sony_Computer_Entertainment), [Toshiba Corporation](./Toshiba_Corporation), and [IBM](./IBM), is a hardware architecture that can function like a stream processor with appropriate software support. It consists of a controlling processor, the PPE (Power Processing Element, an IBM [PowerPC](./PowerPC)) and a set of SIMD coprocessors, called SPEs (Synergistic Processing Elements), each with independent program counters and instruction memory, in effect a [multiple instruction, multiple data](./Multiple_instruction,_multiple_data) (MIMD) machine. In the native programming model all [direct memory access](./Direct_memory_access) (DMA) and program scheduling is left up to the programmer. The hardware provides a fast ring bus among the processors for local communication. Because the local memory for instructions and data is limited the only programs that can exploit this architecture effectively either require a very small [memory footprint](./Memory_footprint) or adhere to a stream programming model. With a suitable algorithm the performance of the Cell can rival that of pure stream processors, however this nearly always requires a complete redesign of algorithms and software.

 

## Stream programming libraries and languages

 

Most programming languages for stream processors start with Java, C or C++ and add extensions which provide specific instructions to allow application developers to tag kernels and/or streams. This also applies to most [shading languages](./Shading_language), which can be considered stream programming languages to a certain degree.

 

Non-commercial examples of stream programming languages include:

 
- [Ateji PX](./Ateji_PX) Free Edition, enables a simple expression of stream programming, the actor model, and the MapReduce algorithm on [JVM](./JVM)
- Auto-Pipe, from the Stream Based Supercomputing Lab at [Washington University in St. Louis](./Washington_University_in_St._Louis), an application development environment for streaming applications that allows authoring of applications for heterogeneous systems (CPU, [GPGPU](./GPGPU), FPGA). Applications can be developed in any combination of C, C++, and Java for the CPU. Verilog or VHDL for FPGAs. Cuda is currently used for Nvidia GPGPUs. Auto-Pipe also handles coordination of TCP connections between multiple machines.
- ACOTES programming model: language from [Polytechnic University of Catalonia](./Polytechnic_University_of_Catalonia) based on [OpenMP](./OpenMP)
- BeepBeep, a simple and lightweight Java-based event stream processing library from the Formal Computer Science Lab at [Université du Québec à Chicoutimi](./UQAC)
- Brook language from [Stanford](./Stanford)
- [CAL Actor Language](./CAL_Actor_Language): a high-level programming language for writing (dataflow) actors, which are stateful operators that transform input streams of data objects (tokens) into output streams.
- Cal2Many a code generation framework from Halmstad University, Sweden. It takes CAL code as input and generates different target specific languages including sequential C, Chisel, parallel C targeting Epiphany architecture, ajava & astruct targeting Ambric architecture, etc..
- DUP language from [Technical University of Munich](./Technical_University_of_Munich) and [University of Denver](./University_of_Denver)
- HSTREAM: a directive-based language extension for heterogeneous stream computing[[12]](./Stream_processing#cite_note-12)
- RaftLib - open source C++ stream processing template library originally from the Stream Based Supercomputing Lab at [Washington University in St. Louis](./Washington_University_in_St._Louis)
- [Rimmel.js](https://github.com/reactivehtml/rimmel) a JavaScript library enabling streams-based UI development by treating all HTML nodes and attributes as reactive sources and sinks)
- SPar - C++ domain-specific language for expressing stream parallelism from the Application Modelling Group (GMAP) at [Pontifical Catholic University of Rio Grande do Sul](./Pontifical_Catholic_University_of_Rio_Grande_do_Sul)
- [Sh](./Lib_Sh) library from the [University of Waterloo](./University_of_Waterloo)
- Shallows, an open source project
- S-Net coordination language from the [University of Hertfordshire](./University_of_Hertfordshire), which provides separation of coordination and algorithmic programming
- StreamIt from [MIT](./MIT)
- Siddhi from [WSO2](./WSO2)
- WaveScript functional stream processing, also from MIT.
- [Functional reactive programming](./Functional_reactive_programming) could be considered stream processing in a broad sense.

 

Commercial implementations are either general purpose or tied to specific hardware by a vendor. Examples of general purpose languages include:

 
- [AccelerEyes](./AccelerEyes)' Jacket, a commercialization of a GPU engine for MATLAB
- [Ateji PX](./Ateji_PX) Java extension that enables a simple expression of stream programming, the Actor model, and the MapReduce algorithm
- Embiot, a lightweight embedded streaming analytics agent from Telchemy
- Floodgate, a stream processor provided with the [Gamebryo](./Gamebryo) game engine for PlayStation 3, Xbox360, Wii, and PC
- [OpenHMPP](./OpenHMPP), a "directive" vision of Many-Core programming
- PeakStream,[[13]](./Stream_processing#cite_note-13) a spinout of the [Brook](./BrookGPU) project (acquired by [Google](./List_of_Google_acquisitions) in June 2007)
- IBM Spade - Stream Processing Application Declarative Engine (B. Gedik, et al. SPADE: the system S declarative stream processing engine. ACM SIGMOD 2008.)
- [RapidMind](./RapidMind), a commercialization of [Sh](./Lib_Sh) (acquired by [Intel](./Intel) in August 2009)
- TStreams,[[14]](./Stream_processing#cite_note-14)[[15]](./Stream_processing#cite_note-15) Hewlett-Packard Cambridge Research Lab

 

Vendor-specific languages include:

 
- Brook+ (AMD hardware optimized implementation of [Brook](./BrookGPU)) from [AMD](./AMD)/[ATI](./ATI_Technologies)
- [CUDA](./CUDA) (Compute Unified Device Architecture) from [Nvidia](./Nvidia)
- [Intel Ct](./Intel_Ct) - C for [Throughput Computing](./High-throughput_computing)
- StreamC from [Stream Processors, Inc](./Stream_Processors,_Inc), a commercialization of the Imagine work at Stanford

 

Event-Based Processing

 
- [Apama](./Apama_(software)) - a combined [complex event](./Complex_event_processing) and [stream processing](./Stream_Processing) engine by [Software AG](./Software_AG)
- Wallaroo
- WSO2 stream processor by [WSO2](./WSO2)
- [Apache NiFi](./Apache_NiFi)

 

Batch file-based processing (emulates some of actual stream processing, but much lower performance in general[*[clarification needed](./Wikipedia:Please_clarify)*][*[citation needed](./Wikipedia:Citation_needed)*])

 
- [Apache Kafka](./Apache_Kafka)
- [Apache Storm](./Apache_Storm)
- [Apache Apex](./Apache_Apex)
- [Apache Spark](./Apache_Spark)

 

Continuous operator stream processing[*[clarification needed](./Wikipedia:Please_clarify)*]

 
- [Apache Flink](./Apache_Flink)
- Walmartlabs Mupd8[[16]](./Stream_processing#cite_note-16)
- Eclipse Streamsheets - spreadsheet for stream processing

 

Stream processing services:

 
- Amazon Web Services - Kinesis
- Google Cloud - Dataflow
- Microsoft Azure - Stream analytics
- Datastreams - Data streaming analytics platform
- IBM streams

- IBM streaming analytics

- Eventador SQLStreamBuilder

 

## See also

  
- [Data stream mining](./Data_stream_mining)
- [Data Stream Management System](./Data_Stream_Management_System)
- [Dimension reduction](./Dimension_reduction)
- [Flow-based programming](./Flow-based_programming)
- [Hardware acceleration](./Hardware_acceleration)
- [Molecular modeling on GPU](./Molecular_modeling_on_GPU)
- [Parallel computing](./Parallel_computing)
- [Partitioned global address space](./Partitioned_global_address_space)
- [Real-time computing](./Real-time_computing)
- [Real Time Streaming Protocol](./Real_Time_Streaming_Protocol)
- [SIMT](./Single_instruction,_multiple_threads)
- [Streaming algorithm](./Streaming_algorithm)
- [Vector processor](./Vector_processor)

 
Links from old [[event stream processing]] page &#x2D;&#x2D; copied relevant entries above.
* [[Complex event processing]] (CEP) &#x2D; A related technology for building and managing event&#x2D;driven information systems.
* [[Data Stream Management System]] (DSMS) &#x2D; A type of software system for managing and querying data streams 
* [[openPDC]] A complete set of applications for processing streaming time&#x2D;series data in real&#x2D;time.
* [[Real&#x2D;time computing]] &#x2D; ESP systems are typically real&#x2D;time systems
* [[RFID]] &#x2D; Radio&#x2D;frequency identification, or RFID, recommends application of ESP to prevent from data flooding
* [[SCADA]] &#x2D; Supervisory control and data acquisition, a similar technology used in engineering applications
* [[Apache Flink]] &#x2D; An open&#x2D;source stream processing framework for distributed, scalable data streaming applications
 

## References

 
1. [↑](./Stream_processing#cite_ref-1) [A SHORT INTRO TO STREAM PROCESSING](https://www.jonathanbeard.io/blog/2015/09/19/streaming-and-dataflow.html)
2. [↑](./Stream_processing#cite_ref-2) [FCUDA: Enabling Efficient Compilation of CUDA Kernels onto FPGAs](http://impact.crhc.illinois.edu/shared/papers/fcuda2009.pdf)
3. [↑](./Stream_processing#cite_ref-3) IEEE Journal of Solid-State Circuits:["A Programmable 512 GOPS Stream Processor for Signal, Image, and Video Processing"](https://ieeexplore.ieee.org/document/4443192/;jsessionid=0F8BC0D153AF18E47A29359358253544?arnumber=4443192), Stanford University and Stream Processors, Inc.
4. [↑](./Stream_processing#cite_ref-4) Khailany, Dally, Rixner, Kapasi, Owens and Towles: ["Exploring VLSI Scalability of Stream Processors"](http://cva.stanford.edu/publications/2003/khailany_im_scalability.pdf), Stanford and Rice University.
5. [↑](./Stream_processing#cite_ref-5) Gummaraju and Rosenblum, ["Stream processing in General-Purpose Processors"](http://www.cs.utexas.edu/users/skeckler/wild04/Paper14.pdf), Stanford University.
6. [↑](./Stream_processing#cite_ref-6) Kapasi, Dally, Rixner, Khailany, Owens, Ahn and Mattson, ["Programmable Stream Processors"](http://cva.stanford.edu/publications/2003/ieeecomputer_stream.pdf), Universities of Stanford, Rice, California (Davis) and Reservoir Labs.
7. [↑](./Stream_processing#cite_ref-7) Eric Chan. ["Stanford Real-Time Programmable Shading Project"](http://graphics.stanford.edu/projects/shading/). *Research group web site*. Retrieved March 9, 2017.
8. [↑](./Stream_processing#cite_ref-8) ["The Imagine - Image and Signal Processor"](http://cva.stanford.edu/projects/imagine/). *Group web site*. Retrieved March 9, 2017.
9. [↑](./Stream_processing#cite_ref-9) ["Merrimac - Stanford Streaming Supercomputer Project"](https://web.archive.org/web/20131218194055/http://merrimac.stanford.edu/). *Group web site*. Archived from [the original](http://merrimac.stanford.edu/) on December 18, 2013. Retrieved March 9, 2017.
10. [↑](./Stream_processing#cite_ref-10) [Imagine](http://cva.stanford.edu/projects/imagine/)
11. [↑](./Stream_processing#cite_ref-11) [Merrimac](http://merrimac.stanford.edu/)
12. [↑](./Stream_processing#cite_ref-12) Memeti, Suejb; Pllana, Sabri (October 2018). "HSTREAM: A Directive-Based Language Extension for Heterogeneous Stream Computing". *2018 IEEE International Conference on Computational Science and Engineering (CSE)*. IEEE. pp. 138–145. [arXiv](./ArXiv_(identifier)):[1809.09387](https://arxiv.org/abs/1809.09387). [doi](./Doi_(identifier)):[10.1109/CSE.2018.00026](https://doi.org/10.1109%2FCSE.2018.00026). [ISBN](./ISBN_(identifier)) [978-1-5386-7649-3](./Special:BookSources/978-1-5386-7649-3).
13. [↑](./Stream_processing#cite_ref-13) [PeakStream unveils multicore and CPU/GPU programming solution Bot generated title ](https://arstechnica.com/news.ars/post/20060918-7763.html)
14. [↑](./Stream_processing#cite_ref-14) [*TStreams: A Model of Parallel Computation*](http://www.hpl.hp.com/techreports/2004/HPL-2004-78R1.html) (Technical report).
15. [↑](./Stream_processing#cite_ref-15) [*TStreams: How to Write a Parallel Program*](http://www.hpl.hp.com/techreports/2004/HPL-2004-193.html) (Technical report).
16. [↑](./Stream_processing#cite_ref-16) ["GitHub - walmartlabs/Mupd8: Muppet"](https://github.com/walmartlabs/mupd8). *[GitHub](./GitHub)*.

 

 

 
| vteParallel computing |
| --- |
| General | Distributed computingParallel computingParallel algorithmMassively parallelCloud computingHigh-performance computingMultiprocessingManycore processorGPGPUComputer networkSystolic array |
| Levels | BitInstructionThreadTaskDataMemoryLoopPipeline |
| Multithreading | TemporalSimultaneous(SMT)Simultaneous and heterogenousSpeculative(SpMT)PreemptiveCooperativeClustered multi-thread(CMT)Hardware scout |
| Theory | PRAM modelPEM modelAnalysis of parallel algorithmsAmdahl's lawGustafson's lawCost efficiencyKarp–Flatt metricSlowdownSpeedup |
| Elements | ProcessThreadFiberInstruction windowArray |
| Coordination | MultiprocessingMemory coherenceCache coherenceCache invalidationBarrierSynchronizationApplication checkpointing |
| Programming | Stream processingDataflow programmingModelsImplicit parallelismExplicit parallelismConcurrencyNon-blocking algorithm |
| Hardware | Flynn's taxonomySISDSIMDArray processing(SIMT)Pipelined processingAssociative processingMISDMIMDDataflow architecturePipelined processorSuperscalar processorVector processorMultiprocessorsymmetricasymmetricMemoryshareddistributeddistributed sharedUMANUMACOMAMassively parallelcomputerComputer clusterBeowulf clusterGrid computerHardware acceleration |
| APIs | Ateji PXBoostChapelHPXCharm++CilkCoarray FortranCUDADryadC++ AMPGlobal ArraysGPUOpenMPIOpenMPOpenCLOpenHMPPOpenACCParallel ExtensionsPVMpthreadsRaftLibROCmUPCTBBZPL |
| Problems | Automatic parallelizationCache stampedeDeadlockDeterministic algorithmEmbarrassingly parallelParallel slowdownRace conditionSoftware lockoutScalabilityStarvation |
| Category: Parallel computing |

 
| vteProgramming paradigms |
| --- |
| Imperative | StructuredJackson structuresBlock-structuredModularNon-structuredProceduralProgramming in the large and in the smallDesign by contractInvariant-basedNested functionObject-orientedClass-based,Prototype-based,Object-basedAgentImmutable objectPersistentUniform function call syntax | Structured | Jackson structuresBlock-structuredModularNon-structuredProceduralProgramming in the large and in the smallDesign by contractInvariant-basedNested function | Object-oriented | Class-based,Prototype-based,Object-basedAgentImmutable objectPersistentUniform function call syntax |
| Structured | Jackson structuresBlock-structuredModularNon-structuredProceduralProgramming in the large and in the smallDesign by contractInvariant-basedNested function |
| Object-oriented | Class-based,Prototype-based,Object-basedAgentImmutable objectPersistentUniform function call syntax |
| Declarative | FunctionalRecursiveAnonymous function(Partial application)Higher-orderPurely functionalTotalStrictGADTsDependent typesFunctional logicPoint-free styleExpression-orientedApplicative,ConcatenativeFunction-level,Value-levelMonadDataflowFlow-basedReactive(Functional reactive)SignalsStreamsSynchronousLogicAbductive logicAnswer setConstraint(Constraint logic)Inductive logicNondeterministicOntologyProbabilistic logicQueryDomain-specificlanguage(DSL)Algebraic modelingArrayAutomata-based(Action)Command(Spacecraft)DifferentiableEnd-userGrammar-orientedInterface descriptionLanguage-orientedList comprehensionLow-codeModelingNatural languageNon-English-basedPage descriptionPipesandfiltersProbabilisticQuantumScientificScriptingSet-theoreticSimulationStack-basedSystemTactileTemplatingTransformation(Graph rewriting,Production,Pattern)Visual | Functional | RecursiveAnonymous function(Partial application)Higher-orderPurely functionalTotalStrictGADTsDependent typesFunctional logicPoint-free styleExpression-orientedApplicative,ConcatenativeFunction-level,Value-levelMonad | Dataflow | Flow-basedReactive(Functional reactive)SignalsStreamsSynchronous | Logic | Abductive logicAnswer setConstraint(Constraint logic)Inductive logicNondeterministicOntologyProbabilistic logicQuery | Domain-specificlanguage(DSL) | Algebraic modelingArrayAutomata-based(Action)Command(Spacecraft)DifferentiableEnd-userGrammar-orientedInterface descriptionLanguage-orientedList comprehensionLow-codeModelingNatural languageNon-English-basedPage descriptionPipesandfiltersProbabilisticQuantumScientificScriptingSet-theoreticSimulationStack-basedSystemTactileTemplatingTransformation(Graph rewriting,Production,Pattern)Visual |
| Functional | RecursiveAnonymous function(Partial application)Higher-orderPurely functionalTotalStrictGADTsDependent typesFunctional logicPoint-free styleExpression-orientedApplicative,ConcatenativeFunction-level,Value-levelMonad |
| Dataflow | Flow-basedReactive(Functional reactive)SignalsStreamsSynchronous |
| Logic | Abductive logicAnswer setConstraint(Constraint logic)Inductive logicNondeterministicOntologyProbabilistic logicQuery |
| Domain-specificlanguage(DSL) | Algebraic modelingArrayAutomata-based(Action)Command(Spacecraft)DifferentiableEnd-userGrammar-orientedInterface descriptionLanguage-orientedList comprehensionLow-codeModelingNatural languageNon-English-basedPage descriptionPipesandfiltersProbabilisticQuantumScientificScriptingSet-theoreticSimulationStack-basedSystemTactileTemplatingTransformation(Graph rewriting,Production,Pattern)Visual |
| Concurrent,parallel | Actor-basedAutomatic mutual exclusionChoreographic programmingConcurrent logic(Concurrent constraint logic)Concurrent OOMacroprogrammingMultitier programmingOrganic computingParallel programming modelsPartitioned global address spaceProcess-orientedRelativistic programmingService-orientedStructured concurrency |
| Metaprogramming | Attribute-orientedAutomatic(Inductive)DynamicExtensibleGenericHomoiconicityInteractiveMacro(Hygienic)Metalinguistic abstractionMulti-stageProgram synthesis(Bayesian,by demonstration,by example,vibe coding)ReflectiveSelf-modifying codeSymbolicTemplate |
| Separationof concerns | AspectsComponentsData-drivenData-orientedEvent-drivenFeaturesLiterateRolesSubjects |
| Comparisons/Lists | Comparison(multi-paradigm,object-oriented,functional),List(OO,by type) |