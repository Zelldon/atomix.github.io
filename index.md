---
layout: home
project: atomix
---

<div class="feature intro">
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <p>
Atomix is an event-driven framework for coordinating fault-tolerant distributed systems using a variety of proven distributed systems protocols. It provides the building blocks that solve many common distributed systems problems including cluster management, asynchronous messaging, group membership, leader election, distributed concurrency control, partitioning, and replication.
        </p>
      </div>
    </div>
  </div>
</div>

<!-- Simple -->
<div class="feature gray-background">
  <div class="container">
    <div class="row">

<div class="col-sm-7" markdown="1">
{% include sync-tabs-params.html active="#atomic-value:AtomicValue" inactive="#atomic-counter:AtomicCounter,#atomic-map:AtomicMap,#atomic-multimap:AtomicMultimap,#distributed-set:DistributedSet,#distributed-list:DistributedList,#distributed-queue:DistributedQueue,#work-queue:WorkQueue,#atomic-document-tree:AtomicDocumentTree,#distributed-lock:DistributedLock,#distributed-semaphore:DistributedSemaphore,#leader-election:LeaderElection,#cluster-management:Cluster Management,#direct-messaging:Direct Messaging,#publish-subscribe:Publish-Subscribe" %}
<div class="tab-content" markdown="1">
<div class="tab-pane active" id="atomic-value" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create an AtomicValue
AtomicValue<String> value = atomix.getAtomicValue("value");

// Set the value
value.set("Hello world!");

// Print the current value
System.out.println(value.get());
```
</div>
<div class="tab-pane" id="atomic-counter" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create an AtomicCounter
AtomicCounter counter = atomix.getAtomicCounter("my-counter");

// Increment the counter
long value = counter.incrementAndGet();

// Reset the counter value
counter.set(0);
```
</div>
<div class="tab-pane" id="atomic-map" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Create a cached AtomicMap
AtomicMap<String, String> map = atomix.atomicMapBuilder("my-map")
  .withCacheEnabled()
  .withCacheSize(100)
  .build();

// Set a value in the map
map.put("foo", "Hello world!");

// Read a value from the map
Versioned<String> value = map.get("foo");

// Update the value using an optimistic lock
while (!map.put("foo", "Hello world again!", value.version())) {
  Thread.sleep(10);
}
```
</div>
<div class="tab-pane" id="atomic-multimap" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a multimap
AtomicMultimap<String, String> multimap = atomix.getAtomicMultimap("my-multimap");

// Add a value to a key
multimap.put("foo", "Hello world!");

// Get the values associated with a key
Versioned<Collection<String>> values = multimap.get("foo");
```
</div>
<div class="tab-pane" id="distributed-set" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Create a cached distributed set
DistributedSet<String> set = atomix.setBuilder("my-set")
  .withCacheEnabled()
  .withCacheSize(100)
  .build();

// Add a value to the set
set.add("foo");

// Check a value in the set
if (set.contains("foo")) {
  ...
}
```
</div>
<div class="tab-pane" id="distributed-list" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a distributed list
DistributedList<String> list = atomix.getList("my-list");

// Add a value to the list
list.add("foo");

// Get a value from the list
String foo = list.get(0);

// Stream all values in the list
list.stream().forEach(value -> {
  ...
});
```
</div>
<div class="tab-pane" id="distributed-queue" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a distributed queue
DistributedList<String> queue = atomix.getQueue("my-queue");

// Add a value to the queue
queue.offer("foo");

// Get a value from the queue
String next = queue.poll();

// Stream all values in the queue
queue.stream().forEach(value -> {
  ...
});
```
</div>
<div class="tab-pane" id="work-queue" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();
```
</div>
<div class="tab-pane" id="atomic-document-tree" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();
```
</div>
<div class="tab-pane" id="distributed-lock" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a distributed lock
DistributedLock lock = atomix.getLock("my-lock");

// Acquire the lock
lock.lock();

// Perform some functions and then release the lock
try {
  ...
} finally {
  lock.unlock();
}

// Attempt to acquire the lock until a timeout
lock.lock(Duration.ofSeconds(5));
```
</div>
<div class="tab-pane" id="distributed-semaphore" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a distributed semaphore
DistributedSemaphore semaphore = atomix.getSemaphore("my-semaphore");

// Acquire the semaphore
semaphore.acquire();

try {
  ...
} finally {
  semaphore.release();
}

// Acquire the lock
lock.lock();

// Perform some functions and then release the lock
try {
  ...
} finally {
  lock.unlock();
}

// Attempt to acquire the lock until a timeout
lock.lock(Duration.ofSeconds(5));
```
</div>
<div class="tab-pane" id="leader-election" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get or create a leader election
LeaderElection<MemberId> election = atomix.getLeaderElection("my-election");

// Enter the election
Leadership<MemberId> leadership = election.run(atomix.membershipService().getLocalMember().id());

// Check if the current node is the leader
if (leadership.leader().equals(atomix.membershipService().getLocalMember().id())) {
  System.out.println("I am the leader!");
}

// Listen for changes in leadership
election.addListener(event -> {
  if (event.newLeadership().leader().equals(atomix.membershipService().getLocalMember().id())) {
    System.out.println("I am the leader!");
  }
});
```
</div>
<div class="tab-pane" id="cluster-management" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get a list of members in the cluster
Collection<Node> nodes = atomix.getMembershipService().getNodes();

