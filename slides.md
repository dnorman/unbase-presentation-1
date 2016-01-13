
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

The most common consistency model implemented by relational databases.

* Determinism via total event ordering
* Sequential numbers
* Easiest way to model causality
* Every RDBMS under the sun uses it

But there's a problem...

---

### Physics

* An up-to-date list is an exclusive resource
* Exclusive resources can only only exist in a single point in space
* Distances between things in space is nonzero!
* Time does not actually exist, only causality
* Light travels at the speed of causality
* No exceptions!

---

### Whoops

Computer scientists like to pretend that space does not exist, and that simultineity is a thing.

* Simultineity does not exist!
* UTC is a convention, it is not simultineity
* Physicists are not optimistic about the invention of an ansible

---

Why do we CS ilk love Linearizability?

 * Easy to reason about
 * Easy to write formal proofs
 * Simplest way to model causality
 * We're lazy - Thinking is hard

But there's another way...

---

# The Dark Side

"Light thinks it travels faster than anything but it is wrong. No matter how fast light travels, it finds the darkness has always got there first, and is waiting for it."  
-Terry Pratchett


---

![Light Cones](World_line.svg)

<p style="font-size:.5em">Of course, it turns out there's actually no such thing as time, or the present.<br>This is a simplified model. Ask a physicist.</p>


---

## The enemy of my enemy

#### Eventual consistency

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
* You get to implement your own consistency model as an overlay
* Your users dislike it when their data is all wunky
* Using a wallclock to resolve conflicts is a recipe for **PAIN**
  <p style="font-size:.5em">*Ahem, Cassandra*</p>

---

### What timezone is it on Mars?

<p style="font-size:.5em">Mars and Earth differ from LA and Chicago only by degree. There is nothing special about being on the surface of earth which magically conjures simultineity.<p>

---

<img src="And-now.jpg" style="border:none">

---

## It's business time

Like it or not, your business is a human/machine hybrid.

* What fraction is machine? <!-- .element: class="fragment" data-fragment-index="1" -->
* What fraction is human?   <!-- .element: class="fragment" data-fragment-index="2" -->
* How much does it cost to train the machines? <!-- .element: class="fragment" data-fragment-index="3" -->
* How much doest it cost to hire and train the humans? <!-- .element: class="fragment" data-fragment-index="4" -->

---

## The gauntlet:
* Deploy the system on six continents <!-- .element: class="fragment" data-fragment-index="1" -->
* Provide nine-nines uptime <!-- .element: class="fragment" data-fragment-index="2" -->
* Provide a screaming fast user experience <!-- .element: class="fragment" data-fragment-index="3" -->
* Save money on staffing <!-- .element: class="fragment" data-fragment-index="4" -->
* Save money on hardware <!-- .element: class="fragment" data-fragment-index="5" -->
* Try to avoid common mode failures <!-- .element: class="fragment" data-fragment-index="6" -->

---

#### Option A - Hire and train a lot of people

* Traditional software design methodology <!-- .element: class="fragment" data-fragment-index="1" -->
* Standard linearizable/serializable RDBMS databases <!-- .element: class="fragment" data-fragment-index="2" -->
* Have humans manage sharding, resource planning, allocation <!-- .element: class="fragment" data-fragment-index="3" -->
* One datacenter per continent <!-- .element: class="fragment" data-fragment-index="4" -->
* Design automated fallback plans - Write loots of code to cope with unpredictable scenarios <!-- .element: class="fragment" data-fragment-index="5" -->
* Design human fallback plans - Who fixes a broken DB, NTP, etc? <!-- .element: class="fragment" data-fragment-index="6" -->
* Hire a large ops team - How many people per continent? <!-- .element: class="fragment" data-fragment-index="7" -->

---

#### Option B - Have the software do the work

* More work up front, but deferred payoff
* Novel engineering efforts are expensive
* Finding bugs in decentralized systems is a big challenge


---

### A self-organizing approach

* No such thing as a "Server" or "Client" <!-- .element: class="fragment" data-fragment-index="1" -->
 * Just big node, little node - Big iron vs iWatch <!-- .element: class="fragment" data-fragment-index="2" -->
 * Just more privileged, or less privileged - Admin vs Subordinate <!-- .element: class="fragment" data-fragment-index="3" -->
 * More memory, or less memory - 1Mb vs 100Tb <!-- .element: class="fragment" data-fragment-index="4" -->
 * More ability, or less ability - x86 vs arm <!-- .element: class="fragment" data-fragment-index="5" -->
* No a priori resource planning ( human or otherwise ) <!-- .element: class="fragment" data-fragment-index="6" -->
* Code is just data <!-- .element: class="fragment" data-fragment-index="7" -->
* All nodes may perform any function of which they are capable. <!-- .element: class="fragment" data-fragment-index="8" -->
* Balancing via back-pressure signals, provided when memory, cpu, or network quotas are near <!-- .element: class="fragment" data-fragment-index="9" -->


---

#### All nodes are equal:
<img src="unbase-model.png" style="width:100%">

---

## Design goals:

* Everything is an immutable message <!-- .element: class="fragment" data-fragment-index="1" -->
* Immutable messages are easy to replicate <!-- .element: class="fragment" data-fragment-index="2" -->
* Only coordinate for actually exclusive resources <!-- .element: class="fragment" data-fragment-index="3" -->
* Project state, don't mutate it <!-- .element: class="fragment" data-fragment-index="4" -->
* Pressurize resources, don't plan them <!-- .element: class="fragment" data-fragment-index="5" -->
* Systematize policy enforcement <!-- .element: class="fragment" data-fragment-index="6" -->
* Locality above centrality <!-- .element: class="fragment" data-fragment-index="7" -->

---

### One possible implementation:

<img src="causality.png" style="width:100%">


---

### Discuss!
