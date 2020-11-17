# occamsgametheory
Markov gametheory. Like a recurrent boltzmann neuralnet except all possible lambda func is node and has 1 weight and 1 bit. Set of all possible sets of lambda functions where forall lambda x in set, forall lambda y in set, forall lambda z in set, (λa.λb.λc.a(λm.λn.n)bc)xyz doesnt halt. Will approx sparse navigate this space using an energy func.

"Anything that can happen (any set of axioms which never contradict eachother) did, does, or will happen"  (see farther below). Lets use that.

This kind of math guarantees an evolution selection pressure equal or greater than sexual compared to asexual reproduction, of lambda functions, and that their compute time and memory cost is considered proportionally in their reproductive fitness, and that any existing information or software or thought etc has some possible form.

Gaming-low-lag GPU optimizations (using lazyCL) are planned. In this kind of math, on average for any statement s, which we do not yet know if it is true or false, it is infinitely faster and easier and cheaper to disprove s if s is false than to prove s if s is true, and it is impossible to prove s if s is false and impossible to disprove s if s is true. for every sparse infinite set of lambdas, if it is an "invalid set" then there is always (in the space of all possibilities) at least 1 finite size proof that it is invalid (usually will be astronomically many), and if it is a "valid set" then it usually cant be proven in finite time but imagine it like a million bullets are fired at x from many angles etc, and by chance x happened to be in one of the few rare places that was near the center of all that as the bullets passed by eachother at angles but was not hit, and they keep shooting randomly and in many dimensions and turing complete combos... so any lambda which survives that, we may not know for sure it with the many other lambdas we think are consistent together, dont actually together prove a contradiction, but theres no "friendly fire damage" between sets of 3 lambdas which are consistent together of all possible sets of 3 lambdas in the "valid set", so the gametheory of making such a system work in practice between many computers which dont trust eachother, is for true statements have exponentially more possible states than false statements (in the state space of sets of lambdas) when possible states are weighted by their actual chance of occurring on the internet which derivatives could in theory be derived comparing multiple sets of lambdas together.

