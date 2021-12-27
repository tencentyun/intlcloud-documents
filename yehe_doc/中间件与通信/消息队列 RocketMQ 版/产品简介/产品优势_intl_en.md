## Open-Source Component Compatibility

TDMQ for RocketMQ is compatible with open-source RocketMQ 4.3.0 and above and supports access from open-source clients in Java, C, C++, Go, and other programming languages.

## Computing-Storage Separation

The service (broker) and storage (bookie) of TDMQ for RocketMQ are separated from each other. Its overall architecture adopts a stateless cloud native design to natively support on-demand usage and scaling, delivering a more serverless use experience with underlying resources imperceptible to users.

## Resource Isolation

TDMQ for RocketMQ offers a multi-level resource structure that allows for both virtual isolation based on namespace and physical isolation at the cluster level. You may enable namespace-level permission verification to distinguish clients in different environments, which is simple and flexible.

## Segmented Storage

As TDMQ for RocketMQ stores message data as segments, issues like data skew are rare. Rebalancing will not be triggered when nodes are added or deleted due to scaling or server fault, thus avoiding a significant reduction in cluster throughput.

## Rich Diversity of Message Types

TDMQ for RocketMQ supports multiple message types such as general, sequential, delayed, and distributed transaction messages. It also supports message retry and the dead letter mechanism, fully meeting the requirements in various business scenarios.

## High Performance

A single TDMQ for RocketMQ server can sustain a production/consumption throughput of up to 10,000 messages. With the distributed architecture and stateless services, the cluster can be scaled horizontally to increase the cluster throughput.

