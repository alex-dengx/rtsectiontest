# rtsectiontest
An Attempt to Bypass Memory Scanners By Misusing the ntdll.dll "RT" Section.

The rtsectiontest project attempts to trick (simple) memory/hook scanners by neither leaving any memory protection alternation nor any additional RX/RWX memory, whether the scanners are used on demand or employed inside anti cheat software.
In order to do this, it tries to place the payload code within the last 2 KB of an undocumented section "RT" of ntdll.dll in the VA space of any arbitrary non-protected (yet trusted) process, whose name may be specified in a #define statement.
The "RT" section is 4 KB in size and executable by default.

Moreover, it tries to keep a low profile while attempting to gain trusted process control by letting x64 HIPS only see the occurrence of an NtOpenProcess call.
First time execution of arbitrary code is triggered using syscall stub hijacking in order to then force silent creation of a dedicated payload thread.
Due to the small section size as well as the required bootstrap code, any payload code should fit into 2 KB.