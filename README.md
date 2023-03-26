# MET

Model Checking-driven Explorative Testing.

## Overview

The **Model Checking-driven Explorative Testing (MET)** framework aims to mix together the advantages of both model checking and testing.

At the model level, developers can specify the target distributed system / protocol using lightweight formal languages like TLA+. The formal specification can be written in an appropriate abstraction level, i.e., it only describes the critical logic that developers care about, and omits other unimportant details. Then, traces can be generated by the supporting model checker tools like TLC efficiently. Integrated by the developers' domain knowledge, state space can be reduced a lot, and subtle deep bugs can be efficiently uncovered during the model checking phase. However, the generated traces are not always convincing because there may exist some discrepancies between the model and the code. This problem can be avoided with the MET framework.

The MET framework will take the model checking-generated traces as test cases, and try to replay these traces at the code level.

Trace replay is non-trivial for distributed systems. Compared to standalone systems, distributed systems may suffer higher uncertainties, like disorders of events on multiple nodes and complex environmental failures (e.g. node crash, network partition, etc).

Through rounds of conformance checking, the test specification is sufficiently accurate and can guide the explorative testing.

## Projects

- **ZooKeeper.** We use RMI and AspectJ to control ZooKeeper, a distributed coordination service, and conduct model checking-driven explorative testing. We intercept events and schedule them according to model-level traces to check if they can be replayed at the code level. We uncovered critical deep bugs in ZooKeeper, such as [ZOOKEEPER-4646](https://issues.apache.org/jira/browse/ZOOKEEPER-4646) and [ZOOKEEPER-4646](https://issues.apache.org/jira/browse/ZOOKEEPER-4646), and replayed subtle bugs like [ZOOKEEPER-3911](https://issues.apache.org/jira/browse/ZOOKEEPER-3911) and [ZOOKEEPER-2845](https://issues.apache.org/jira/browse/ZOOKEEPER-2845).
- **CRDT-Redis.** We implemented several Conflict-Free Replicated Data Types (CRDTs) based on Redis(6.0.5), and tested these CRDTs using MET. The goal of MET is to ensure the correctness of the design and implementation of CRDTs in the system.
- **PySyncObj** and **Redis Raft.** We created a TMET framework to conduct exploratory testing using model checking on two commonly used systems. The framework intercepts syscalls and network transparently, providing deterministic control over the target systems. This allows for deterministic replay of model checking traces, eliminating transcription errors and identifying all invariant violations as bugs in the code. Our testing uncovered and fixed critical bugs in PySyncObj, including issues [#161](https://github.com/bakwc/PySyncObj/pull/161), [#166](https://github.com/bakwc/PySyncObj/issues/166), [#167](https://github.com/bakwc/PySyncObj/issues/167) and [#169](https://github.com/bakwc/PySyncObj/issues/169).

## Links

- ZooKeeper: <https://github.com/Lingzhi-Ouyang/MET>
- CRDT-Redis: <https://github.com/elem-azar-unis/CRDT-Redis/tree/master/MET>
- PySyncObj and Redis Raft: <https://github.com/tangruize/TMET>