/** Similar to a recurrent boltzmann neuralnet except every possible lambda function is a node,
and there is 1 weight per node, and there is 1 bit per node thats like the boltzmann node state
aka is the node/function included or not. You choose weights for some set of functions you are
interested in, and all other weights default to 1 (so your weights would be many times bigger),
and it estimates which set of functions can be included together without any of them contradicting
eachother. Its called a valid set of functions if none of them contradict eachother, else an invalid set.
<br><br>
An object in this system is a mapping of function to complexNumber,
where complexNumber.real is a nonnegative weight (default 1, your chosen weights will normally be many times bigger),
and complexNumber.imaginary is chance that function is included (normally jumps between 0 and 1 like boltzmann neuralnet).
The current occamsfuncer code (2020-11-16+) could easily be modified to generate 256 bit ids for every possible lambda function,
a 1 to 1 mapping between function and id (as long as hash collisions arent found, in practice, but we know pigeonhole)
by defining the universal function (u) as 256 0s and defining a binary forest node's id as sha3_256(concat(left,right)),
where left and right are each such 256 bits. It already has perfect dedup without the ids
but that will change during optimizations where dedup is relaxed to be lazy.
So in that case, an object in this system would be a set of int384 which each have a function id and 2 float64s/doubles.
<br><br>
Foreach validSetOfFuncs in setOfAll_validSetOfFuncs:
	foreach func x in validSetOfFuncs:
		foreach func y in validSetOfFuncs:
			foreach func z in validSetOfFuncs:
				((λa.λb.λc.a(λm.λn.n)bc)xyz) does not halt. //aka (x false y z) does not halt. aka (lispCdr x y z) does not halt.
<br><br>
This precisely defines an infinite set of 3sat constraints on as many bits as possible lambda functions,
where for each 3 funcs (such as x y z, or x y x) either all 8 possibilities are allowed OR only the 7 possibilities !(x&y&z) are allowed.
It only defines 3-way-exclusion-edges and never requires anything be included,
and instead increases score (decreases energy) by summing the weights of the included funcs
and trying to get higher score aka lower energy, similar to a boltzmann neuralnet.
<br><br>
A function in a valid set may contain or be able to derive functions that are not in the set, such as true and false
are probably not in most such sets cuz they were not designed to never halt for any (x_isTrueOrFalse false y z) in the set,
but they could still be inside such wrappers. 
<br><br>
Think of it as each func is an undirectedGraph between every pair of possible funcs,
which it allows that pair to exist in the same set or not (at most 1 of them allowed, either 1),
so the set of all possible functions is actually an undirectedThreeWayGraph aka for every 3 possible functions,
those 3 can exist in the same set or not. Any set which contains all 3 of them is an invalid set
if its some certain 3 where (x false y z) halts, for any order of x y and z including (x false x x) and (x false y x) etc
as there are 27 combos of that for each 3 possible funcs, and if any of those 27 halts then theres a 3-way-exclude-edge
between those 3 funcs. Up to 2 of the funcs can be included even if theres a 3-way-exclude-edge of those 2 funcs and 1 more func.
(x true)->anyFuncYouWantPutHere. (x false) is used in constraints. (x false y z) must not halt (else energy function resists it).
<br><br>
Given a mapping of func to scalar (its weight), occamsgametheory looks for a mapping of func to bit (aka set of funcs)
which minimizes the energy function:
e = -sum(bit(x)*weight(x)) where bit(x) is 1 for funcs in the validSetOfFuncs else 0.
If we view chanceHalts(((λa.λb.λc.a(λm.λn.n)bc)xyz)) as a fraction (0 to 1,
such as sparsely finding any 3 funcs that halt then having to remove any 1 of those to fix the contradiction),
then (TODO...) writing the energy function to combine those few things (chanceHalts, bit*weight, foreach, etc)...
so that bits (or chance func is included vs excluded) can be adjusted approximately and gradually
like a boltzmann neuralnet jumps around similar patterns changing some bits while others tend to stay the same
in some combos.... so that it doesnt have to be completely a validSetOfFuncs but by navigating the
energy function of this sparse turing complete space, can converge toward validSetOfFuncs
and "change the rules of the game" gradually by adding some funcs and removing others,
like a clique (or approx clique) of funcs (with 3-way-constraints) can move like a swarm
where some funcs leave and some funcs join but the swarm itself, which is just a set of facts about math
that dont have execute permission... the swarm can grow into any desired system,
using (x(λm.λn.m)) to store any function in the function x,
compared to (x(λm.λn.n)) is used to check constraints, and that call may use (x(λm.λn.m)) to also
consider the "wrapped function" inside eachother.
For example, ((λg.λh.λi.igh)ab) is a churchEncoding pair of a and b,
and lispCar calls (λm.λn.m) aka true on its param,
and lispCdr calls (λm.λn.n) aka false on its param,
so if you want a function that just stores some literal value v and doesnt make any constraints
then you could use (λg.λh.λi.igh)v(any function that infinite loops for all possible params).
BUT (imagine Murphy's Law in action) if some other function (func santaConstraint) is included which does not allow any 2 functions to exist
where one of them has the literal value "santa claus exists" (func santaTrue)
and the other one has the literal value "santa claus does not exist" (func santaFalse),
then the 3 funcs santaConstraint, santaTrue, and santaFalse cant all exist at once (or are gradually repelled by energy func),
so you can have [santaTrue and santaFalse] or [santaConstraint and santaTrue] or [santaConstraint and santaFalse]
but you cant have  [santaConstraint and santaTrue and santaFalse]
cuz (santaConstraint (λm.λn.n) santaTrue santaFalse) halts, and if it halts fast enough for someone to notice
then they will tend to not share all 3 of those funcs together with others but may share up to any 2 of them.
Similarly, there may be a func that checks if other funcs are checking for constraints about santa
and only allows them if they also give a working physics model of how santa fits down a chimney,
but that would be a very advanced use of this possible system,
and its more likely to be used on things like a set of int64 that are each a 2d voxel
in a 1024x1024 video with 2^32 time steps, in 12 bit color,
so an int64 is time32 y10 x10 red4 green4 blue4,
and if time is in units of microseconds then it can last up to 71 minutes,
or if int128 then we could have 2^64 such sparse videos so store the first int64 as "a namespace"
and second int64 as things in that namespace, or something like that.
For example, a game could be displayed across many computers where constraints are made on sparse combos
of pixels in the (namespace,time,x,y)->color space, and mount a joystick into a certain (namespace,x,y)
as it would have 4096 possible positions per dimension, but for sound you should have at least 16 bits per number,
so maybe this isnt the best way to divide the int64 into a 3d rectangle in time x y value,
and could instead use the low 32 bits as byte[1<<23] so each int reads or writes 1 of about 8 million bytes
as negatives read a byte (after flipping the sign bit) and positives write a byte (time_32 readVsWrite_1 address_23 value_8),
and theres not actually any separate reads and writes since each bit is in 3 possible states by bayes rule: 0, 1, or superposition,
and a bit is in superposition relative to a set of funcs if no constraint prevents 0 and no constraint prevents 1
inside a func which contains such int128 as its wrapped literal
(and would actually be stored in int[] or long[] or byte[] or gpu memory efficiently),
but a problem is you then need at least 2 ints per pixel (for 15 bit color) or 3 ints for 24 bit color.
These kind of details could be worked out within the sets of functions constraining eachother
since a bitstring can be viewed as a lambda function of pairs of pairs of pairs... of true vs false
(padded with true false false false... until the next power of 2 as its a complete binary tree of true and false).
<br><br>
If used like a blockchain (but is a web, not a chain, and doesnt change over time, is just sets of facts of math)...
then its suggested to define weights this way for function x:
(double)(1/sha3_256(id(x))), where salt may be anywhere inside a function if used at all, aka proofOfWork,
such as a 256 bit or 512 bit occamsfuncer id (in progress as of 2020-11-16+,
but the occamsfuncer universal function works, see testcases),
or maybe it should be log of that or log squared? Can experiment with various kinds of gametheory.
<br><br>
If used unlike a blockchain and for fast calculations in a local computer, its suggested to vary the float64/double
weights like you would in a neuralnet, to train it to pattern match sets of functions
and like a boltzmann neuralnet, to fill in the rest of a pattern from a partial pattern aka
to create new functions (already in the set of all possible lambda functions) which match the set of
constraints currently on screen or to remove some of those constraints and add other constraints
that when constraints look at other constraints none of them (or gradually fewer) are observed to be disproven.
If you dont want your constraints getting automatically removed then give them a higher weight.
Functions with lower weight (0 <= weight < infinity, default 1) are more likely to be removed.
Functions with very high weight can still be removed if enough other high weighted funcs fit together
consistently with eachother but not with the fewer funcs that get removed.
<br><br>
A single func keyvalConstraint could be a constraint that some kind of key/value datastruct has at most 1 value per key,
like (pair "abc" "def") and (pair "abc" 42) and keyvalConstraint, could not all 3 exist at once,
but (pair 5 7) could since "abc" does not equal 5 so each can have value independently,
and of course that depends on knowing where in the funcs to look for
such pairs (in (x true) somewhere maybe, for x in a valid set).
<br><br>
How this would be computed sparsely in a p2p network is something like this...
Everyone has this function: (λa.λb.λc.a(λm.λn.n)bc).
Pick 3 functions in the current local set of functions, and call ((λa.λb.λc.a(λm.λn.n)bc) x y z).
If you observe that halts (wait just a short time else give up) then you have to remove x y or z,
so pick one at random, considering their weights. You may add any function back later
to look for other combos that fit together, like maybe you removed z and later remove x and add z back.
Cache some of the sets of 3 funcs so you know those exclusion-triples and can estimate them with GPU.
Even if you give up on or dont notice a bunch of contradictions, the system should be so
redundantly cross-referencing that other constraints will probably exclude those contradictions.
*/
package immutable.occamsgametheory;

