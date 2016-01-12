
### Unbase
#### A concept for next generation computing



Daniel Norman  
CTO of güdTECH  
daniel@gudtech.com  
Twitter: @DreamingInCode

---

## Motivation

* Software for retailers with high order volume - large warehouses.
* Our customers are totally reliant on the system
* Some use our software for 3 shifts - nearly 24 hours per day
* Thousands of cycles per day, per user
* Low application latency is a major part of our value proposition
* Uptime is *critical*

---

# Caution!

* I am not a physicist <!-- .element: class="fragment" data-fragment-index="1" -->
* I am not a mathematician <!-- .element: class="fragment" data-fragment-index="2" -->
* Unbase is presently total vaporware <!-- .element: class="fragment" data-fragment-index="3" -->
* This talk may damage your brain <!-- .element: class="fragment" data-fragment-index="4" -->  
   
   
### *You have been warned* <!-- .element: class="fragment" data-fragment-index="5" -->

---

## Please Wait <!-- .element: class="fragment" data-fragment-index="1" -->

<img src="spinning-wheel.gif" style="border:none;background: transparent">

### Your call will be answered in the order received <!-- .element: class="fragment" data-fragment-index="2" -->

---

###  What the heck does "Availabile" mean?

**CAP theorem is undeniably correct**  <!-- .element: class="fragment" data-fragment-index="1" -->  

...IF you accept Gilbert and Lynch's definitions of C, A, and P  <!-- .element: class="fragment" data-fragment-index="2" -->   

* What exactly is "Consistency"? - They assume Linearizability<!-- .element: class="fragment" data-fragment-index="3" -->
* How long can I make you wait before I'm no longer considered Available? - 30 seconds? 5 minutes? an hour? <!-- .element: class="fragment" data-fragment-index="4" -->
* Retransmit after a fiber cut is fixed, was it really a Partition? <!-- .element: class="fragment" data-fragment-index="5" -->

---

(Check out Martin Kleppmann's excellent paper debunking CAP Theorem)

---

# Most Wanted

Serializability image ( dead or alive )

---

# Serializability

What is Serializability / Linearizability?

"Serializability is the classical concurrency scheme. It ensures that a schedule for executing concurrent transactions is equivalent to one that executes the transactions serially in some order. It assumes that all accesses to the database are done using read and write operations."

Put more simply:   
### An up-to-date list can only only exist in a single point in space.
### No exceptions!

Physicists are not optimistic about the advent of an ansible

---

# The Dark Side

"Light thinks it travels faster than anything but it is wrong. No matter how fast light travels, it finds the darkness has always got there first, and is waiting for it."  
-Terry Pratchett


---

![Light Cones](World_line.svg)

 *Of course, it turns out there's actually no such thing as time, or the present, so this is a simplified model. Ask a physicist.*

 # Why do we CS folk like Serializability?

 * Easy to reason about
 * Easy to write formal proofs
 * We're lazy - Thinking is hard.


---

# The enemy of my enemy

### eventual-consistency alone isn't the solution

##### The good:
* No waiting. Everybody reads and writes as they please.
* Always "Available" because there's no coordination (Shared-nothing)
* Mongo is hip as fuck

##### The bad:
* Stale data is virtually guaranteed
* You get to write your own consistency model as an overlay.
* Your users dislike it when their data is all wunky
* Using a wallclock to resolve conflicts is a recipe for PAIN

---

# What timezone is it on Mars?

* The state of CS, and our poor understanding of time
* Light cones, CRDTs, and Causality (oh my!)
* Business implications of a new approach

---

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
