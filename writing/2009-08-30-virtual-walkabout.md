---
layout: page
title: Virtual Walkabout
---

###### 2009 August 31<br>
I have yet to understand the true advantages for using virtual machines for almost everything like some people claim will happen. I know they're useful for temporary testing and some backwards compatibility, but I draw the line there.

That said, when I heard they were trying to implement live migration last summer it didn't strike me as ultimately important, but at least as a very interesting problem to figure out. How DO you take a virtual machine and move it to another host machine WITHOUT the VM noticing? No shut down, reboot, nothing. I eventually decided it just has to be either a push or a pull operation. For a push, you slowly replicate all of the resources to the new machine and then suddenly start executing the process there instead. For a pull, you immediately switch the process over and the minimal resource set, then bring the rest over as needed or is convenient. But I figured this is where the thought would end.

A few weeks ago I saw that they had implemented live migration. I'm rather impressed they pulled it off. The next thought in my head is some lowly virtual machine wandering around a server rack OF ITS OWN VOLITION. Or a data center. Or across the internet. Suddenly we have a key feature for Skynet. A self contained execution unit capable of being moved live anywhere you want it, or anywhere it wants to go. You can't shut it down if you don't know where it is. Creepy.

My next set of ideas were around testing the resiliency of such a migration. Could I take a server rack, write a simple program called Walkabout, and give a VM this wandering behavior, but letting it decide where to go? If the APIs are strait forward, writing a script to do this would be quite easy. Then I thought of the following games:
- Musical chairs - 1 VM per host. Send the VMs migrating in some circular fashion for a random amount of time. When the time expires, shut down one host. The VM on that host is down and out. The game continues.
- [Scotland yard](http://en.wikipedia.org/wiki/Scotland_Yard_(board_game)) - Mr x is a bad guy and wants to get away. You are a pack of detectives trying to find and capture him. There is a fixed cost to move from one node in the graph to another, but some links will take you further than others (taxi, bus, subway, vs switch, subnet, router?). Every five or six turns Mr x's location is shown. Mr x wins if he can survive 20 rounds. I picture this being played in a data center somewhere, either by board IT staff or by people hunting the Skynet AI.
- [Towers of Hanoi](http://en.wikipedia.org/wiki/Towers_of_hanoi) - Starting with three host machines, and host one having x recursively nested VMs on it (H1[VM1[VM2[VM3[VM4]]]]), move all of the machines to host three. The catch? You can only move the 'top' VM, or in other words the VM without any VMs inside of it (VM4 in the previous example).

Unfortunately this last one is not possible as the software doesn't allow for nesting VMs. I understand there are performance reasons not to do this, and possibly hardware reasons, but it does break the VM abstraction model slightly.

One of these days our toys will use us as toys.

<details>
  <summary>Background</summary>
Originally posted at https://tracher.livejournal.com/111385.html.<br/>
<br/>
Now there's a powershell API for this, I might have to try it some day. https://docs.microsoft.com/en-us/powershell/module/failoverclusters/move-clustervirtualmachinerole?view=win10-ps
</details>