...

Like Murphys Law aka "Anything that can go wrong will go wrong", the Mathematical Universe Hypothesis aka https://en.wikipedia.org/wiki/Mathematical_universe_hypothesis approx says "Anything that can happen (any set of axioms which never contradict eachother) did, does, or will happen", but I would add "happens exactly once" in the context of for example a bose condensate is a blob of very cold "particles" (whatever those are) which together have less energy than the powerset of their possible statistically independent actions among eachother (colder things have exponentially less possible states together, see boltzmann math).

In my claims about functions in general, its sometimes important to understand that some lambda functions automatically have a pointer to themself for recursion (specifically in occamsfuncer opcodes numbered 1-7), which is not just a universal lambda function but also a pattern calculus function and quine. In fact, its impossible to create any occamsfuncer halted function which is not a quine aka (L x (R x))->x (and that halts trivially in constant time) for all halted x. In other words, if you are using the occamsfuncer model of computing (which is 1 of infinitely many interchangible models of computing, each able to emulate all the others but often impractically slowly if so), then the fraction of functions shared across the Internet which are quines will certainly be 100% compared to the usual fraction of functions which are quines which is approx .0000000001% or something like that. I interpret this difference between observation and theory of "how great quines are" is mostly the inability of common systems to efficiently process the specifically quine-like properties of quines compared to "mutable spaghetti code" or general disorganization. Its an advanced kind of math.
