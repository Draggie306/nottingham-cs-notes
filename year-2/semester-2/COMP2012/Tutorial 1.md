2026-02-03

The symbols of a language is an alphabet (ASCII, Unicode): a finite set.

Epsilon: the empty words.  $\epsilon$ We are defining words as lists, so empty words are empty lists.

An automata: a box, with a word as part of an alphabet in it. The output can either be another word, or a binary value (accept / reject ). 

In the halting problem, the input word is a description of an automata, and the output is a yes if it terminated, and no if it does not terminate. However, we do not know if they terminate: some may terminate, others may terminate for some inputs but not others.

For an automata to decide the halting problem if there are 2 conditions: in order to decide a language, it must output a tick every time the word given is in a language (and cross if not). Implicitly, we require it to terminate on all inputs.

