# database_replication

# 1. Synchronous Replication
Behavior: Every change made to the master is immediately propagated to the slaves. The transaction on the master waits until it is confirmed that the change has been successfully applied to the slaves.
Use Case: Ensures that the master and slaves are always in perfect sync, making it ideal for critical applications requiring high consistency.
Example Systems: Some setups of PostgreSQL with streaming replication, or other databases with strong consistency models.
Tradeoff: Slower write performance because the master waits for slaves to acknowledge.

# 2. Asynchronous Replication
Behavior: Changes made to the master are sent to the slaves, but the master does not wait for confirmation that the slaves have applied the changes. Slaves may lag behind the master if the system is under heavy load or due to network latency.
Use Case: High write performance and tolerates some lag between master and slave. Common in scenarios where read scalability is prioritized.
Example Systems: MySQL replication (default setup), many NoSQL databases like MongoDB.
Tradeoff: Potential for some data loss on slaves if the master fails before changes are replicated.

# 3. Delayed Replication
Behavior: Slaves are configured to deliberately lag behind the master by a specified amount of time (e.g., 5 minutes).
Use Case: Useful as a fail-safe mechanism against accidental or malicious data corruption. If data is deleted or corrupted on the master, the delay gives administrators time to recover the data from the slave before the changes propagate.
Example Systems: MySQL and PostgreSQL both support delayed replication.
Tradeoff: Slaves are not real-time and cannot be used for immediate failover.
