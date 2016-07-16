This trip report summarize the SciPy 2016 conference. The conference
was held in Austin, Texas, July 11–17, 2016. SciPy 2016 was the 15th
annual Scientific Computing with Python conference. The annual SciPy
Conference brings together over 650 participants from industry,
academia, and government to showcase their latest projects, learn from
skilled users and developers, and collaborate on code development. The
full program consisted of two days of tutorials (July 11–12), three
days of talks (July 13–15), and two days of developer sprints (July
16–17). The attendee did not participate in the developer sprints, so
they will not be discussed in this trip report.

The attendee is a developer on the Lynx project, so most of his
conclusions are cast in the context of Lynx, though they may be
applicable to other Python-based software projects within NNL.

Tutorials
=========
Attendees were allowed to select from four half-day tutorials, though
many were coupled into full-day tutorials. The attendee participated
in the Scientific Python Software Carpentry course and the Machine
Learning with scikit-learn course. Each of these is summarized below.

Software Carpentry: Scientific Python
-------------------------------------
> Software Carpentry's mission is to help scientists and engineers get
> more research done in less time and with less pain by teaching them
> basic lab skills for scientific computing. This hands-on workshop
> will cover basic concepts and tools, including a brief review of
> programming in Python, version control with git, and an introduction
> to testing.

This course was intended for beginning Python programmers. Although
the attendee considers himself to be an intermediate Python
programmer, several good software practices were taught that will be
incorporated into the Lynx project.

The first hour of the course focused on the basics of Python, using
Jupyter notebooks as the platform. Normally, Software Carpentry
classes would spend significantly more time than this, but this
portion was minimized to make more time for version control and
testing. The next topic was source control with Git. The presenters
describes the basis of the Git system, using some simple examples to
demonstrate Git to new users. They then had the students set up
accounts on GitHub, and demonstrated the use of GitHub for
collaborative development. This included discussions about code
reviews via GitHub and pull requests.

The afternoon centered around testing in Python, using assertions for
preconditions and Pytest for unit and integration tests. For
regression testing, the point was made that tests for bugs should be
included in regression testing to prevent the bug from
reappearing. Finally, the concept of continuous integration (CI)
testing was introduced, which tied together all aspects of the course:
Python, version control, and testing. The Travis CI platform was used
as the continuous integration system. The instructors stressed the
importance of testing, and relayed the Python testing mantra as, "If
it’s not tested, it’s broken."

At NNL-Knolls, many Python and non-Python projects already use the Git
version control system successfully. The Lynx project uses Microsoft's
Team Foundation Server (TFS) in a similar manner as many open source
projects use GitHub. TFS lags behind GitHub in the tools it provides
for collaborative development, but is further along in integration
with work planning tools. It would be nice to provide an installation
of GitHub Enterprise for use in NNL, but due to the difficulty in
bringing in and hosting outside software, TFS will suffice for most
needs. As GitHub is further developed, it would be worthwhile to
monitor its development and see if it’s a tool NNL should pursue.

Likewise, the Lynx project uses Pytest extensively for unit and
integration tests. The developers could adopt a more aggressive stance
toward runtime testing using assertions. The Jenkins system is
provided at NNL for continuous integration testing, but developers
should consider providing Travis CI as well. This would allow for a
cleaner test environment and increased separation between the test
environment and the production HPC systems. Additionally, Travis CI
provides integration with GitHub, as well as the capability of testing
on multiple platforms and multiple configurations.

Machine Learning with scikit-learn
----------------------------------
> This tutorial aims to provide an introduction to machine learning
> and scikit-learn "from the ground up." We will start with core
> concepts of machine learning, some example uses of machine learning,
> and how to implement them using scikit-learn. Going in detail
> through the characteristics of several methods, we will discuss how
> to pick an algorithm for your application, how to set its
> parameters, and how to evaluate performance.

This course was geared toward intermediate-level Python programmers,
as well as newbies to machine learning. It covered concepts such as
supervised and unsupervised learning, scientific computing tools in
Python, training vs. testing data, classification, clustering,
cross-validation, grid searching, pipelining, performance metrics,
support vector machines, decision trees, and ensemble methods. The
concurrent engineering project could benefit greatly from these
capabilities, depending on the maturity of the Big Data project in
Engineering Computations. These capabilities are also in the R
language, and integration with R may be an approach if a pure-Python
approach lacks feasibility. All the scikit-learn computational methods
are implemented in Cython, and can be performed in multithread and
multiprocess configurations using standard Python tools.

Conference Talks
================
The conference proper was held July 13–15. Each day began with a
keynote address during the first half of the morning, with all
attendees present. The second half of each morning, as well as each
afternoon, consisted of three parallel sessions with different topical
focus areas. Both the keynote addresses and focus area talks will be
discussed below.

Keynote \#1: Altair: Declarative Statistical Visualization in Python
--------------------------------------------------------------------
(Brian Granger, Associate Professor of Physics, Cal Poly State University)

This speaker is the creator of iPython and the Jupyter ecosystem. He
announced that iPython v5.0 has been released and will be the last
version to support Python 2, with many cheers from the audience. He
also walked through a list of notable features of the Jupyter system,
including the JupyterLab project, which may serve as the basis for a
Python-based concurrent engineering system.

The speaker then presented a new Python visualization system called
Altair. His premise is that visualization in Python is painful, with
many choices of packages that have non-overlapping capabilities. These
packages require (sometimes significant) programming expertise to
perform even the simplest task. Altair seeks to simplify these choices
by introducing a grammar for visualization that abstracts a wide range
of visualization concepts: Data, Transforms, Scales, Guides, and
Marks. It uses a declarative Application Programming Interface (API),
specifying *what* should be done, instead of *how* it should be
done. Under the hood, Altair generates Vega JSON input and is
integrated into Jupyter tools. The Vega system reads the JSON input
and generates the appropriate JavaScript to accomplish the
visualization task.

The speaker has spoken with the owners of the other Python
visualization libraries, such as Matplotlib and Bokeh, and there is
interest in those packages adopting Vega as a standard language as
well. Altair provides a carefully designed API, which includes type
checked attributes, a thin layer of methods, method chaining, and
operator overloading. The API follows the "flat is better than nested"
guidance. In addition to generating Vega JSON from Python code, Altair
can generate the Python code from Vega JSON input, allowing for full
utilization by any user.

Keynote \#2: High Performance with Python: Architectures, Approaches, and Applications
--------------------------------------------------------------------------------------
(Andreas Klöckner, Assistant Professor, University of Illinois at
Urbana-Champaign)

> Data-parallel programming plays a significant role in HPC, for the
> numerous applications that can leverage it and for the many parallel
> architectures that provide high performance for it. Literally, high
> performance computing means measuring, understanding, and improving
> performance as part of a scientific process, in which Python can be
> immensely helpful. Two key ingredients for this are just-in-time
> compilation, which enables run-time code generation, and
> transformation-based programming. After briefly exploring available
> programming models and abstractions, I will introduce and
> demonstrate PyOpenCL and Loopy, two complementary tools that help
> with all parts of this process. Unlocking good performance means
> experimenting with different algorithms, data layouts, approaches to
> parallelization. Conventionally, each of these requires a
> near-rewrite of the code under consideration. Loopy, by being based
> on transformations, entirely avoids this problem. Moreover, it
> separates application concerns from performance concerns, allowing
> the mathematical objective and its performant implementation to be
> expressed cleanly and separately. I will close with some examples
> that demonstrate the effectiveness of the approach.

