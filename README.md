About
=====
The libraries were compiled using Visual Studio 2008.
The linking used Multi-threaded DLL (/MD).



The Visual Studio solutions were modified slightly to using the CRT Multi-threaded
DLL and to remove Airpcap and WanAPI from the dependencies.


Packet.lib (packetNtx/Dll/Project/Packet.sln)
=============================================

Use configuration Release
Set configuration win32 or x64

Remove definitions for HAVE_AIRPCAP and HAVE_WANAPI

Under "C++/Code Generation", set Runtime Library to Multi-threaded DLL (/MD)

Under "Linker/Input" remove npptools.lib

Under "C++/Preprocesser", remove definitions for HAVE_AIRPCAP_API and HAVE_WANPACKET_API

Remove WanPacket.cpp from project


wpcap.lib (wpcap/PRJ/wpcap.sln)
===============================


Use configuration "Release - No Airpcap"
Set configuration win32 or x64

Under "C++/Code Generation", set Runtime Library to Multi-threaded DLL (/MD)

Under "C++/Preprocesser", remove definitions for HAVE_SNPRINTF
In wpcap/libpcap/pcap-int.h search for HAVE_SNPRINTF and modify the code to look like:

#if !defined(HAVE_SNPRINTF)
#define snprintf _snprintf
//#define snprintf pcap_snprintf
//extern int snprintf (char *, size_t, const char *, ...);
#endif


Resource file
=============

If there is a compile error for missing header "afxres.h" it might be because
you are using an Express version of Visual Studio or don't have the Windows SDK
installed.  You can replace afxres.h with windws.h:

    -#include "afxres.h"
    +#include "windows.h"

