---
published: true
---
## Introduction
		Introduce concept here
## Laying the groundwork

**Issues**
 
		Talk about issues I came across, listed in my notes.txt
            handle was dropped when calling into_raw()
            shared mem file isn't being deleted at the end of the program due to panic: swapped to nanomsg
            panicking because WSAStartup isn't being called: fixed via ghost bind -- no longer needed due to WSA calls during socket hand off
            hanging on sending/receiving from pipe: had to call dial/listen
            handle table needs duplication: wsaduplicatesocket
            will fail if run as admin for parent
            doesn't handle elevation request being denied
