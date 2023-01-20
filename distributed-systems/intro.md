### Distributed Systems Conditions
- Should have multiple computers
- They should run concurrently
- They should not share a global clock

Eg. Amazon is a distributed system. But your computer is not as it shares a global clock

## Distributed Storage 
### Read Replication
- A leader database and other databases have copies of the leader
- To change some data the other dbs have to reach outto the leader and the leader prpogates the write to all the dbs
- Based on the fact that reads >>>>> writes: read heavy
- Challenges:
    - Complexity
    - Consistency

### Sharding
![image](https://user-images.githubusercontent.com/54491362/213788700-3e814569-131c-47fb-8a88-bee68d6626e4.png)
- Challenges:
    - Complexity
    - Limited Data models: There should be a field in the db that is there in every query, like the user id
    - Limited data access patterns: Not suitable for OLAP