The speaker is the author of the PyCUDA and PyOpenGL packages, as well
as many other high-performance packages for Python. He lamented that
recently the number of cores on a chip has been increasing, but the
individual cores have been slowing down. The solution for this has
been multithreading and/or multiprocessing, but these approaches are
well-known to the community so he focused his presentation on speeding
up single-core performance. He demonstrated his approach with a matrix
multiplication example that used nested loops. Typically, if one
wanted to increase performance of the operation (which took ~100 s in
pure Python), one would first use Numpy (~1 s), then Cython
(compile-time optimization) or Numba (just-in-time [JIT]
optimization), both of which resulted in a speedup of 300,000x (~300
ms). Although this sounds impressive, doing an analysis of the
specifications of his laptop, it was only 37% of the theoretical
capability of the hardware.

The speaker then described concurrent computing and
GPU[^Graphical Processing Unit. A GPU is a hardware device normally found in high-end graphics and computational machines that is optimized for certain types of (often vectorized) computational operations. Using GPUs for those or similar computations can significantly increase performance. The primary drawbacks include proprietary, complex programming languages and the need to transfer data to special memory accessible to the GPU.]
computing and proposes that programmers should decompose these
operations into tasks and approach a solution like in GPU
computing. The issue is that is not a simple thing to do and requires
expertise. He then introduced Loopy, which is a Python package for
generating GPU code from a common syntax. Using this package and
inspecting the generated C code, including vectorization and cache
utilization, he was able to tune his example algorithm to his machine;
the final runtime for his algorithm was 45 ms (better than optimal
because task were executed on the GPU as well). He also showed how
Loopy can predict the optimal runtime and memory usage for the
hardware. At this time, Loopy supports generation of OpenCL, CUDA,
Intel Xeon Phi, and Numba code.

Keynote \#3: Machine Learning for Social Science
------------------------------------------------
(Hanna Wallach, Microsoft Research NYC and Adjunct Associate
Professor, UMass Amherst)

The speaker is a social computer scientist who started programming
using MATLAB, then switched to C/C++ and Java, but ended up in Python
because it made programming much easier and less time consuming. She
started looking at using machine learning to analyze complex social
science problems. The speaker separates data analysis into two
categories: prediction (computer scientists) and explanation (social
scientists). These different goals lead to different analysis
approaches, which can many times conflict because prediction is
concerned about accuracy, which results in very complex models, while
explanation aims to understand connections between causes, which a
complicated model cannot allow. The speaker has been working on
measurement modeling, which can reconcile these conflicts

The speaker presented two examples of the use of measurement
modeling. The first example was analyzing declassified government
documents. She walked though the algorithm used (Poisson
decomposition) to analyze document word count and classify documents
according to their topics. The algorithm was written in only six lines
of Python code. Her analysis discovered temporal trends in global
events and in classification and declassification of documents, as
well as the department from which the document originated.

The second example dealt with international relations. Historically,
political scientists manually created databases of international
events, which were used to study international relationships. These
databases are time consuming to construct, and therefore very
restrictive. Recently, machine learning has been used to automate
collection and categorization of all this data. She used a similar
algorithm as above, but this time decomposing n-dimensional tensors to
analyze tensors of relationships. This extends the approach to
discover multilateral relations to determine *who* did *what* to
*whom*, *when*. She found the results simple enough for even
non-experts to consume and understand. The speaker posits that the
Poisson decomposition method is very useful for analyzing count data,
but cautions that social computer scientists must be careful with
ethical concerns that may be raised by "unbiased" models that
reinforce biases in society.

Wednesday Sessions
------------------
The following talks were presented at the sessions on Wednesday,
July 13. For each talk, the title is given, with the focus area in
brackets following the title, and well as the speakers’ names and
affiliations. Additionally, the provided summary of the talk is shown,
along with the attendees’ comments.

### Conduit: A Scientific Data Exchange Library for HPC Simulations \[HPC\]
(Cyrus Harrison, Brian Ryujin, and Adam Kunen, Lawrence Livermore
National Laboratory)

