
## Unbase - A concept for next generation computing

Daniel Norman  
CTO of güdTECH  
daniel@gudtech.com  
Twitter: @DreamingInCode

---

# Motivation

* We write software for retailers with high order volume, and large warehouses.
* Our customers are totally reliant on us. We are their lifeblood.
* Some use our software nearly 24 hours per day.
* Thousands of cycles per day, per user
* Low application latency is a major part of our value proposition
* Uptime is *critical*

---

# Caution

* I am not a physicist
* I am not a mathematician
* Unbase is at present total vaporware
* This talk may damage your brain

### *You have been warned*

---

# Availability
What does it even mean??

* CAP theorem is undeniably, factually correct, _IF_ you accept Gilbert and Lynch's adorable definitions for C, A, and P

* What exactly is Consistency? (They assume Linearizability)

* How many seconds can you wait before I'm no longer considered [A]vailable?

* If a data packet retransmits after a fiber cut is fixed, was it ever really a Partition? How is this different from congestion, or light travel time?


_See Martin Kleppmann's excellent paper for extra CAP theorem debunkitude_

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


# Option B - Write something new

* Novel engineering efforts are expensive
* Finding bugs in decentralized systems is a big challenge
* 
