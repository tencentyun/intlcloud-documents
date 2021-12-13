## Scenario Description
Reconciliation is an **auxiliary system** required in all billing systems. No matter whether used as a primary or secondary payment system, reconciliation is always necessary during or after payment to ensure billing accuracy. TDMQ for Pulsar can guarantee reconciliation timeliness without affecting the critical path of transactions.

## Problems Encountered

1. **System decoupling**
A transaction involves many systems, which need to be **decoupled** so as not to affect each other.
2. **Time difference of data arrival**
There is a **time difference** of data arrival between systems, so it must be ensured that data arriving at different times can be aggregated.
3. **Data consistency**
In order to eliminate exceptional reconciliation results, it must be ensured that data will never be **lost**.
4. **Cross-region data transfer**
Systems are deployed in different regions, so **cross-region** data transfer is involved.

## Deployment Architecture Diagram
![](https://main.qcloudimg.com/raw/2b9a77de79238d6c72ad4b217f13e42b.png)


## Problem Solving

TDMQ for Pulsar can be used to solve the problems mentioned above.

#### 1. System decoupling

Intuitively, to implement reconciliation between different systems, messages can be reported directly to the reconciliation system for reconciliation processing. However, this causes some new problems; for example, many existing and future systems need to be connected, which is time-consuming and intrusive to the system process in the production environment. Obviously, such a design is very unreasonable. You can adopt TDMQ for Pulsar and connect different systems to it in a unified manner, so that failures in an individual system will not affect other services.

#### 2. Time difference of data arrival

Reconciliation requires the aggregation of data from different systems. Under normal circumstances, the data arrival times of different systems don't differ significantly, but the processes between systems are always sequential; therefore, after the data is delayed for one system, to implement data aggregation, you need to control the data read speed and thus prevent a large amount of data from simply waiting in the reconciliation system. The temporary message storage feature of TDMQ for Pulsar makes it possible that data sent at the same time arrives at different systems generally at the same time.

#### 3. Data consistency

TDMQ for Pulsar provides highly consistent and reliable data storage to ensure that data will never get lost. In addition, it features a high service availability and automatic failover.
   
#### 4. Cross-region data transfer

TDMQ for Pulsar offers two schemes to implement data replication between regions and serves as a real-time data replication channel for the business layer.
- For scenarios where critical data requires cross-region disaster recovery, TDMQ for Pulsar supports cross-region strong sync that distributes messages in different regions.
- For scenarios with low requirements for data consistency, TDMQ for Pulsar provides a cross-region async replication scheme to achieve eventual data consistency in multiple regions.

The two cross-region sync schemes are compared as follows:

| Cross-region Sync Scheme | Production Duration | Disaster Recovery Performance | Storage Costs |
|---------|---------|---------| ---------|
| Cross-region strong consistency | High | High | Low |
| Cross-region eventual consistency | Low | Low | High |

By leveraging TDMQ for Pulsar and real-time computing, you can upgrade daily transaction reconciliation to real-time reconciliation, which allows you to check the transaction accuracy more quickly.
