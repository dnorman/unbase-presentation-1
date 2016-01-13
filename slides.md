
### Unbase

#### A concept for next generation computing
(Database smackdown edition)


Daniel Norman  
CTO of güdTECH  
daniel@gudtech.com  
Twitter: @DreamingInCode

---

## Motivation

* Software for retailers with high order volume, large warehouses.
* Customers totally reliant on the system
* Some use the software for 3 shifts ~ 24 hours per day
* Thousands of cycles per day, per user
* Low application latency is a major part of our value proposition
* Uptime is *critical*

---

# Caution!

* I am not a physicist <!-- .element: class="fragment" data-fragment-index="1" -->
* I am not a mathematician <!-- .element: class="fragment" data-fragment-index="2" -->
* Unbase is presently vaporware <!-- .element: class="fragment" data-fragment-index="3" -->
* This talk may damage your brain <!-- .element: class="fragment" data-fragment-index="4" -->  
   
   
### *You have been warned* <!-- .element: class="fragment" data-fragment-index="5" -->

---

## Please Wait <!-- .element: class="fragment" data-fragment-index="1" -->

<img src="spinning-wheel.gif" style="border:none;background: transparent">

### Your call will be answered in the order received <!-- .element: class="fragment" data-fragment-index="2" -->

---

###  What is Availability?

**Brewer's CAP theorem is undeniably correct**  <!-- .element: class="fragment" data-fragment-index="1" -->  

...IF you accept Gilbert and Lynch's definitions of C, A, and P  <!-- .element: class="fragment" data-fragment-index="2" -->   

* What exactly is "Consistency"? - They assume Linearizability<!-- .element: class="fragment" data-fragment-index="3" -->
* How long can I make you wait before I'm no longer considered Available? - 30 seconds? 5 minutes? an hour? <!-- .element: class="fragment" data-fragment-index="4" -->
* Retransmit after a fiber cut is fixed, was it really a Partition? <!-- .element: class="fragment" data-fragment-index="5" -->

---

#Tsk Tsk

* Brewer called it a theorem long before it was proven.
* Check out Martin Kleppmann's excellent paper debunking CAP theorem

---

## What is Linearizability?

Linearizability / Serializability is the most common consistency model implemented by relational databases.

* Determinism by total order of events
* Sequential numbers
* Easiest way to model causality

But there's a problem...

---

## Physics - Part 1

* An up-to-date list is an exclusive resource
* Exclusive resources can only only exist in a single point in space.
* No exceptions!
* Distances between things is nonzero!

---

## The great disconnect - Part 1

* Computer scientists like to pretend that space does not exist
* Physicists are not optimistic about the invention of an ansible

---

## Why do we CS ilk love Linearizability?

 * Easy to reason about
 * Easy to write formal proofs
 * Simplest way to model causality
 * We're lazy - Thinking is hard

But there's another way...

# The Dark Side

"Light thinks it travels faster than anything but it is wrong. No matter how fast light travels, it finds the darkness has always got there first, and is waiting for it."  
-Terry Pratchett

---

## Physics - Part 2

* There is distance between all stuff
* Time does not exist (only causality)
* _Simultineity does not exist_
** UTC is a convention - not a fact

---

![Light Cones](World_line.svg)

 *Of course, it turns out there's actually no such thing as time, or the present, so this is a simplified model. Ask a physicist.*


---

# The enemy of my enemy

### Eventual consistency

* No coordination (Shared-nothing)
* No freshness guarantees
* Nothing but uptime

---

##### Eventual consistency - The good:
* No waiting. Everybody reads and writes as they please.
* Always "Available" (Shared-nothing)
* Mongo is hip as fuck


---

##### Eventual Consustency - The bad:

* Stale data is virtually guaranteed
* You get to write your own consistency model as an overlay
* Your users dislike it when their data is all wunky
* Using a wallclock to resolve conflicts is a recipe for **PAIN**

---

# What timezone is it on Mars?

* Wallclocks are BAD
* CS does not understand time
* Light cones, CRDTs, and Causality (oh my!)
* Business implications of a new approach

---

# And now, for something completely different

<img src="And-now.jpg" style="border:none">


# A self-organizing approach

* No such thing as a "Server" or "Client"
 * Just big node, little node - Big iron vs iWatch
 * Just more privileged, or less privileged - Admin vs Subordinate
 * More memory, or less memory - 1Mb vs 100Tb
 * More ability, or less ability - x86 vs arm
* Each node is an empty vessel
* No a priori resource planning ( human or otherwise )
* Code is data
* All nodes may perform any function of which they are capable.
* Balancing via back-pressure signals, provided when memory, cpu, or network quotas are near

---
# Business implications

### Like it or not, your system is a human/machine hybrid
You must design your human systems every bit as much as your design your computer systems.


---

# The gauntlet:
* Deploy your system on six continents
* Provide 100% Uptime (even five nines is a huge challenge)  
 *assuming the UI-attached node is working
* Provide a screaming fast user experience


---

# Option A - Hire and train a lot of people

* Use traditional software design methodology
* Employ standard linearizable/serializable RDBMS databases
* Hire humans to manage shards, respond to long term load fluctuation
* Deploy one datacenter per continent
* Design automated fallback plans - Write loots of code to cope with unpredictable scenarios
* Design human fallback plans - Who fixes a broken DB, NTP, etc?
* Hire a large ops team - How many people per continent?


# Option B - Have the software do the work

* Novel engineering efforts are expensive
* Finding bugs in decentralized systems is a big challenge
*



---


* Projection over Mutation
* Pressure over planning
* policy definition/enforcement over implementation ( define it, then enforce the definition, don't define the policy in human systems )
* Capacity over assignment
* locality above centrality
* autonomy over coordination
