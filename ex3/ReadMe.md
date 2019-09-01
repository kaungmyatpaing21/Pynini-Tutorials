# String processing with Pynini edit transducers
<a href = "kbg@google.com">Kyle Gorman</a> & <a href = "rws@google.com">Richard Sproat</a>
Google, Inc.
111 8th Ave., New York, NY 10011

String alignment and matching are used in bioinformatics, information retrieval, and natural language processing. For example, RNA and DNA bases are aligned to detect mutations, and string matching is used to detect plagiarism, correct spelling mistakes, and provide "translation memories" to assist human translators. Efficient algorithms exist for these problems, but their implementations tend to be complex and use ad hoc designs, limiting code reuse.

In what follows, we describe a data structure called the edit transducer and show how it can be used for string problems. An edit transducer is an abstract data structure—more specifically, a weighted finite-state transducer (WFST)—which expresses:

the ways in which strings may differ from each other, and
the costs associated with these differences.
An edit transducer and an operation called composition is first used to create a lattice—itself a WFST—aligning pairs of strings. We then use the lattice to compute the Levenshtein distance, a widely-used metric of string similarity, or to build a Levenshtein automaton used to find similar strings.

Our implementation of edit transducers allows users to specify the costs for the various types of edits. For instance, if we're looking for mutations of a gene in a larger genome, we might specify that insertions (i.e, bases present in the genome not matching any of those in the gene) are essentially "free", but deletions (the inverse) have a non-zero cost. Few existing implementations of string algorithms support this. For example, <a href = "https://docs.python.org/2/library/difflib.html#difflib.SequenceMatcher">`difflib`</a>, part of the Python core library, implements the textbook algorithm for computing <a href = "https://en.wikipedia.org/wiki/Levenshtein_distance">Levenshtein distance</a> (Wagner & Fischer 1974), but it only supports fixed edit costs. The same is true of Python implementations of <a href = "https://en.wikipedia.org/wiki/Levenshtein_automaton">Levenshtein automaton</a> (Schulz & Mihov 2002) available <a href = "http://blog.notdot.net/2010/07/Damn-Cool-Algorithms-Levenshtein-Automata">here</a> and <a href = "http://julesjacobs.github.io/2015/06/17/disqus-levenshtein-simple-and-fast.html">here</a>.

Rather than implementing these algorithms from scratch, we use <a href = "http://www.opengrm.org/twiki/bin/view/GRM/Pynini">Pynini</a>, a Python library which uses <a href = "http://www.openfst.org/twiki/bin/view/FST/WebHome">OpenFst</a>, a C++ 11 library for WFSTs, as a backend. Both Pynini and OpenFst were developed at Google for use in speech and language products. These libraries allow us to we delegate the most difficult work to compiled code, carefully tested and extensively optimized, and minimize the risk of programmer error.

In what follows, we provide a brief introduction to finite-state machines (see <a href = "https://www.oreilly.com/ideas/how-to-get-superior-text-processing-in-python-with-pynini">here</a> for a gentler, more detailed introduction). Then, we describe the construction of an edit transducer. Finally, we show how the edit transducer can be used to compute Levenshtein distance and implement Levenshtein automata.

Throughout this tutorial, we apply various optimizations to the WFSTs using the optimize method and functions like prune and synchronize. While this produces smaller, more efficient WFSTs, our motivation is primarily pedagogical: optimized WFSTs are usually easier to read and understand. We reserve general discussion of WFST optimization for future work.
