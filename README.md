# Hutton32MRM
Tim Hutton's 32-state cellular automaton is Turing-complete

This repository's `Patterns` folder contains the working components of a Minsky Register Machine<br />
Currently, this only contains the register components. Assembling this into a working machine is currently an exercise 
for the reader

## Description of Hutton's CA
>Motivation: In the original von Neumann transition rules, lines of transmission states can
extend themselves by writing out binary signal trains, e.g. 10000 for extend with a right-directed
ordinary transmission state (OTS). But for construction, a dual-stranded construction arm (c-arm)
is needed, simply because the arm must be retracted after each write. I noticed that there was room
to add the needed write-and-retract operation by modifying the transition rules slightly. This
allows the machine to be greatly reduced in size and speed of replication.<br /><br />Another modification was made when it was noticed that the construction could be made rotationally
invariant simply by basing the orientation of the written cell on the orientation of the one writing
it. Instead of "write an up arrow" we have "turn left". This allows us to spawn offspring in 
different directions and to fill up the space with more and more copies in a manner inspired by
Langton's Loops.<br /><br />
>A single OTS line can now act as a c-arm in any direction. Below are the signal trains:<br />
>100000 : move forward (write an OTS arrow in the same direction)<br />
100010 : turn left<br />
10100  : turn right<br />
100001 : write a forward-directed OTS and retract<br />
100011 : write a left-directed OTS and retract<br />
10011  : write a reverse-directed OTS and retract<br />
10101  : write a right-directed OTS and retract<br />
101101 : write a forward-directed special transmission state (STS) and retract<br />
110001 : write a left-directed STS and retract<br />
110101 : write a reverse-directed STS and retract<br />
111001 : write a right-directed STS and retract<br />
1111   : write a confluent state and retract<br />
101111 : retract<br /><br />
>Achieving these features without adding new states required making some slight changes elsewhere,
though hopefully these don't affect the computation- or construction-universality of the CA. The 
most important effects are listed here:<br />
>1: OTS's cannot destroy STS's. This functionality was used in von Neumann's construction and 
read-write arms but isn't needed for the logic organs, as far as I know. The opposite operation
is still enabled.<br />
>2: STS lines can only construct one cell type: an OTS in the forward direction. Some logic organs
will need to be redesigned.<br /><br />
>Under this modified JvN rule, a self-replicator can be much smaller, consisting only of a tape
contained within a repeater-emitter loop. One early example consisted of 5521 cells in total, and 
replicates in 44,201 timesteps, compared with 8 billion timesteps for the smallest known JvN-32
replicator. This became possible because the construction process runs at the same speed as a moving
signal, allowing the tape to be simply stored in a repeater-emitter loop. The machine simply creates
a loop of the right size (by counting tape circuits) before allowing the tape contents to fill up
their new home.<br /><br />
>The rotational invariance allows the machine to make multiple copies oriented in different directions.
The population growth starts off as exponential but soons slows down as the long tapes obstruct the 
new copies.<br /><br />
>Some context for these modifications to von Neumann's rule table:
Codd simplified vN's CA to a rotationally-invariant 8 states. Langton modified this to make a 
self-replicating repeater-emitter, his 'loops'. Other loops were made by Sayama, Perrier, Tempesti, 
Byl, Chou-Reggia, and others. So there are other CA derived from vN's that support faster replication
than that achieveable here, and some of them retain the computation- and construction-universality
that von Neumann was considering. Our modifications are mostly a historical exploration of the 
possibility space around vN's CA, to explore the questions of why he made the design decisions he did.
In particular, why didn't von Neumann design for a tape loop stored within a repeater-emitter? It would
have made his machine much simpler from the beginning. Why didn't he consider write-and-retraction
instead of designing a complicated c-arm procedure? Of course this is far from criticism of vN - his 
untimely death interrupted his work in this area.<br /><br />
>Some explanation of the details of the modifications is given below:<br />
>The transition rules are as in Nobili32 (or JvN29), except the following:<br />
>1: The end of an OTS wire, when writing a new cell, adopts one of two states: excited OTS and excited
STS, standing for bits 1 and 0 respectively. After writing the cell reverts to being an OTS.<br />
>2: A sensitized cell that is about to revert to an arrow bases its direction upon that of the excited
arrow that is pointing to it. <br />
>3: A TS 'c', with a sensitized state 's' on its output that will become an OTS next (based on the 
state of 'c'), reverts to the ground state if any of 'c's input is 1, else it quiesces. <br />
>4: A TS 'c', with a sensitized state 's' on its output that will become a confluent state next
(based on the state of 'c'), reverts to the first sensitized state S is any of 'c's input is one, 
else it reverts to the ground state.<br />
>5: A TS 'c', with an STS on its output, reverts to the ground state if any of 'c's input is 1.

-- Tim Hutton

## About
Notes:
1. Working out the register was definitely the hardest part

More coming soon!
