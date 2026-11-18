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

Figures -> https://github.com/Tomoki1204/Figures_parallel_extension.git

Figure 1 and 2 are the benchmark results for the parallel extension implementation, and 3 and 4 are the results for the parallel implementation. As the Figure 2 and 4 show, the overall runtime for the extension increases compared to the original version. However, in theory, extension version needs to be faster then the original version. Therefore, it can be concluded that the runtime can be heavily affected by the state of the local machine.
Additionally, the figure 1 looks more stable then the figure 3 because the original parallel implementation allocate a new memory every time, but the extension version does not since it has two whole maps and swap them every time after finishing the calculation.


6. KNOWN LIMITATIONS
--------------------
  - Comparison needed to be run at the same situation and state of the local machine.
