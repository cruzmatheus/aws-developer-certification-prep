# EBS Volume - Elastic Block Store Volume

* EC2 loses its root volume (main drive) when it is manually terminated
* EBS Volume is anetwork drive that can be attached in instances while they run
* It allows to persist data
* Not a phisical drive
* Netwotk drive, can have a bit latency
* It's locked to a AZ
* Can be snapshoted and restored into a different AZ
* Billed by what was provisioned, not used

## EBS Volume Types
* GP2 (SSD) - General Purposes
* IO1(SSD) - Highest-performance SSD
* ST1 (HDD) - Low cost HDD for frequently accessed workloads (Throughtput optimized, Streaming)
* SC1 (HDD) - Low cost HDD for less frequently accessed workloads(Throughtput optimized, Streaming)

NOTE: Only GP2 and IO1 can be used as boot volumes

## Instance Store

* A ephemeral storage
* Is physically attached to the machine (EBS is a network driver)

Pros:
* Better IO performance
* Good for buffer, cache, scratch data, temporary content
* Data survives reboot

Cons:
* On stop or termination, the instance store is lost
* Can't resize it
* Backups must be operated by the user