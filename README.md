etcd-lock
=========

Distributed lock implementation using etcd

Sample usage
============
```
import ".../utils"

func someFunc() {
  // Create an etcd client and a lock.
  lock, err := utils.NewMaster(utils.NewEtcdRegistry(), "foo", "172.16.1.101", 30)

  // Start a go routine to process events.
  go processEvents(lock.EventsChan())

  // Start the attempt to acquire the lock.
  lock.Start()
}

func processEvents(eventsCh <-chan utils.MasterEvent) {
     for {
        select {
        case e := <-k.eventsCh:
            if e.Type == utils.MasterAdded {
               // Acquired the lock.
            } else if e.Type == utils.MasterDeleted {
               // Lost the lock.
            } else {
               // Lock ownership changed.
            }
        ...
        }
     }
}
```
