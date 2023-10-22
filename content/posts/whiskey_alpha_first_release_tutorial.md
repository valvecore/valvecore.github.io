+++
title = "Whiskey alpha first release tutorial"
url = "/whiskey_alpha_first_release_tutorial"
date = 2023-10-20
+++

{{<rawhtml>}}
<h1>Tutorial for whiskey alpha(First Release)</h1>

<FONT COLOR="#ff0000">Whiskey is still in very early development, there will be several bugs.</FONT>
{{</rawhtml>}}


{{<rawhtml>}}
<h3>Game: Rage Golf</h3>
{{</rawhtml>}}

The first thing you will need to do is download rage golf, and since there is a space in the exe name you will need to rename the exe so that there isnt a space in there.

Then you will need to create a new whiskey project, and example would be...
```
whiskey new_hack --user billy --exe_path /home/billy/RageGolf.exe --name billys_ragegolf_hack
```


The --user argument should be the user you will want to run the exe as. The --exe_path argument should be that path to the rage golf exe, it must be the absolute path.
This will create a folder with the name you supplied in the --name argument. There should be a file inside called main.wisk, this will be the file you will put the python code 
in.

Whats inside the main.wisk file should be similar to this.

```
$set_exe_path /home/billy/RageGolf.exe
$set_byte_order little_endian
$set_user billy



$set_external_script {


attach()

#do stuff here

dettach()

    

}
```

Add this line before the set_external_script command

```
$set_process_name 5000
```

This lengthens how long whiskey will wait for rage golf to start to 5000 miliseconds or 5 seconds.

In this file you will also see the $set_external_script command and the code in the brackets, that is where you will code in python. You will also see the attach() command, that attaches into the process. There is also the dettach() command, that dettaches from the process. During the time you are attached into the process the process will freeze. Do not use any command that will delay the script during that time.

Now, to verify that the whiskey script runs correctly, you do...

```
sudo whiskey run 
```



The rage golf window should have opened and the output should look somthing like this...

```
compiling...
None
./WHISKEY_WINE_DONOTEDIT
finished compiling
running exe
success running exe! pid is 14074
running whiskey python scripts, hit ctrl+c to end it
done running python scripts
```

The part you should look for is the pid, you use that number for other programs to find memory addresses so you can read or write to them with whiskey.




Now, add this before the attach() command...

```
address = hex_to_int( input(">>") )
```

This puts the address from user input into a variable, the hex_to_int command takes a string with an hex and converts it to an int. The input command is a modified version of the default input command in python, unlike the input command in python; you must give it a string.

In between attach() and dettach() you put this code in...

```

print(read_32(address))
write_32(address,10000)
print(read_32(address))

```

The read_32 command returns the 32bit data stored at that address, and write_32 writes a 32bit int to that address. There is a bug with both read_32 and read_64, it will read the wrong value the first time you read. So if that happens do the command twice but print the return from the second one.

You can now run the whiskey project, if it executes correctly you will see something like this...

```
compiling...
None
./WHISKEY_WINE_DONOTEDIT
finished compiling
running exe
success running exe! pid is 14933
running whiskey python scripts, hit ctrl+c to end it
>>
```

And the rage golf window should have opened too, Now press start in the game menu. You will see the sc value in the top left corner, now use the software of your choice to find the address of sc. In my case i will use scanmem.

Now once you have found the address of sc, copy it and input it into the whiskey program. If it has completed sucessfully, you should see something like this...

```
compiling...
None
./WHISKEY_WINE_DONOTEDIT
finished compiling
running exe
success running exe! pid is 16160
running whiskey python scripts, hit ctrl+c to end it
>>a56238
1
10000
done running python scripts
``` 

The sc value should in rage golf should have changed to 10000.

You have completed the tutorial for the first release of whiskey, do note that there are many bugs and many things will change over time. 




