<h1>PicoCTF: BabyGame3-WriteUp</h1>
<div align="center"> <img src="https://github.com/user-attachments/assets/572bd9fa-1385-4429-9c04-73285da0e0f4" alt="image"></div>
<br>

The provided challenge includes a file that can be downloaded. I used the `wget <urlFile>` utility to download the file and saved it in the desired folder.
![wget file](https://github.com/user-attachments/assets/ff9a28a5-6c5b-40a5-a303-cb276e6140f9)
After checking the file, I tried to change the application policy execution with the command `chmod +x <applicationname>`. By changing this, the application can be run.
and then, when I tried to run the application. The ctf provided a hint, so I tried entering several combinations, such as 'w', 'a', 's', and 'd'. After trying this several times
like this combination that has i created `aaaaaaaaawwwwspaaaaaaaaawwwwspaaaaaaaaawwwwsp`
it shows this result:
![VirtualBox_kali-linux-2024 1-virtualbox-amd64_18_02_2025_21_28_38](https://github.com/user-attachments/assets/05ecd5cd-1480-4402-9316-cdd2495d683e)

After changing that, I used the gdb (GNU debugger) tool to decompile the application. This allowed me to see what functions were used for this application. The GNU debugger shows the 'win()' function, which is clearly useful for handling the application to the final stage that will raise the flag. 
![VirtualBox_kali-linux-2024 1-virtualbox-amd64_18_02_2025_21_33_03](https://github.com/user-attachments/assets/3ae263c4-4949-436f-aa2a-a229b0fdcc7b)
In light of this information, an attempt was made to establish a breakpoint on the win function and execute a jump utilizing the [little-endian principle](https://en.wikipedia.org/wiki/Endianness).
![VirtualBox_kali-linux-2024 1-virtualbox-amd64_18_02_2025_21_35_48](https://github.com/user-attachments/assets/0b89127e-65b6-453a-a8fd-dd051dc24ee3)
After trying this, I tried to enter a payload in the gdb environment with the following results: 
![VirtualBox_kali-linux-2024 1-virtualbox-amd64_18_02_2025_21_37_48](https://github.com/user-attachments/assets/b5f63fe5-0c9c-4ad9-a80f-dc45ed64a2df)
And as seen, the program stops in win, right before making the jump, to run the program outside of gdb. I tried using lab, provided by pico for testing payloads with the following command
`cat final.txt | nc rhea.picoctf.net 62846`
By entering this command, I get a challenge flag, which is:
`picoCTF{gamer_leveluP_334c3e00}`
![VirtualBox_kali-linux-2024 1-virtualbox-amd64_18_02_2025_21_39_51](https://github.com/user-attachments/assets/a8cf22d4-c461-41de-9e2a-4b3f81e6996f)


