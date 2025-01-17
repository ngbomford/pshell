A tiny Raspberry Pico shell with flash file system, Vi, and C compiler.

[busybox]: https://www.busybox.net
[amacc compiler]: https://github.com/jserv/amacc.git
[c4 virtual machine]: https://github.com/rswier/c4.git
[Squint]: https://github.com/HPCguy/Squint.git

Credit where credit is due...

- The vi code is ported from the [BusyBox] source code.
- The compiler code is a remix of the [amacc compiler] parser generator
and the [c4 virtual machine]. Floating point support was taken fom
the [Squint] project.

Building from source.

```
# NOTE: Requires sdk 1.3 or later
git clone https://github.com/lurk101/pshell.git
cd pshell
git submodule update --init
mkdir build
cd build
cmake ..
make
```

Example log.

```sh
Pico Shell - Copyright (C) 1883 Thomas Edison
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See LICENSE file for details.

console on UART (detected 48 rows, 120 columns)

enter command, hit return for help

/: ls
filesystem is not mounted
/: format
are you sure (y/N) ? n
user cancelled
/: mount 
mounted
/: ls

       9 .exrc
      56 hello.pas

/:             
     cd - change directory
     cp - copy file
 format - format the filesystem
    get - get file (xmodem)
     ls - list directory
  mkdir - create directory
  mount - mount filesystem
     mv - rename file or directory
    put - put file (xmodem)
      q - quit
     rm - remove file or directory
 status - filesystem status
unmount - unmount filesystem
     vi - vi editor

/: mkdir bak
/bak created
/: cp hello.pas bak/save.pas
file /hello.pas copied to /bak/save.pas
/: ls

       0 [bak]
       9 .exrc
      56 hello.pas
                                                                                                                        
/: ls bak                                                                                                               
                                                                                                                        
      56 save.pas                                                                                                       
                                                                                                                        
/: cd bak                                                                                                               
changed to /bak                                                                                                         
/bak: ls                                                                                                                
                                                                                                                        
      56 save.pas                                                                                                       
                                                                                                                        
/bak: ls /                                                                                                              
                                                                                                                        
       0 [bak]                                                                                                          
       9 .exrc                                                                                                          
      56 hello.pas                                                                                                      
                                                                                                                        
/bak: cd                                                                                                                

/: vi hello.pas

... fullscreen VT102/xterm compatible output edited out
                                                                                                                        
/: q                                                                                                                    
                                                                                                                        
done                                                                                                                    
```

