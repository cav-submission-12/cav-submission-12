Build Instructions
==================

Install these dependencies:

* pandoc
* ninja-build
* Oracle java 8

Run `./build` to run all tests.
Run `./build t/TEST-NAME.prover.test` to run an individual test.

Repository Layout
=================

 * `matching-logic-prover.md` contains the implementation
 * `direct-proof.md` contains solutions to domain specific queries that 
   can be checked against an SMT solver.
 * The `t/` directory contains a number of tests and experiments, detailed below.

Tests & Experiments
===================

In the `t/` directory, we have a number of tests. Each test consists of a
"claim" (the matching logic pattern that we are trying to prove), and a
strategy. The strategy directs the prover in choosing which axioms to apply. The
`search-bound(N)` strategy causes the prover to begin a bounded depth first
search for a proof of the claim. All lemmas named in the paper except one
(`t/lsegright-list-implies-list`; see below) are proved with a search depth of 5
or lower. The program verification example is proved with a search up to depth
3. In addition, there is an example of a coninductive proof
(`t/zip-zeros-ones-implies-alters.prover`; see below).

The `t/zip-zeros-ones-implies-alters.prover` test proof is at a depth of 17, 
and so we specify the strategy to reduce the search space.
The `t/lsegright-list-implies-list` test needs some help in instantiating
existential variables, which is done by specifying a strategy as a substitution.

Timings
-------

Times as reported by the `time` command. Entries marked with `*` do not peform a search

|   | time (real)|  Test name                                                                             |
|---|------------|----------------------------------------------------------------------------------------|
|   | 0m7.129s   | t/emptyset-implies-isempty.prover                                                      |
|   | 0m10.681s  | t/lsegleft-implies-lsegright.prover                                                    |
|   | 0m10.824s  | t/lsegleft-implies-list.prover                                                         |
|   | 0m9.447s   | t/sortedlist-implies-list.prover                                                       |
|   | 0m9.900s   | t/listSortedLength-implies-listLength.prover                                           |
|   | 0m29.872s  | t/lsegleftsorted-sortedlist-implies-sortedlist.prover                                  |
|   | 0m34.251s  | t/listSegmentRightLength-listSegmentRightLength-implies-listSegmentRightLength.prover  |
|   | 0m8.035s   | t/listSegmentRightLength-appendone-implies-listSegmentRightLength.prover               |
|   | 0m11.871s  | t/lsegright-implies-lsegleft.prover                                                    |
|   | 0m9.479s   | t/listSortedLength-implies-listSorted.prover                                           |
|   | 0m28.582s  | t/dllSegmentLeft-dll-implies-dll.prover                                                |
|   | 0m10.710s  | t/dllSegmentLeftLength-dllLength-implies-dllLength.prover                              |
|   | 0m11.358s  | t/dllSegmentRightLength-dllSegmentRightLength-implies-dllSegmentRightLength.prover     |
|   | 0m29.885s  | t/bst-implies-bt.prover                                                                |
|   | 0m37.980s  | t/avl-implies-bst.prover                                                               |
|   | 0m7.674s   | t/find-before-loop.prover                                                              |
|   | 0m24.454s  | t/find-in-loop.prover                                                                  |
|   | 0m7.563s   | t/sum-to-n.prover                                                                      |
| * | 0m7.791s   | t/lsegright-list-implies-list.prover                                                   |
| * | 0m6.913s   | t/LTL-Ind.prover                                                                       |
| * | 0m8.836s   | t/zip-zeros-ones-implies-alters.prover                                                 |
