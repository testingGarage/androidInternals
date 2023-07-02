
# Android App Internals - Terminologies



##  Performance Terminologies
1. **Dalvik**
	- It is a discontinued process Virtual Machine (VM) in the Android OS that executes applications written for Android.
	- From Android 5, Dalvik got replaced with ART (Android Runtime)

2. **ART** (Android Runtime)
	-  It is the managed runtime used by applications and some system services on Android
	- As the runtime, it executes the Dalvik executable format and Dex bytecode specification
3. **Garbage Collection**
	- The act of cleaning up data objects that are no longer used so that the memory chunk can be given to new objects.
4. **PSS** (Proportional Set Size)
	-	The total memory used by the app. Total Memory is -- Unique Set Size + % of shared memory.
5. **Private Dirty**
	-	The memory that is stored in the RAM. If it is cleared from RAM, the app has to be rerun for getting data back.
6. **Private Clean**
	-	The memory having items in RAM and as well on the disk of the device. If it is cleared, it can load the data back from the disk
7. **Native Heap**
	-	 It is the memory space available for the virtual machine itself to operate. It is like "Native Heap = Total Memory - Memory Used by Other Apps". Ex: JIT, AoT, Common F/W Classes, Class Loaders, etc.
8. **Dalvik Heap**
	-	The heap space available for a process (for your app's process).
9. **Heap Size**
	 -	The memory available for a virtual machine at run time associated with a process (i.e. to your app only).
10. **Heap Alloc**
	- The amount of memory tracked by Dalvik and the heap allocators. It is always greater than the Total PSS value because a process is forked by Zygote. 
	- This Zygotes includes allocations by our app process with other processes.
11. **App Context**
	-	It returns the context of a single i.e. global object of the current process than the current component i.e. current activity.
12. **Activities**
	 -	In singular it is an Activity. The Activit is an app component that provides a screen that users can use to interact with a specific task. For example, calculation UI in Android.
13. **ViewRootImplm**
	 -	Number of active view roots available for a process. Each view is associated to an Activity i.e. to a screen. Do an Activity has multiple screens opened?
14. **Views**
	 - View is a basic building block for UI components. A View comprises a rectangular area on the screen and it helps in drawing and event handling of UI.
15. **Assets**
	 -	It is a file system which helps helps to have files as text, fonts, music, video, etc.
16. **Local Binders**
	 -	Number of binder opened which is associated to a process (i.e. to your app). Binder inturn is an IPC. 
	 -	Though IPC is never called, internally the app makes use of IPC to communicate. 
	 -	The IPC i.e. communication works with the Intent which is the action to be performed. Each action will have URI and an 'action' to do. Binder will have a binder token which will uniquely identify a binder. A binder token can act as a 'shared token' across multiple processes.
17. **Proxy Binders**
	 -	Number of proxies opened for communication with destined target for a source process (i.e. your application).
18. **Death Recipients**
	 -	An intimation to System i.e. Android System saying that a binded communication is dead and no more available. 
	 -	So, the system will release the accumulated resource on behalf of the binded communication which is no more. This is part of Binder.
19. **OpenSSL Sockets**
	 -	The number of objects opened for the protected layer of communication in the app's context.
20. **GC_For_Alloc**
	 -	The GC is triggered because there is not enough space left in the heap to perform further allocation.
21. **GC_Concurrent**
	 -	It is triggered when the heap has reached a level of objects to collect.
22. **GC_Explicit**
	 -	The GC is asked to collect explicitly and not triggered by high water marks in the heap.
	 -	Frequent call of this indicates, the app or framework used in the app is smart enough to know the space is needed and when a thread is killed."
23. **Concurrent Mark Sweep**
	 -	ART uses CMS as the default GC type
	 -	CMS tries to reduce pause time by doing most of the work concurrently to the application thread
	 -	ART further optimizes using Sticky CMS and Partial CMS
	 -	ART performs heap compaction when the app is moved from background to foreground
24. Background Partial Concurrent Mark Sweep
	 -	It collects all the spaces except for image spaces and zygote spaces
25. Background Sticky Concurrent Mark Sweep
	 -	It is ART's non-moving generational garbage collector
	 -	It scans only the portion of the heap that was modified since the last GC
	 -	It can reclaim only the objects alloted since the last GC
	 -	Since it frees the memory objects allocated since last GC, it is much faster and has less pause time

 
