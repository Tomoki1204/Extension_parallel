PARALLEL EXTENSION: <EXTENSION NAME, e.g. Double Buffer memory strategy>
==========================================================================

Authors: <name (username)>, <name (username)>


1. WHAT THIS EXTENSION IS
-------------------------
<1-3 sentences: which extension from the docs this is, and the idea behind it.>
e.g. Workers write their rows directly into one of two boards allocated
once at start-up, instead of allocating a new strip every turn.


2. HOW IT DIFFERS FROM THE PRIMARY IMPLEMENTATION
-------------------------------------------------
Primary (parallel.zip):   <e.g. heap allocation: each worker makes a new
                           strip every turn and sends it back on a channel>
This extension:           <e.g. two boards made once; workers write in place;
                           distributor waits (WaitGroup / done channel), then swaps>

Files changed:
  - <folder/file.go>: <what changed>
  - <folder/file.go>: <what changed>

Synchronisation:
  <How workers and the distributor stay in step, and how races are avoided
   (e.g. each worker writes only its own rows; ticker/'s' copy the board
   under the mutex).>


3. HOW TO BUILD AND RUN
-----------------------
1. Copy the files in this folder into a fresh copy of the skeleton,
   replacing <gol/distributor.go>.
2. From the project root:
     go run .                          (normal run with SDL)
     go test ./tests -v                (all tests)
     go test ./tests -v -race          (race detector)
     go test ./tests -bench . -benchmem   (benchmarks)


4. TESTING
----------
  - All tests pass:            <yes / no, list any failures>
  - Passes with -race:         <yes / no>
  - Tested thread counts:      <e.g. 1-16>


5. RESULTS SUMMARY
------------------
Machine: <CPU model, cores, RAM, OS>
Image / turns: <e.g. 512x512, 1000 turns>

  Threads | Primary time | Extension time | Primary allocs/op | Extension allocs/op
  --------+--------------+----------------+-------------------+--------------------
     1    |              |                |                   |
     2    |              |                |                   |
     4    |              |                |                   |
     8    |              |                |                   |
    16    |              |                |                   |

Key finding: <1-2 sentences, e.g. far fewer allocations and less GC time;
speed-up largest at high thread counts>. Full analysis is in report.pdf,
Section <N>.


6. KNOWN LIMITATIONS
--------------------
  - <e.g. ticker and 's' must copy the board, adding a small cost>
  - <anything not finished or not tested>
