# simulate-concurrent-chat-system

💬 Concurrent Chat System Simulation (Clojure)

A Functional Programming–based concurrent chat simulation built using Clojure, demonstrating safe and predictable concurrency through Software Transactional Memory (STM) and Agents (Actor Model).

📌 Project Overview

This project simulates a concurrent chat system where multiple users send messages simultaneously while ensuring:

✅ Data consistency

✅ Thread safety

✅ Race condition prevention

✅ Atomic state transitions

Traditional concurrency often relies on shared mutable state and manual locking mechanisms, which can cause race conditions, deadlocks, and unpredictable behavior.

This implementation avoids those issues by applying Functional Programming (FP) principles, leveraging:

Immutable data structures

Pure functions

Software Transactional Memory (STM)

Agent-based concurrency (Actor Model)

All development and execution were performed inside an Ubuntu Linux Virtual Machine to ensure reproducibility and platform consistency.

🧠 Functional Programming Concepts Applied
1️⃣ Immutability

All data structures in Clojure are immutable by default.

The shared chat log is stored inside a ref:

(def chat-room (ref []))

Each update creates a new version of the vector instead of modifying the existing one.
This prevents data corruption during concurrent execution.

2️⃣ Pure Functions & Referential Transparency
(defn create-message [user text]
  {:user user
   :text text})

Depends only on input parameters

Produces the same output for the same inputs

Has no side effects

This ensures deterministic and predictable behavior.

3️⃣ Software Transactional Memory (STM)
(defn post-message [message]
  (dosync
    (alter chat-room conj message)))

dosync → starts transactional block

alter → safely updates shared state

Automatic retry if conflicts occur

STM guarantees:

Atomicity

Consistency

Isolation

No explicit locks required.

4️⃣ Agents (Actor Model Concurrency)
(def users
  {:alice (agent nil)
   :bob   (agent nil)
   :carol (agent nil)})

Each user is represented by an independent agent.

Agents:

Process messages asynchronously

Execute sequentially per agent

Run concurrently with other agents

Avoid shared mutable state

Messages are dispatched using:

(send (:alice users) send-message "Alice" "Hello everyone!")
🏗️ System Architecture
Component	Purpose
ref	Shared transactional chat log
dosync + alter	Atomic state updates
Pure functions	Deterministic message creation
Agents	Independent concurrent users
send	Asynchronous message dispatch
🖥️ Linux Virtual Machine Setup
Virtualization Platform

Oracle VirtualBox

Linux Distribution

Ubuntu LTS

Verify OS:

lsb_release -a
⚙️ Dependencies
1️⃣ Java Development Kit (JDK)
java -version
2️⃣ Clojure CLI
clojure -Sdescribe

No external libraries were used — only Clojure’s built-in concurrency features.

▶️ Execution Steps
# Create project directory
mkdir ~/clojure_concurrent_chat
cd ~/clojure_concurrent_chat

# Create source file
nano chat_simulation.clj

# Run program
clojure chat_simulation.clj
💻 Example Output
Bob sent: Hi Alice!
Carol sent: Good morning!
Alice sent: Hello everyone!
Bob sent: Doing great!
Alice sent: How are you all?
Carol sent: Let's start the meeting.

Final Chat Log:
Bob : Hi Alice!
Carol : Good morning!
Alice : Hello everyone!
Bob : Doing great!
Carol : Let's start the meeting.
Alice : How are you all?

⚠️ Due to asynchronous execution, message order may vary.
However, the final chat log will always contain all messages safely and correctly.

🧪 Key Learning Outcomes

Functional concurrency design

Eliminating race conditions without locks

Transactional memory management

Actor-based system modeling

Safe parallel system architecture

Linux-based development environment setup

🔐 Why This Approach Is Robust
Traditional Concurrency	This Project
Manual thread handling	High-level concurrency abstractions
Lock-based synchronization	STM transactions
Shared mutable state	Immutable data
Deadlock risk	No explicit locks
Hard to debug	Deterministic & predictable
📈 Scalability & Extensibility

The system can be extended to include:

Message timestamps

Chat rooms with multiple channels

Persistent storage

Real-time UI integration

Distributed actor systems

🎯 Conclusion

This project demonstrates how Functional Programming principles can be applied to build a secure, predictable, and robust concurrent system.

By combining:

Immutability

Pure functions

Software Transactional Memory

Agent-based concurrency

the system successfully avoids common concurrency pitfalls such as race conditions and deadlocks.

The implementation highlights the strength of Clojure’s concurrency model and proves that functional design provides a clean and scalable solution for concurrent system development.

🛠️ Tech Stack

Clojure

Java (JVM)

Ubuntu Linux (VM Environment)

Oracle VirtualBox
