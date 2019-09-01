# Pynini

OpenGrm <a href= "http://www.openfst.org/twiki/bin/view/GRM/Pynini">Pynini</a>, like <a href="http://www.openfst.org/twiki/bin/view/GRM/Thrax">Thrax</a>, compiles grammars expressed as strings, regular expressions, and context-dependent rewrite rules into weighted finite-state transducers. It uses the <a href="http://www.openfst.org/twiki/bin/view/FST/WebHome">OpenFst library</a> and its <a href = "https://www.python.org/">Python</a> extension to create, access and manipulate compiled grammars. Pynini is embedded in a Python module, allowing users to write Thrax-like grammars using Python's flexible syntax (including imperative programming constructs not available in Thrax) and powerful toolchain, including an <a href="http://ipython.org/">interactive development</a> ("REPL") environment.


<h3>Note</h3>
Pynini can be used in Text Normalization Problems.This examples only demostrates how to use some build-in functions of pynini and it does not contain any information on how to create the necessary files for using it with a particular language.You should familiar with finite state transducers.Learn about FSTs here <a href = "https://www.youtube.com/channel/UCsg4NhZjN7NZuJIjwea0njw">FST</a>.

<h3>References</h3>
Gorman, K. 2016. Pynini: A Python library weighted finite-state grammar compilation. In Proceedings of the ACL Workshop on Statistical NLP and Weighted Automata, pages 75-80.

Schulz, K., and Mihov, S. 2002. Fast string correction with Levenshtein-automata. International Journal of Document Analysis and Recognition 5(1): 67-85.

Wagner, R. A., and Fischer, M. J. 1974. The string-to-string correction problem. Journal of the ACM 21(1): 168-173.
