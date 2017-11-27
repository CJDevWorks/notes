- shared libraries have many names - shared libraries, shared objects, dynamic shared objects (DSOs),
dynamically linked libraries (DLLs - if you're coming from a Windows background).

To examine any executable :

$ readelf -h /usr/bin/uptime
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF32
  [...] some header fields
  Entry point address:               0x8048470
  [...] some header fields

As long as the executable needs no shared libraries [3], it needs no relocations.