> Conduit (http://software.llnl.gov/conduit) is a new open source
> project from Lawrence Livermore National Laboratory. It provides an
> intuitive model for describing hierarchical scientific data in C++,
> C, Fortran, and Python. Conduit supports in-core data coupling
> between packages, serialization, and I/O tasks. Conduit leverages
> ideas from JSON and Numpy to provide a cross-language data access
> API that simplifies sharing data in the HPC ecosystem. For SciPy
> 2016, an important focus of our talk will be Python support in
> Conduit and how positive experiences using Python motivated our
> approach to build a sane cross-language data description solution.

Conduit is part of the Advanced Simulation and Computing (ASC)
Computational Science (CS) toolkit, which is being developed at
Lawrence Livermore National Laboratory (LLNL) for multiphysics
applications. The toolkit is composed of three modules: *Conduit*,
which is used to exchange data, *Relay*, which is a communications
library using MPI and WebSockets, and *Blueprint*, which supports
higher-level computational conventions, such as meshes. The
capabilities of the ASC CS toolkit are similar to those provided by
Lynx, but go a step further in that they include data access
mechanisms on the solver side.

Conduit supports solvers that use C++, Python, C, and Fortran. The
lead developers have experience on the Visit visualization project;
their technical expertise is in the areas of multiphysics and
deterministic transport. Until the development of Conduit, most data
exchange had been file-based; but Conduit focuses on in-core
(in-memory) data exchange. The requirements for Conduit development
include: a description mechanism for numeric primitives, support for
mixed-memory semantics, and the usage of higher-level conventions
(e.g., UNIX-like data paths) for data access. Conduit provides
JSON-based data descriptions and dynamic APIs to access the data.

At this time, the ASC CS toolkit is not yet mature enough to adopt as
a multiphysics simulation tool. It is still under development and is
linked with proprietary solvers. This being said, development of the
toolkit should be watched closely to learn from their development
issues and maturity of the system for potential usage at NNL.

### Bootstrapping an Open Source Library: How MetPy Got Up and Running with Lazy Developers \[Earth and Space Science\]
(Ryan May, UCAR/Unidata)

> MetPy is an open-source Python package for meteorology, providing
> domain-specific tools for reading data, performing calculations, and
> visualizing data that we have recently started developing
> actively. In order to keep code working and in good shape, and
> minimize the accrual of technical debt, the project developers have
> focused on making use of many cloud services to automate the
> development of the project. These services accomplish: static code
> analysis, continuous integration testing, automated documentation
> builds, and automated releases. We will present our experiences of
> how these services have helped with development, as well as
> challenges that presented themselves, with the goal to encourage
> others to use those to support their own development efforts.

This talk was essentially a summary of all the open-source testing
tools provided by GitHub, and the ones the presenter found useful in
his project. None of these tools are available at NNL, but they should
be brought in. The testing systems he uses are summarized below:

- Travis CI for continuous integration testing:
  - The presenter performs automated testing on all "current" versions
    of Python (2.7, 3.3, 3.4, and 3.5) with the latest versions of
    dependent packages.
  - He also includes special tests using the minimum supported
    versions of both Python and dependent packages to determine when
    he should bump versions. For example, if MetPy requires Numpy v1.8
    or greater, he has a test that specifically uses Numpy v1.8. When
    the test fails, he can change that requirement to use Numpy 1.9 as
    the minimum supported version.
  - He also has tests that run the developmental versions of Python
    and all required packages. These tests don’t dictate failure of
    the code, but alert him to possible issues before new releases
    come out.
- Sphinx is used to build the documentation, but can’t check for
  correctness, only the presence of Sphinx warnings; users are relied
  upon for correctness and grammar checking.
- Nbconvert can run example iPython notebooks, so it is used to test
  examples and tutorials.
- The Pytest plugin pytest-mpl performs image comparison tests and is
  used to test visualization output.
- Codecov.io is used for test coverage. It is a web application that
  provides good visualization of test coverage, and can track trends
  in coverage.
- Quantified Code and Codify are used for for static code checking,
  similar to Pylint and the PEP-8 checkers. These provide web
  interfaces and GitHub integration.
- Versioneer is a Python package that synchronizes version strings. It
  ensures the version string generated by a release from GitHub
  matches that in the Python Package Index and the distribution of the
  package.

The author’s usage of these tools was impressive. Any of these things
are done manually in the Lynx project and other Python projects at
NNL, but the developers could do a much better job. Getting systems
that automate these types of tests, and providing guidelines for the
types of tests that should be automated, should be pursued by the
computational software community.

### JupyterHub as an Interactive Supercomputing Gateway \[HPC\]
(Michael Milligan, Minnesota Supercomputing Institute, University of
Minnesota)

> At the Minnesota Supercomputing Institute we are exploring ways to
> provide the immediacy and flexibility of interactive computing
> within the batch-scheduled, tightly controlled world of traditional
> cluster supercomputing. As Jupyter Notebook has gained in
> popularity, the steps needed to use it within such an environment
> have proven to be a barrier to entry even as increasingly powerful
> Python tools have developed to take advantage of large computational
> resources. JupyterHub to the rescue! Except out of the box, it
> doesn't know anything about resource types, job submission, and so
> on. We developed BatchSpawner and friends as a general JupyterHub
> backend for batch-scheduled environments. In this talk I will walk
> through how we have deployed JupyterHub to provide a user-friendly
> gateway to interactive supercomputing.

The presenter works for the Minnesota Supercomputing Institute (MSI),
whose focus is interactive high-performance computing (HPC) through
web services. He presented BatchSpawner, which is a Python package
that uses JupyterHub to submit batch HPC jobs. The tool currently
integrates with the Torque and Slurm job scheduling systems, but could
be easily extended to support Platform LSF as well. Additionally, he
presented WrapSpawner, which allows HPC administrators to define job
profiles and users to select the profile to use. This could be used to
replace the queueing system currently used on the NNL HPCs by allowing
profiles from small, single-core jobs to jobs that have specific
memory requirements on many nodes. The presenter uses JupyterHub with
an Apache interface for authentication that supports Two-Factor
Authentication. All jobs can be interactive, and users never have to
wait as the job fails immediately if resources are not available. This
behavior can be overridden if desired.

Other tools used at the MSI that could be useful on our HPCs include
Puppet for dynamic configuration management and Splunk for logging and
tracking resource usage. The next steps include auto-population of
configuration options, environment management using Modules that works
with Python, integration with iPyParallel, and tunneling
visualization through the proxy for interactive parallel visualization
tasks.

### Experiments as Iterators: asyncio in Science \[Reproducibility\]
(Daniel Allan, Thomas Caswell, and Kenneth Lauer, Brookhaven National Lab)

> A key challenge to reproducible data collection is capturing and
> organizing metadata without constraining flexibility and
> improvisation. "Bluesky" is a data collection framework designed to
> solve this problem. It communicates with hardware through a
> high-level interface and performs data collection, capturing data
> and rich metadata for streaming, live analysis.
>
> The project is developed at the National Synchrotron Light Source
> II—a Department of Energy X-ray user facility. The X-ray beam is
> used by internal scientific staff and external visitors from
> academia and industry. These users employ Bluesky in a broad range
> of experiments, ranging from well-defined, established techniques to
> ad hoc, improvised experiments.
>
> Bluesky expresses an experimental procedure as an iterable. Each
> element in the iterable specifies a granular step: "Move motor X;
> read detector Y; ...." Bluesky supervises the execution of each step,
> handling common supervisory tasks: monitoring for problems,
> recovering from interruptions, safely cleaning up. In hardware
> control, the devil is in the details. Bluesky handles many of these
> details for the user, separating them from the scientific logic of
> the experimental procedure.
>
> While executing the procedure, bluesky collates all measurements
> and metadata into Python dictionaries with a flexible schema. These
> data "documents" are created in a streaming fashion during the
> experiment and dispatched to user-defined functions. They can be
> printed, plotted, written into a database, broadcast as JSON
> documents, or fed into a real-time processing pipeline.
>
> Bluesky employs Python language features not as commonly used in
> the SciPy community: generators, coroutines, and the asyncio event
> loop. For example, generators provide a parsimonious syntax for
> expressing sequential steps of an experiment. Coroutines can express
> adaptive logic, such as spacing measurements adaptively in response
> to the local slope, concentrating on regions of high
> variability. The asyncio event loop manages hardware control, data
> collection, visualization, and light-weight analysis in a single
> process. Wherever possible, bluesky relies on core language features
> and built-in data structures, avoiding a proliferation of special
> classes or a sprawling vocabulary.
>
> By integrating cleanly with the SciPy stack, bluesky empowers
> scientists to build sophisticated experimental control logic. While
> currently deployed for X-ray experiments at NSLS-II, bluesky is
> developed in the open and should be useful for scientific experiment
> control in any context. It is thoroughly documented at
> http://nsls-ii.github.io/bluesky. The source code is available at
> http://github.com/NSLS-II/bluesky.

The essence of the speaker’s work is included in the summary
above. The tool he developed uses many of the asynchronous
capabilities of Python 3 to control flow into and out of user-provided
routines. He designed an API that could be described as "declarative,"
which makes the user-provided routines much simpler to write. The Lynx
team should research declarative API design further and incorporate it
into the design of their system.

### Reproducible, One-Button Workflows with the Jupyter Notebook and SCons \[Reproducibility\]
(Jessica Hamrick, University of California, Berkeley)

> What is the best way to develop analysis code in the Jupyter
> notebook, while managing complex dependencies between analyses? In
> this talk, I will introduce nbflow, which is a project that
> integrates a Python-based build system (SCons) with the Jupyter
> notebook, enabling researchers to easily build sophisticated,
> complex analysis pipelines entirely within notebooks while still
> maintaining a "one-button workflow" in which all analyses can be
> executed, in the correct order, from a single command. I will show
> how nbflow can be applied to existing analyses and how it can be
> used to construct an analysis pipeline stretching the entire way
> from data cleaning, to computing statistics, to generating figures,
> and even to automatically generating LaTeX commands that can be used
> in publications to format results without the risk of copy-and-paste
> error.

This talk was interesting. The presenter is a graduate student who
wrote a simple API to define dependencies for SCons, a software
construction tool (similar to CMake) that is written in Python. SCons
can dynamically determine control flow based on dependencies between
targets. She used this system to perform her research and write her
thesis. If she changed data somewhere in a Jupyter notebook, the
system only ran what was necessary to reflect that change in the
results, including the results published in the thesis.

### Proselint: The Linting of Science Prose, and the Science of Prose Linting \[General\]
(Michael Pacer and Jordan Suchow, University of California, Berkeley)

> Writing is notoriously hard, even for the best writers, and it's not
> for lack of good advice—a tremendous amount of knowledge is strewn
> across usage guides, dictionaries, technical manuals, essays,
> pamphlets, websites, and the hearts and minds of great authors and
> editors. But this knowledge is trapped, waiting to be extracted and
> transformed. We built Proselint, a Python-based linter for
> prose. Proselint identifies violations of expert style and usage
> guidelines. Proselint is open-source software released under the BSD
> license and works with Python 2 and 3. It runs as a command-line
> utility or editor plugin (e.g., Sublime Text, Atom, Vim, Emacs) and
> outputs advice in standard formats (e.g., JSON). Though in its
> infancy—perhaps 2% of what it could be—Proselint already includes
> modules addressing: redundancy, jargon, illogic, clichés, sexism,
> misspelling, inconsistency, misuse of symbols, malapropisms,
> oxymorons, security gaffes, hedging, apologizing,
> pretension. Proselint can be seen as both a language tool for
> scientists and a tool for language science. On the one hand, it
> includes modules that promote clear and consistent prose in science
> writing. On the other, it measures language usage and explores the
> factors relevant to creating a useful linter.

The summary above reflects the content of this presentation. Proselint
appears to be a useful tool for documentation and letter-writing. It
recognizes many *text* formats, so to analyze a Word document or other
binary formats, it must first be converted to plain text using Pandoc.

### Reinventing the .whl: New Developments in the Upstream Python Packaging Ecosystem \[General\]
(Nathaniel Smith, UC Berkeley)

> Pip, wheels, and setuptools are the standard tools for installing,
> distributing, and building Python packages—which means that if
> you're a user or package author then you're probably using them at
> least some of the time, even though when it comes to handling
> scientific packages, they've traditionally been a major source of
> pain. Fortunately, things have been getting better! In this talk,
> I'll describe how members of the scientific Python community have
> been working with upstream Python to solve some of the worst issues,
> and show you how to build and distribute binary wheels for Linux
> users, build Windows packages without MSVC, use wheels to handle
> dependencies on non-Python libraries like BLAS or libhdf5, plus give
> the latest updates on our effort to drive a stake through the heart
> of setup.py files and replace them with something better.

This presentation updates the status of the Wheel system and how it
fits into the standard Python packaging system. The Python Package
Index (PyPI) is the standard way of obtaining pre-built package
distributions, and now has the ability to distribute packages
specifically for Linux. This allows packages that have extensive
external dependencies (like Numpy's dependency on BLAS) to include
those dependent libraries in a binary distribution. Additionally, the
presenter was curious why Microsoft libraries couldn't be linked from
open source compilers, like the GNU C Compiler (GCC). During his
investigation, the presenter discovered a bug in GCC that prevented it
from recognizing some Microsoft library wrappers. With a one-line fix,
GCC can now link against Microsoft libraries. This will help in
distributing package binaries for Windows.

### Lightning Talks
This session consisted of many short presentations on a variety of
topics. Many of them highlighted future conferences or logistical
concerns about this conferences, but one of interest was on
[conda-forge](#conda-forge). This is a collaborative system for
building and distributing Python packages, which is detailed later in
this trip report.

Thursday Sessions
-----------------
The following talks were presented at the sessions on Thursday,
July 14. For each talk, the title is given, with the focus area in
brackets following the title, and well as the speakers’ names and
affiliations. Additionally, the provided summary of the talk is shown,
along with the attendees’ comments.

### <a name="dask"/>Dask: Parallel and Distributed Computing \[General\]
(Matthew Rocklin and Jim Crist, Continuum Analytics)

> Dask is a pure Python library for parallel and distributed
> computing. Last year Dask parallelized Numpy and Pandas computations
> on multi-core workstations. This year we discuss using Dask to
> design custom algorithms and execute those algorithms efficiently on
> a cluster. This talk discusses Pythonic APIs for parallel algorithm
> development as well as strategies for intuitive and efficient
> distributed computing. We discuss recent results in machine learning
> and novel scientific applications.

The Dask package was originally designed to distribute Numpy and
Pandas calculations across a cluster of nodes, but as the developers
explore the other types of things the community does, they have
realized that there are more needs for distributed computing. Under
the hood, Dask uses a scheduler and a task graph to interact with and
assign tasks to nodes. The developers have written a thin API to
expose the scheduler and task graph to users. Additionally, in
addition to schedulers for synchronous, multithread, and multiprocess
tasks, they have written a distributed scheduler to interact with
large HPC machines. This scheduler decomposes the task graph and
assigns chunks of the graph to machines as they are available. With
this approach, the scheduler is able to add workers or graphs at any
time during execution, and knows how to re-create data so it can
recover from losing a worker as well. Dask also provides a web
interface for monitoring the job remotely as it proceeds.

The presenter demonstrated a new class called `Delayed`, which is a
lazy object that only executes its tasks when its `compute()` method
is called. This object is useful for inspecting the task graph and
asynchronously defining tasks and graphs. Additionally, he showed the
`dklearn` module, which is a Dask-aware wrapper of the scikit-learn
package for distributed machine learning.

The Dask package looks very similar to the eventual goal of the Lynx
task scheduler, and may be able to perform those tasks with little
modifications. The Lynx developers should look at replacing their
scheduler package with a Dask wrapper.

### Communicating Model Results \[Data Science\]
(Bargava Subramanian)

> For a data scientist building predictive models, the following are
> important:
>
> 1. How good is the model?
> 2. How good is it compared to competing/alternate models?
> 3. Is there a way to identify what worked in the models built so far,
>    to leverage it to build something even better?
>
> The stakeholder/end-user who finally uses the output from the
> model, for whom the ML process is mostly black-box, is concerned
> with the following:
>
> 1. How to trust the model output?
> 2. How to understand the drivers?
> 3. How to do what-if analysis?
>
> The unifying theme that could answer most of the above questions is
> visualization. The biggest challenge is to find a way to visualize
> the model, the model fitting process and the impact of drivers. This
> talk summarizes the learnings and key takeaways when communicating
> model results.

This presentation was an overview of commonly used plots in the data
science field. He used a simple example of stock prices to show
different plotting techniques. It is easy to plot the projections of a
single model, but how do you plot the model in the parameter space or
different models with different parameter spaces? Additionally, how
does one plot a parameter space with many dimensions? There were no
answers to these questions, but common approaches were shown. The
presenter pointed out that R has many more capabilities than Python
for plotting these types of data at this time, but developers are
working hard to add R-like capabilities to Python.

### SymPy Code Generation \[General\]
(Aaron Meurer and Anthony Scopatz, University of South Carolina)

> This talk showcases SymPy’s code generation capabilities. SymPy is
> a Python library that enables symbolic manipulation of mathematical
> expressions. Code generation is useful across a wide variety of
> domains. SymPy supports generating code for C, Fortran,
> Matlab/Octave, Python, Julia, Javascript, LLVM, Rust, and
> Theano. The code generation system is easily extensible to any
> language. Code generation supports a wide variety of expressions,
> including matrices. Code generation allows users to deal only with
> the high level mathematics of a problem, avoids mathematical errors
> and typos, makes it possible to deal with expressions that would
> otherwise be too large to write by hand, and opens possibilities to
> perform mathematical optimizations of expressions. SymPy’s code
> generation is used by libraries such as PyDy, chemreac, and
> sympybotics.

SymPy is a Python package that does symbolic mathematics, similar to
*Mathematica*. When used in Jupyter notebooks, SymPy results are
returned as MathJax (or LaTeX) output, displaying the result in purely
symbolic form. The presented showed a new capability of exporting
symbolic math as source code (similar to `CForm` in
*Mathematica*). This capability allows for mathematical optimizations
in addition to compiler optimizations. At this time, these mathematical
optimizations are limited to reducing the number of operations, and
not yet extended to more complex optimizations. The presenter
demonstrated this by symbolically solving a simple decay chain
problem, and a complex n-body pendulum problem. He then inverted the
pendulum problem to show dynamic control of the pendulum.

### Integrating Scripting into Commercial Applications \[Case Studies in Industry\]
(Eric Jones, CEO, Enthought)

Commercial customers use many types of commercial off-the-shelf (COTS)
software to perform their work, and they are interested in reducing
costs and making their employees' jobs easier, but they don't care
about software; they want modern tools, but they don't want to break
their current processes that work. The presenter discussed his
company's approach to addressing the concerns of his commercial
customers. He outlined two approaches depending on the tool he was
replacing or augmenting.

If the tool does not have a graphical interface, his approach is
simple: replace the physics engine with Python, then one can build all
kinds of things around the kernel. These things can be scripted input,
graphical interfaces, web interfaces, etc. If the tool does have a
graphical interface, there are several levels of options. The first
involves modifying the tool to read and write the data models that are
used under the hood, then writing external Python scripts that modify
these files and can be called through menu options. The second
approach involves accessing the internal data models directly through
Python, which can be more difficult but is often more performant as
well.

Enthought provides the tools to do this in the Canopy
project. Specifically, the CanopyGeo product, which was developed for
a geophysical customer. The geophysics solver in CanopyGeo can easily
be stripped out and replaced by another physics solver while keeping
the outside system intact. This allows a high-performance system to be
constructed that can handle large amounts of data efficiently (datasets
in CanopyGeo can be &gt;1 TB).

### Out with the Old and in with the New: Embedding Python in Old Fortran HPC Code \[HPC\]
(Brendan Smithyman, 3point Science, University of Western Ontario)

> Seismic Full-Waveform Inversion (FWI) is a field with decades-old
> academic codes. The program Fullwv started life in 1989, written in
> Fortran 77 by numerous researchers. We detail how we extended Fullwv
> and embedded a new Python-based FWI package called Zephyr. We
> override or replace portions of the Fortran source code with Python,
> to enable rapid development of new algorithms and methods.

- Compared writing "Hello, world!" in Python, F77, C, and Cython
- Showed how they can all call each other
- Motivation was to have students write new code in Python, and
  embedding that code in the legacy Fortran code
- Wrote a C API that can be called by Fortran, that initializes the
  Python interpreter, sends data from Fortran to Python, runs Python
  functions, and destroys the interpreter
- Nothing really beyond what we have done in Lynx, but its a little
  simpler to integrate new code in an existing solver

### <a name="conda-forge"/>Community Powered Packaging with conda-forge
(Philip Elson, Met Office)

> Conda has solved the package deployment problem. Users on any of the
> major operating systems can now use complex libraries by simply
> conda installing them—no need for a compiler, and typically no
> requirement for users to install packages at the operating system
> level.
>
> In solving the package deployment problem though, conda has
> introduced some problems of its own. Making high quality
> distributions available that aren't packaged by Continuum is
> complex. Considerations need to be made for things such as
> installing an appropriate Visual Studio, using a suitably old glibc,
> and ensuring that systems don't bleed dependencies from their own
> package managers.
>
> For some time this has been made easier by repositories, such as
> conda-recipes-scitools and ioos/conda-recipes to name but a few,
> making use of freely available continuous integration services to
> build and deploy conda distributions through a GitHub workflow. The
> reproducible and consistent environment used for building generally
> produces high quality distributions, and in some situations has even
> proved to be of valuable in fixing packages built by Continuum
> themselves.
>
> There remained one major problem with the model though—repositories
> were managing growing numbers of conda recipes without clear scope,
> resulting in recipe redundancy, duplication and inconsistencies in
> the community. Growing a single repository of many conda-recipes
> failed to scale in other ways too; it wasn't possible to give
> individual permissions on specific packages, and it wasn't possible
> to build every package for each commit of the repository.
>
> SciPy 2015 proved to be the ideal platform to refine and develop a
> plan to solve these issues, and to scale the conda package building
> pipeline out to a wider community of packagers.
>
> In this talk, I will present conda-forge—an ambitious project which
> has grown into a thriving community with openness and
> reproducibility at its core. conda-forge is a medley of
> technologies, including CI automation, Heroku, gitpython, pygithub,
> requests, GitHub webhooks, conda\[-build\[-all\]\] and Docker. I
> will present just some of the infrastructure which has been
> developed in order to support conda-forge's one package to one
> repository approach, and will demonstrate how you too can help with
> the maintenance of the packages that you care about through
> conda-forge.

Anaconda comes with a command line utility (called "conda") that is
used by the system for package management. The "conda-build" command
builds a package from a build recipe, which is defined in a
YAML-formatted file. A few years ago, the presenter developed a
package called ObviousCI that could be used in a CI tool to install
package dependencies with conda; this capability was brought into
conda through a command called "conda-build-all." The presenter
created the "conda-recipes-scitools" repository to store the recipes
used by conda-build-all. Others followed suit, including
ioos/conda-build and Bioconda. As usage increased, the presenter
proposed the idea of creating a GitHub community where each repository
contained only one recipe (called a "feedstock"). That community is called
"conda-forge."

The presenter has recently written the "conda-smithy" tool that
creates a recipe from a feedstock template and creates the GitHub
repository for the recipe in conda-forge. Anyone can add a new recipe,
and there is an automated system in place using GitHub hooks that
enables this configuration control. Recent additions include a linter
for checking recipe standards. Plans include releasing an installer
for speeding up the build process.

### GT-Py: Accelerating Numpy programs on CPU & GPU with Minimal Programming Effort \[General\]
(Chi-keung Luk, Intel)

> GT-Py is a newly developed just-in-time compiler that can offload
> Numpy code to hardware accelerators with relatively little
> programming effort. It lets programmers add pragmas to a Python
> program to specify what need to be offloaded, without writing the
> actual offloading code. By generating OpenCL code, GT-Py can run on
> a variety of accelerators including GPUs from different vendors,
> multicore CPUs, and potentially FPGAs. Experimental results
> demonstrate that significant performance gains, as much as over
> 9000x faster than the Python interpreter execution, can be obtained
> by adding only a couple of pragmas to the Numpy program. GT-Py
> supports both Python 2.7 and Python 3.4+. It will be available to
> public use for free.

The speaker presented an alternative to Numba/Dask for GPU
programming, specifically for Intel GPUs. He first summarized the
existing methods of improving performance of Python code, which
include compile-time optimization (Cython), JIT optimization (Numba),
and manually writing GPU code using Python wrappers (PyCUDA and
PyOpenCL). For GPU programming, it is difficult and intrusive to
insert into existing code, and requires special knowledge of GPU
programming and the specific hardware on which the code will be run.

GT-Py was written by Intel to specifically address this issue for
Intel GPUs. GT-Py uses `pragma`s similar to OpenMP to mark GPU
sections of code that will be executed on the GPU. the `pragma`s can
be used to target optimization for CPUs as well, both serially and in
parallel. At this time, GT-Py provides `pragma`s for looping and
vectorization, and `pragma`s to replace some common standard library
functions as well. The speaker showed *significant* performance
increase (2–10,000x speedup) even on multi-core CPUs. The first public
release of GT-Py is scheduled for the fall, and will support Intel
Xeon Phi and Altera FPGA GPUs in the future.

[^Central Processing Unit. A CPU, in contrast to a GPU, is a general-purpose hardware device that it commonly used for computations, in addition to standard computer tasks such as running the operating system and productivity applications. It is typically easy to write code for a CPU, and many compilers exist to optimize software for a particular CPU. CPUs today typically include more than one "core," which is the component that performs the computations, and all the cores on a CPU share some portion of a fast memory buffer. Each core can typically run one process at a time, with each process having one or two threads of computation. A single computer may have one (typical) or many CPUs.]

### HoloViews: Let your Data Reveal Itself \[Data Science\]
(Philipp Rudiger, Jean-Luc Stevens, and James A. Bednar, Continuum Analytics)

> Data exploration typically involves code for analyzing and
> transforming a dataset together with separate code used for
> visualization. This back and forth between tools provides a serious
> bottleneck to getting a real grasp of the data. In this talk we will
> demonstrate how the HoloViews library lets you wrap datasets of any
> complexity and size, making the data instantly visualizable in
> Jupyter Notebooks to allow interactive exploration via widgets and
> various plotting backends including Matplotlib and Bokeh.

The presenters lamented that, although most Python visualization
packages generate very nice visualizations, their interfaces require
sometimes many lines of code to use. They wanted a system that would
allow dynamic plotting of data to allow exploration that didn't
require much code to use.

HoloViews is a new Python package that provides such an interface. The
input is relatively simple, allowing for powerful, chained commands
with very little coding. HoloViews allows adding of additional
dimensions to plots by faceting, overlays, dropdowns, sliders, and
combinations thereof by simply chaining commands. It can compare and
combine data inline, and provides interactive inspection in real
time. Additionally, HoloViews allows overlaying of drawings over
plots, while preserving interactivity. HoloViews is only a front-end
to other popular plotting packages, such as Matplotlib and Bokeh, and
these backends can be switched easily. This is useful when publishing
notebooks, as Matplotlib provides support for exporting vector
graphics, while Bokeh excels at interactivity.

### JupyterLab: Building Blocks for Interactive Computing \[Data Science\]
(Brian Granger, Cal Poly State University, Project Jupyter)

> Project Jupyter provides building blocks for interactive and
> exploratory computing. These building blocks make science and data
> science reproducible across over 40 programming language (Python,
> Julia, R, etc.). Central to the project is the Jupyter Notebook, a
> web-based interactive computing platform that allows users to author
> data- and code-driven narratives - computational narratives - that
> combine live code, equations, narrative text, visualizations,
> interactive dashboards and other media.
>
> While the Jupyter Notebook has proved to be an incredibly
> productive way of working with code and data interactively, it is
> helpful to decompose notebooks into more primitive building blocks:
> kernels for code execution, input areas for typing code, markdown
> cells for composing narrative content, output areas for showing
> results, terminals, etc. The fundamental idea of JupyterLab is to
> offer a user interface that allows users to assemble these building
> blocks in different ways to support interactive workflows that
> include, but go far beyond, Jupyter Notebooks.
>
> JupyterLab accomplishes this by providing a modular and extensible
> user interface that exposes these building blocks in the context of
> a powerful work space. Users can arrange multiple notebooks, text
> editors, terminals, output areas, etc. on a single page with
> multiple panels, tabs, splitters, and collapsible sidebars with a
> file browser, command palette and integrated help system. The
> code base and UI of JupyterLab is based on a flexible plugin system
> that makes it easy to extend with new components.
>
> In this talk, we will demonstrate the JupyterLab interface, its
> code base, and describe how it fits within the overall roadmap of the
> project.

The presenter is the lead developer of the Jupyter system. He began by
speaking to the current capabilities of Jupyter and the user
base. Recent additions to the user community includes LIGO, the Laser
Interferometer Gravitational-Wave Observatory, which recently
published its discovery of gravitational waves from colliding black
holes using Jupyter notebooks. Another recent development includes
Binder, which can remotely host and execute Jupyter notebooks using
Docker.

The current capabilities of Jupyter include: a file explorer (the
"tree"), a code editor, a shell extension, and the notebooks. The
developers want to add future capabilities, such as integration with
version control systems, code editing, layout of building blocks, and
debugging. However, with the design of the "notebook" capabilities,
these are not easy to do.

A new project, called JupyterLab, seeks to redesign the Jupyter front
end into a pluggable interface. Under JupyterLab, all the current
features of Jupyter, including notebooks, will be plugins that can be
customized to fit the end users' needs. JupyterLab is the natural
evolution of the notebook, serving as a complete, and completely
customizable, integrated development environment for Python, Julia,
and Ruby.

At this time, JupyterLab has been released in an alpha version. The
developers hope to have a major release before the SciPy 2017
conference.

### Lightning Talks (YouTube)
This session consisted of many short presentations on a variety of
topics, some of which are listed below:

- DataLore from JetBrains: cloud-based interactive data processing;
  conda and GitHub integration; live interactive editing; in private
  beta right now
- Virtual Core from Enthought: interactive volumetric plotting with
  Mayavi
- Voronoi tessellation on large data sets using CGAL, Cython, mpi4py,
  and kd-tree
- Intel Python distribution: accelerated Python using Intel libraries;
  working closely with Continuum Analytics to be Conda compatible
  (Intel channel on anaconda.org); improved performance with MPI4Py,
  PySpark, and PyDAAL
- Steno3D for interactive, web-based 3D concurrent engineering
- HDF5 v10.0: Single Writer/Multiple Reader capability, virtual
  datasets introduced
- Dask can now start iPython on remote workers to inspect and
  manipulate remote data

Friday Sessions
---------------
The following talks were presented at the sessions on Friday,
July 15. For each talk, the title is given, with the focus area in
brackets following the title, and well as the speakers’ names and
affiliations. Additionally, the provided summary of the talk is shown,
along with the attendees’ comments.

### Tell Me Something I Don't Know: Analyzing OkCupid Profiles \[Data Science\]
(Matar Haller, Jaya Narasimhan, and Juan Shishido, University of
California, Berkeley)

> In this talk, we present an approach for combining natural language
> processing with machine learning in order to explore the
> relationship between free text self-descriptions and demographics in
> OkCupid profile data. We discuss feature representation, clustering
> and topic modeling approaches, as well as feature selection and
> modeling strategies. We find that we can predict a user's
> demographic makeup based on their user essays, and we conclude by
> sharing some unexpected insights into deception.

The presenters were interested in analyzing the ways people present
themselves in an online dating context. They looked at both chosen
characteristics (like gender, age, and drug use) and "essay" input,
which involved tokenizing general text and looking for keywords. They
analyzed the essay data based on both lexical analysis and semantic
analysis, which looks for meanings not just words. This presentation
only focused on the semantic analysis.

The presenters used the TF-IDF (term frequency–inverse document
frequency) metric to convert from a word-space to a number-space,
accounting for the occurrence of non-meaningful words. They then
factorized the matrix of TF-IDF data to isolate topics from the data
to categorize the entries into topical categories. They found that
most topics are similarly weighted across demographics, but some can
be very different. One example was the high interest in rock music by
self-identified drug users. They found by visual inspection that it
looked like users who didn't answer the question on drug use were more
likely to use words in their essay entries that were similar to those
used by self-identified drug users. Performing a machine learning
analysis on the data showed that around 50% of users who didn't
identify as drug users wrote in a way very similar to drug users.

### Scaling Up and Out: Programming GPU Clusters with Numba and Dask \[Data Science\]
(Stanley Seibert and Siu Kwan Lam, Continuum Analytics)

> In this talk, we show how Python, Numba, and Dask can be used for
> GPU programming that easily scales from your workstation to a
> cluster, and can be controlled entirely from a Jupyter notebook. We
> will describe how the Numba JIT compiler can be used to create and
> compile GPU calculations entirely from the Python interpreter, and
> how the Dask task scheduling system can be used to farm these
> calculations out to a GPU cluster. Using an image processing example
> application, we will show how these two projects make it easy to
> iterate and experiment with algorithms on large data sets. Finally,
> we will conclude with tips and tricks for working with GPUs and
> distributed computing.

The presenter is the lead developer of the Numba package at Continuum
Analytics. His presentation addressed "scaling up," which he defined
as adding CPUs and GPUs on a single machine using tools such as Cython,
CUDA, and OpenCL, and "scaling out," which he defined as analogous to
distributed computing using tools such as MPI, Hadoop, and Spark.

In order to address single-machine scaling, the speaker presented
Numba, which is a Python package that translates Python code to
machine code at runtime (JIT optimization), for both CPU and GPU
applications. This is done by providing a set of decorators to
indicate which functions to translate and the architectures for which
to compile the code. It also provides a vectorization decorator to
vectorized Numpy universal functions (`ufunc`s). Helper functions also
exist in Numba to assist in programming details that are specific to
GPUs.

For "scaling out," the speaker presented an overview of
[Dask](#dask). He showed a simple example of how to combine delayed
tasks into a graph of an algorithm. Dask recognizes data that should
be shared between functions and reduces them automatically.  Then,
visualization of the generated graph can help in analysis of a
particular algorithm. Converting the algorithm from local execution to
distributed execution then only requires adding two lines of
code. Another benefit of Dask is that it simplifies execution of
workers on multiple GPUs on a single machine.

Finally, the speaker demonstrated an image stitching algorithm that
used Numba and Dask. He stitched an image that was broken into 30
pieces, showing a factor of two speedup when running on two single-CPU
machines versus one machine, and also showed mixed Windows-Linux
execution to demonstrate Dask's ability to schedule on heterogeneous
systems.

### A "BLAS" for Tensors with Portable High Performance \[HPC\]
(Devin Matthews, The University of Texas at Austin)

> Tensor computations are an important kernel in many high-performance
> domains such as quantum chemistry, statistics, machine learning, and
> others. We follow the example of the successful BLAS interface for
> matrix operations in defining a simple, low-level interface for
> tensor contraction and other operations, while providing a
> high-performance implementation using the BLIS framework. In this
> talk, the proposed "BLAS-like" tensor interface is discussed in the
> context of existing tensor and matrix abstractions, and performance
> data for tensor contraction is presented. Our tensor contraction
> implementation achieves similar performance to matrix multiplication
> and does not require any explicit tensor transposition or additional
> workspace, while also incorporating multithreading at several
> levels. These traits make our implementation ideal for layering
> underneath higher-level interfaces such as Numpy.

The speaker presented a brief overview of a BLAS (Basic Linear Algebra
Subsystem), and lamented that, although tensor operations are very
similar to the operations performed in BLAS, there doesn't currently
exist a tensor BLAS that is as optimized as vectors and
matrices. Tensor operations are common in many different engineering
and science disciplines, and applied mathematics. He also spoke to the
user interface for BLAS, which was defined many years ago and
originally written in Fortran 77.

The speaker then pointed out improvements that may be made to the BLAS
interface, and proposed an interface that is more general and optimal
for tensor contractions, his operation of interest. He then
generalized this interface to many other vector, matrix, and tensor
operations. Finally, he introduced the BLIS library, which implements
this interface using low-level, optimized assembly and C/C++ code. His
performance shows comparable performance with Intel-developed
libraries on Intel hardware. This interface is similar to the
interface of the Numpy `einsum` function, which was written for this
specific purpose and could be modified to use this approach under the
hood.

### <a name="peta"/>Launching Python Applications on Peta-scale Massively Parallel Systems \[HPC\]
(Yu Feng, Berkeley Center for Cosmological Physics, Berkeley Institute
for Data Science)

> We introduce a method to launch Python applications at near native
> speed on large high performance computing systems. The python
> runtime and other dependencies are bundled and delivered to
> computing nodes via a broadcast operation. The interpreter is
> instructed to use the local version of the files on the computing
> node, removing the shared file system as a bottleneck during the
> application startup. Our method can be added as a preamble to the
> traditional job script, improving the performance of user
> applications in a non-invasive way. Furthermore, our method allows
> us to implement a three-tier system for the supporting components of
> an application, reducing the overhead of runs during the development
> phase of an application. The method is used for applications on Cray
> XC30 and Cray XT systems up to full machine capability with an
> overhead typically less than 2 minutes. We expect the method to be
> portable to similar applications in Julia or R. We also hope the
> three tier system for the supporting components provides some
> insight for the container-based solutions for launching applications
> in a development environment. We provide the full source code of an
> implementation of the method at
> https://github.com/rainwoodman/python-mpi-bcast. Given that large
> scale Python applications can be launch extremely efficiently on
> state of art supercomputing systems, it is the time for the high
> performance computing community to seriously consider building
> complicated computational applications at large scale with Python.

The presenter works in the astrophysics field and needs to perform
large matrix operations on large datasets. Unfortunately modern
systems such as Hadoop or Spark aren't good at this, but traditional
HPCs are. However, much of his work is migrating to Python and he is
interested in running Python in parallel on large HPCs. The issue with
this is that Python modules are imported by reading files, which are
typically stored on a global shared file system, resulting in
bottlenecks in starting up Python sessions (can take up to one second
for each process serially). The typical solution to this is to bypass
the global filesystem and store Python modules locally using
virtualization or containers. The problem with this is that it is
difficult to maintain and preserve consistency with development
environments.

The presenter's solution was to develop an application that runs in
parallel whose job is to load application bundles on the master
process, broadcast the bundles to the slave nodes, and deploy the
bundles to provide the Python environment locally. This results in
greatly improved startup time for the Python runtime and dependent
modules, starting up hundreds of thousands of Python sessions in a few
minutes.

### SymEngine: A Fast Symbolic Manipulation Library \[General\]
(Ondřej Čertík, Los Alamos National Laboratory, and Isuru Fernando,
Thilina Rathnayake, and Abhinav Agarwal, Indian Institute of
Technology-Kharagpur)

> The goal of SymEngine https://github.com/symengine/symengine is to
> be the fastest C++ symbolic manipulation library (OpenSource or
> commercial), compatible with SymPy, that can be used from many
> languages (Python, Ruby, Julia, etc.). We will present the current
> status of development, how things are implemented internally, why we
> chose C++, benchmarks, and examples of usage from Python (SymPy and
> Sage), Ruby and Julia.

The presenter is the author of SymPy. SymPy can be slow for large or
complicated expressions, so he wrote a library in C++, called
SymEngine, that performs the bulk of the work for expression
simplification, with thin wrappers for Python, Ruby, Julia, and
Haskell. His goal was to be fastest symvolic manipulation library, and
serve as core for SymPy. In developing ths library, the presenter
explored many options to improve performance, but eventually chose
C++. He demonstrated the tool in Python, Ruby, and Julia, all using
Jupyter notebooks with different backends.

SymPy can use SymEngine under the hood now, but not all capabilities
are yet in SymEngine. The expressions can be mixed and SymPy will
still use the Python implementation for capabilities not yet in
SymEngine. The library uses the Trilinos Teuchos library for
reference-counted pointers to prevent memory leaks. He showed
benchmarks against GiNaC, SymPy, *Mathematica* and Maple. The results
showed that SymEngine is not as fast as Maple for polynomials, but
faster for more complex operations; it was signuficantly faster than
*Mathematica* for all benchmarks, and faster than the pure-Python
implementation in SymPy by about 30x.

### Diffing and Merging Jupyter Notebooks with nbdime \[General\]
(Min Ragan-Kelley, IPython/Jupyter, Simula Research Lab)

> Jupyter notebooks are JSON documents containing a combination of
> code, prose, and output. These outputs may be rich media, such as
> HTML or images. The use of JSON and including output can present
> challenges when working with version control systems and code
> review. The JSON structure significantly impedes the readability of
> diffs, and simple line-based merge tools can produce invalid
> results. nbdime aims to provide diff and merge tools specifically
> for notebooks. For diffs, nbdime will show rendered diffs of
> notebooks, so that the content can be compared efficiently, rather
> than the raw JSON. Merges performed with nbdime will guarantee a
> valid notebook as a result, even in the event of conflicts. nbdime
> integrates with existing tools, such as git, so you shouldn't need
> to change how you work. We hope to make the experience of
> collaborating on notebooks less painful and more fun.

Jupyter notebooks contain prose, input, and many types of output, but
under the hood, notebooks are just JSON files. These JSON files store
all information necessary to reconstruct the document. Humans should
be looking at the rendered notebooks, not the JSON files. Differences
between two notebooks are readable, but can be unwieldy and are very
difficult to do with version control systems. GitHub now has notebook
rendering, but not for diffs.

Differencing tools view text files as simply lines and have no
understanding of the file's content. Right now, there are several ways
to attempt to solve this problem: nbconvert can be used to convert the
notebook to Markdown, but it discards all output, which may be of
interest. There are several tools available to help with this (e.g.,
ipymd, notedown, and jsondiffpatch), but they all have drawbacks.

The speaker presented a set of tools he calls nbdime (*N*ote*B*ook
*DI*ff and *ME*rge). These tools can difference and merge notebooks,
and include tools for use on the command line and rendering HTML.
Integration with Git was a primary requirement for the design of the
nbdime toolset. The tool set consists of:

- `nbdiff` for the terminal,
- `nbdiff-web` for HTML output, and
- `git-nbdiffdriver` for Git on the command line.

The speaker demonstrated each tool for the audience by differencing
several types of simple and complex notebooks. The merging capability
is not yet complete; the `nbmergedriver` tool will let Git auto-merge
conflicts in notebooks, but tools for interactive merging are yet to
come. The tools are currently available, but the HTML output still
needs some interface design work. Once the HTML interface is complete,
the Jupyter team will work with GitHub to integrate nbdime into GitHub.

### Lightning Talks (YouTube)
This session consisted of many short presentations on a variety of
topics, some of which are listed below:

- Bandit: security linter for Python
- Wargames: platforms for learning how to hack and practice skills
- CTF (capture the flag) competitions for testing skills
- Mercurial: written in Python, demo of rebasing-like capability,
  concept of draft (rewritable) commits vs. public (non-rewritable)
  commits
- Genapp: tool developed by NIST to assist non computer–scientists in
  creating simple web-based GUIs for collaboration
- anagram.py: uses metaprogramming to determine anagrams on import
- Numpy v1.11 new features
- Tracking thunderstorms in areas with poor radar coverage by tracking
  lightning data
- *Elegant SciPy*: new book that teaches how you use SciPy to write
  elegant scientific software
- Teaser about future Enthought Canopy integration with LabView
- Gadfly: used Pandas and Numba to store and analyze large
  astrophysical datasets
- Python CMake Build System: CMake-based build system for Python
  interpreter
- Generated functions in Python using Numba
- IPyWidgets: interactive widgets in Jupyter notebooks

Birds of a Feather Sessions
===========================
In an effort to increase community building, SciPy emphasizes the
birds of a feather sessions (BoFs) to discuss primary or
tangentially related topics in an interactive setting. These sessions
usually include short presentations by a moderator and panel followed
by an open discussion with everyone in attendance. The BoFs attended
are summarized below.

Distributed Computing BoF (Wednesday)
-------------------------------------
This BoF was attended to gain insight into what parallel programming
paradigms are is use throughout the community, and learn about what
tools are available for those paradigms. The community employs two
types of distributed computing: HPC computing using MPI, and cloud
computing using, primarily, Hadoop or Spark. Both sets of communities,
however, have similar concerns and goals: dealing with large amounts
of data that cannot fit on a single computer, and moving their
computations to that data for efficiency.

HPC systems typically use shared file systems, primarily Lustre, which
come with their own sets of problems (see [this talk](#peta) for an
example). Many of the tools used on these systems also use HDF5 for
parallel file-base input and output. A developer from the HDF Group,
the developers of HDF5, noted that the HDF Group is looking at using
alternatives to file-based storage, including S3 and HDFS, both used
in the cloud computing community.

Most developers at the session use Anaconda for Python package
management. Anaconda seems well-suited to deploying custom
environments on remote machines, and is likely a good candidate to
replace the "wheelhouse" system currently used by Lynx. This would
provide a more maintainable and stable system across all HPCs at NNL
than the current system. Additionally, most of the cloud computing
community uses Docker containers for deployment to remote
machines. Though this approach is very different from the systems used
at NNL, and the Common Environment system currently in development, it
does provide a much more stable and configurable approach to HPC, and
can provide modes across clusters.

Finally, the author of Dask talked about solutions to their customers'
problems. Dask looks like a great system to replace the ZMQ-based
system used by Lynx for job control and scheduling. More on Dask is
presented [elsewhere](#dask) in this trip report.

Matplotlib BoF (Thursday)
-------------------------
- 2.0 beta release out; only change is the default color map, and
  couple bug fixes
  - To get old styles:
	```python
	from matplotlib import style;
    style.use(‘classic’)
	```
  - No way to get old styles globally
- 2.1 will be soon-ish, and will include api changes
  - Traitlets: will allow export to multiple formats (altair
    integration)

Jupyter BoF (Friday)
-------------------
- Around the room with introductions and interests
- Dediated to improving stability for future extensions
- Will make better distinction between public stable APIs and
  non-public APIs
- open to communication wth users via GitHub
- very open to working with new people to develop new capabilities in
  ipython and jupyterlab
- Notes on [Google Docs](http://tinyurl.com/jupyter-bof-2016)
- After JupyterLab, next step is real-time collaboration


Conclusions
===========
- Can we open-source Lynx?
  - Separate subpackages based on capabilities (i.e., configuration
    system, materials, mesh, and coupling; keep nuclear internal?)
  - Extract classified and sensitive (i.e., export controlled) code
    out of system (TRANSX and Bengal)
  - Have internal repo as primary; periodically (patch releases?) push
    updates to GitHub. Fetch updates from GitHub whenever a pull
    request is approved, or daily.
  - Justification: collaboration among peers at other labs, easier
    integration with other scientific packages, presentation to
    outside community and usage by students and others
  - Free developer resource
  - Still able to maintain quality and configuration control
  - Contributions possible remotely by NNL Lynx developers
  - Concerns:
	- Classification: review of all code by ADC before release
	- Information Security: blanket PU approval with manager sign-off?
	- Legal/Licensing: ??? (talk to lawyer)
	- Others?
- Convert to Anaconda for management of software stack
- All presentations are available on
  [Enthought YouTube channel](https://www.youtube.com/playlist?list=PLYx7XA2nY5Gf37zYZMw6OqGFRPjB1jCy6).
- Spark
