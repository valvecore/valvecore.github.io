
+++
title = "The Whiskey Project Overview"
url = "/whiskey_project_overview/"
date = 2023-09-19
+++

Whiskey is an easy to learn game hacking utility/software for linux, it uses wine for running windows games and a custom api using ptrace. 
Whiskey is designed for hacking windows games, but development for linux native games is planned.

Whiskey uses python for scripting, an example is...

```
$set_exe_path /home/tony/SortTheCourt.exe

$set_byte_order little_endian

$set_user tony

$set_process_name SortTheCourt.ex

$set_external_script { #you do your python scripting inside of here


address1 = hex_to_int ( input("Address >") ) 
address2 = hex_to_int ( input("Address 2>") ) 
address3 = hex_to_int ( input("Address 3>") )
address4 = hex_to_int ( input("Address 4>") )
attach()

print( read_32(address1) )

write_32(address1,1000000) 
write_32(address2,1000000) 
write_32(address3,1000000) 
write_32(address4,1000000) 
print( read_32(address2) )

dettach()

    

}
```

With ptrace you can read and write to the cpu registers of the game, and change or read its syscalls. This provides a lower level access to the game that other software doesnt provide. It is also planned to add a internal scripting feature, so you could have a more lower level access to the game you are trying to hack. 

The software will be released soon.

