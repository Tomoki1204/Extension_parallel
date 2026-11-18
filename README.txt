PARALLEL EXTENSION
==========================================================================

Authors: Tomoki Hara: Tomoki1204


1. WHAT THIS EXTENSION IS
-------------------------
For the approach 2, two separated map are created at the beginning of the cumputation, and when the workers finish calculating they write down the results directly on the other map.
[step3 explanation]

2. HOW IT DIFFERS FROM THE PRIMARY IMPLEMENTATION
-------------------------------------------------
Primary (parallel.zip):   heap allocation: each worker makes a new strip every turn and sends it back on a channel.
This extension:           two boards made once -> workers write in place -> then swaps -> going back to the first step

3. TESTING
----------
  - All tests pass:            yes
  - Passes with -race:         yes
  - Tested thread counts:      1-16


4. RESULTS SUMMARY
------------------
Machine: M2 chip MacBook: an 8-core CPU (4 performance + 4 efficiency)
Image / turns: 512x512, 1000 turns





Key finding: <1-2 sentences, e.g. far fewer allocations and less GC time;
speed-up largest at high thread counts>. Full analysis is in report.pdf,
Section <N>.


6. KNOWN LIMITATIONS
--------------------
  - <e.g. ticker and 's' must copy the board, adding a small cost>
  - <anything not finished or not tested>