// Listen for members joining/leaving the cluster
atomix.getMembershipService().addListener(event -> {
  switch (event.type()) {
    case MEMBER_ADDED:
      System.out.println(event.subject().id() + " joined the cluster");
      break;
    case MEMBER_REMOVED:
      System.out.println(event.subject().id() + " left the cluster");
      break;
  }
});
```
</div>
<div class="tab-pane" id="direct-messaging" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get the cluster communication service
ClusterCommunicationService communicationService = atomix.getCommunicationService();

// Register a listener for the "test" subject
communicationService.subscribe("test", message -> {
  System.out.println("Received message " + message);
});

// Send a "test" message to all other nodes
communicationService.broadcast("test", "Hello world!");

// Send a "test" message to node "foo"
communicationService.unicast("test", "Hello world!", atomix.getMembershipService().getNode("foo").id());

// Send a "test" message to node "bar" and wait for a reply
communicationService.send("test", "Hello world!", atomix.getMembershipService().getNode("bar").id())
  .thenAccept(reply -> {
    System.out.println("bar said: " + reply);
  });
```
</div>
<div class="tab-pane" id="publish-subscribe" markdown="1">
```java
// Create an Atomix instance from a HOCON configuration file
Atomix atomix = new Atomix("atomix.conf");

// Start the instance
atomix.start().join();

// Get the cluster event service
ClusterEventService eventService = atomix.getEventService();

// Register a listener for the "test" subject
eventService.subscribe("test", message -> {
  System.out.println("Received message " + message);
});

// Send a "test" message to all other subscribers
eventService.broadcast("test", "Hello world!");

// Send a "test" message to one of the subscribers
eventService.unicast("test", "Hello world!");

// Send a "test" message to one of the subscribers and wait for a reply
eventService.send("test", "Hello world!")
  .thenAccept(reply -> {
    System.out.println("responder said: " + reply);
  });
```
</div>
</div>
</div>
    <div class="col-sm-5 text-right">
      <h2>Simple</h2>
      <p>Atomix provides a collection of dead simple, synchronous and asynchronous APIs for sharing mission critical state, communicating across nodes, and coordinating state changes in distributed systems.</p>
    </div>
    </div>
  </div>
</div>

<!-- Reliable -->
<div class="feature white-background">
  <div class="container">
    <div class="row">
      <div class="col-sm-6">
        <h2>Reliable</h2>
        <p>Atomix features reliable data consistency guarantees backed by a novel implementation of the Raft consensus protocol, allowing it to maintain its guarantees even when machine or network failures occur.</p>
      </div>
      <div class="col-sm-5 text-right">
        <img class="svg" src="/assets/img/icons/reliable.svg">
      </div>
    </div>
  </div>
</div>

<!--Resilient -->
<div class="feature gray-background">
  <div class="container">
    <div class="row">
      <div class="col-sm-5 col-sm-offset-1">
        <img class="svg" src="/assets/img/icons/resilient.svg">
      </div>
      <div class="col-sm-6 text-right">
        <h2>Resilient</h2>
        <p>Atomix clusters are resilient to failure, automatically redistributing state as nodes come and go.</p>
      </div>
    </div>
  </div>
</div>

<!--Scalable -->
<div class="feature white-background">
  <div class="container">
    <div class="row">
      <div class="col-sm-6">
        <h2>Scalable</h2>
        <p>Atomix partitions data to provide the ability to scale data size and throughput without sacrificing consistency guarantees.</p>
      </div>
      <div class="col-sm-5 text-right">
        <img class="svg" src="/assets/img/icons/scalable.svg">
      </div>
    </div>
  </div>
</div>

<!-- Embeddable -->
<!-- <div class="feature gray-background">
  <div class="container">
    <div class="row">
<div class="col-sm-6" markdown="1">
```java
AtomixReplica replica = AtomixReplica.builder(address, members)
  .withTransport(new NettyTransport())
  .withStorage(new Storage(StorageLevel.DISK))
  .build()
  .open()
  .join();
```
</div>
      <div class="col-sm-6 text-right">
        <h2>Embeddable</h2>
        <p>Atomix supports fully embeddable replicas that live in-process, eliminating the need to manage external coordination services.</p>
      </div>
    </div>
  </div>
</div> -->

<!--Learn more -->
<div class="feature get-started">
  <div class="container">
    <div class="row">
      <div class="col-sm-12 text-center">
        <h2>Ready to learn more?</h2>
        <p>
          <a href="/docs/latest/user-manual" class="btn btn-default btn-lg doc-btn">Explore the Docs</a>
        </p>
      </div>
    </div>
  </div>
</div>

<script type='text/javascript'>
// Format tabs
$(function(){
  var $container = $('#sync-tabs');

  updateTabs($container);
  $(window).resize(function(){
    updateTabs($container);
  })

  function updateTabs($tabsContainer){
      var $containerWidth = $tabsContainer.width();
      var tabWidths = [];
      var $tabs = $tabsContainer.find('li');
      $tabs.each(function(index, tab){
        tabWidths.push($(tab).width());
      });

      var formattedTabs = [];
      var maxWidth = $containerWidth;
      var maxWidthSet = false;
      var rowWidth = 0;
      for(var i = tabWidths.length - 1; i >= 0; i--){
          var tabWidth = tabWidths[i];
          if(rowWidth + tabWidth > maxWidth){
            if(!maxWidthSet){
              maxWidth = rowWidth;
              maxWidthSet = true;
            }
            rowWidth = tabWidth;
            formattedTabs.unshift($('<div class="spacer"></div>'));
          }else{
            rowWidth += tabWidth;
          }
          formattedTabs.unshift($tabs.get(i));
      }

      var $tempContainer = $('<div></div>');
      formattedTabs.forEach(function(tab, index){
        $tempContainer.append(tab);
      });
      $tabsContainer.html($tempContainer.html());
  }
});
</script>