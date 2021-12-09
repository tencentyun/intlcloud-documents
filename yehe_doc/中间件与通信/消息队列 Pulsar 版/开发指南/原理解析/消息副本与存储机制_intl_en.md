## Message Metadata Composition

In Pulsar, the message data in each partitioned topic is stored in the form of ledger on bookie storage nodes in the BookKeeper cluster. Each ledger contains a set of entries, and bookies write, find, and get data only by entry.

>?In case of batch message production, one entry may contain multiple messages, so the entries do not necessarily correspond to messages one by one.

Ledgers and entries correspond to different metadata respectively.

- The metadata of ledgers is stored in ZooKeeper.
- In addition to message data, entries also contain metadata. The data of entries is stored on the bookie nodes.

![](https://main.qcloudimg.com/raw/fee2f4130655c879d9cf47d084e76d8e.png)

<table>
<tr>
<th>Type</th>
<th>Parameter</th>
<th>Description</th>
<th>Data Storage Location</th>
</tr>
<tr>
<td rowspan="4">Ledger</td>
<td>ensemble size (E)</td>
<td>Number of bookie nodes selected by each ledger</td>
<td rowspan="4">Metadata is stored in ZooKeeper</td>
</tr>
<tr>
<td>write quorum size (Qw)</td>
<td>Number of bookies to which each entry needs to send write requests</td>
</tr>
<tr>
<td>ack quorum size (Qa)</td>
<td>Number of write acks that should be received before a write can be considered successful</td>
</tr>
<tr>
<td>Ensembles (E)</td>
<td>The ensemble list used in the format of &lt;entry id,="" ensembles=""&gt; tuple <li>key (entry ID): the entry ID at the start of the ensemble list</li><li>value (ensembles): the list of IPs of the bookies selected by the ledger. Each value contains E IPs</li>Each ledger may contain multiple ensemble lists and can have at most one ensemble list in use at any time</td>
</tr>
<tr>
<td rowspan="4">Entry</td>
<td>Ledger ID</td>
<td>ID of the ledger of the entry</td>
<td rowspan="4">Data is stored on bookie nodes</td>
</tr>
<tr>
<td>Entry ID</td>
<td>ID of the current entry</td>
</tr>
<tr>
<td>Last Add Confirmed</td>
<td>Entry ID of the known latest write ack when the current entry is created</td>
</tr>
<tr>
<td>Digest</td>
<td>CRC</td>
</tr>
</table>


During the creation of each ledger, E bookie nodes will be selected from the list of existing candidate bookie nodes in writable status in the BookKeeper cluster. If there are not enough candidate nodes, the `BKNotEnoughBookiesExceptio` exception will be thrown. After the candidate nodes are selected, this information will be combined to form the &lt;entry id, ensembles&gt; tuple and stored in ensembles of the ledger's metadata.

## Message Replica Mechanism

**Message write process**

![](https://main.qcloudimg.com/raw/d656e1820506959959b6902b283d34dc.png)

When the client writes a message, each entry will send a write request to Qw bookie nodes in the ensemble list currently used by the ledger. After Qa write acks are received, the current message will be considered written and stored successfully, and LAP (lastAddPushed) and LAC (LastAddConfirmed) will be used to mark the position currently pushed and the position where the storage ack is received respectively.

The value of the LAC metadata in each entry being pushed is the position value of the last received ack when an entry sending request is created at the current moment. The position of LAC and preceding messages are visible to the read client.

In addition, Pulsar uses the fencing mechanism to prevent multiple clients from writing to the same ledger at the same time. This is suitable for scenarios where the ownership of one topic/partition is transferred from one broker to another.

**Message replica distribution**

When each entry is written, the set of Qw bookie nodes in the ensemble list with which the current entry needs to be written will be determined based on the entry ID of the current message and the entry ID at the start of the currently used ensemble list (key value). Then, the broker will send a write request to these bookie nodes. After Qa write acks are received, the current message will be considered written and stored successfully. At this point, Qa message replicas can be guaranteed at the least.

![](https://main.qcloudimg.com/raw/0fe7cafe153a9042051a712f0437fc26.png)

As shown above, the ledger selects 4 bookie nodes (bookies 1–4), a message is written to 3 nodes each time, and after 2 write acks are received, the message will be considered stored successfully. The ensemble selected by the current ledger uses bookies 1, 2, and 3 to write entry 1 and uses bookies 2, 3, and 4 to write entry 2, and entry 3 will be written to bookies 3, 4, and 1 according to the calculation result.



## Message Recovery Mechanism

By default, each bookie in a Pulsar BookKeeper cluster is started with the recovery service enabled automatically, which performs the following tasks:

1. Auditor election (by AuditorElector).
2. Task replication (by ReplicationWorker).
3. Failure monitoring (by DeathWatcher).

Bookie nodes in a BookKeeper cluster will elect a master bookie through ZooKeeper's temporary node mechanism, which mainly performs the following tasks:

1. Monitor changes in bookie nodes.
2. Mark the ledgers on failed bookies in ZooKeeper `Underreplicated`.
3. Check the number of replicas of all ledgers (the default cycle is one week).
4. Check the number of replicas of entries (not enabled by default).

The data in a ledger is recovered by fragment (each fragment corresponds to a set of ensemble lists in the ledger; if there are multiple lists, multiple fragments need to be processed).

To perform recovery, the first step is to determine which storage nodes in which fragments of the current ledger need to be replaced with new candidate nodes for data recovery. If there is no entry data on an associated bookie node in a fragment (determined based on whether the entries at the start and end exist by default), the bookie node needs to be replaced, and the fragment requires data recovery.

After the data in the fragment is recovered with the new bookie node, the original data of the ensemble list in the current fragment will be updated in the metadata of the ledger.

In scenarios where the number of data replicas is reduced by failures of bookie nodes, after this process is completed, the number will be gradually restored to Qw (i.e., the number of replicas specified on the backend, which is 3 in TDMQ by default).
