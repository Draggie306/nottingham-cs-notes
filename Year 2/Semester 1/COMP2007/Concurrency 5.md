
> Coursework: Do not add parameters to function specifications. Instead



## The Dining Philosophers Problem, continued

Recap: a semaphore locks the table (`&eating`), and locks the left and right forks (redundant). Then, it eats (`printf()`) and unlocks (`post(&eating)`), allowing the next philosopher to eat.

This is certain/atomic, but not optimal as it locks the *entire* table. This is similar to languages like Python’s interpreter lock.

### Concurrency primitives
“Can semaphore `eating`’s capacity be set to 2 for parallelism?”

In this case, after one philosopher semaphore runs wait(&eating), the semaphore still has a non-zero capacity (and this first philosopher is eating). Then, the next philosopher begins to eat, and runs `wait(&eating)`… but gets stuck as they do not have 2 forks!

> Question: will this still improve parallelism, as do not make naive scheduling assumptions: may the scheduler not just pick one that can have 2 forks?

### Maximum parallelism

A more sophisticated solution: 
- `state[N]`: one state, in THINKING, HUNGRY and EATING
- `phil[N]`: one semaphore per philosopher rather than per fork
	- this blocks if one neighbour is eating
	- the neighbors wake up the philosopher if they have finished eating
- `sync`: one to enforce mutual exclusion of the critical section when updating the states.

![](../../../Pasted%20image%2020251023151439.png)

There is no capacity in the philosopher semaphore at initialisation: they block by default.

- Pointer magic to deduce current ID
- Forever: think, take forks, eat, put forks away.

![](../../../Pasted%20image%2020251023151622.png)

i is the philosopher. Straightforward maths to work out who is on left/right. If the philosopher interested in is hungry, and both the neighbours are not eating (so do not have forks claimed), then post to the philosopher.

!! State change: `state[i]` changes, so may cause a race condition. This means that there should be a semaphore/mutex lock further out, before calling this function. !! 


![](../../../Pasted%20image%2020251023151820.png)

lock: prevents messing with shared state in an uncontrolled manner.

take_forks: locks, set state to hungry. Then tests state: is hungry (yes) and neighbours are hungry: Then allow syncing. Finally, 


put_forks: try to grab the lock, then set to thinking. test(left) and test(right) is like nudging both neighbours, waking them up if they are hungry, then releasing the lock, allowing the next philosopher to repeat this.

Pattern: “eat, nudge immediate neighbours, release”

## The Readers-Writers problem.

Reading data can happen in parallel without problems.

Writing needs mutual exclusion to avoid races. 

The aim is to exploit the ability to have multiple readers to efficiently synchronise access to data.


Solution 1: no parallelism
![](../../../Pasted%20image%2020251023153001.png)


Solution 2 allows parallel reading. A correct implementation requires:
- a counter for the number of readers
	- writers are blocked if there are non-zero `readers`
	- writers rereleasd if there are zero `readers`
	- `readers` must wait if writing.



![](../../../Pasted%20image%2020251023153220.png)

- Lock count mutex.
- First reader to arrive, so check wait and there is nothing.
- Unlock count mutex.
- Do some reading
- Record the number of readers going down, locking and decrementing.
- As we are the last reader, decrement the read counter (now zero) so post to the sync (allowing writer to do stuff)
- Unlock count mutex



`rwSync` is just about coordinating shared state, e.g. both wanting to get into a room.

Writers: shy. Only if the lights are off do they do anything - going in, lights on, writing, then turn lights off. 

Readers: more interesting. If the first reader to arrive - slightly differnt attitude. If the light is off, then go in and turn the light on. If the light is already on, they are more sociable. They won’t go in to the room if there is a writer in, but will go in with other readers. When they leave, they leave, and only the last reader in the room will turn off the light. 

It’s now not hard to imagine how the writers start. 

> It can be hard to think in terms of variables; instead, think in terms of queues (supermarket queues, light switched).


Starvation can still occur if there are too many readers. Even with lots of writers and a fair implementation, readers will still run.









