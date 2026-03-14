# Setting the DAK and NMK with hpavkey

Creating the Device Access Key (DAK) and Network Membership Key (NMK) from a password or passphrase used by the powerline adapters is performed using a program called hpavkey.

You will only see or be able to set the DAK when plugged directly into the powerline adapter, all other times the DAK will show as ```DAK 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 (none/secret)``` in output.

Now there is some debate if you have to use this hpavkey program to convert the password or passphrase into a hexadecimal number for the ```.pib``` file because as long as the DAK hexadecimal number is unique for each powerline adapter and the NMK hexadecimal number is the same on each powerline adapter thats to be in a powerline network group, then is there a need for this program? Why not just create an appropriately long random hexadecimal number for the DAK and NMK? You can!

Hpavkey will take a variable length password or pass phrase and convert it into a fixed length hexadecimal key ready to add to the firmware ```.pib``` file.

```
.\hpavkey --help
```

### Push Button Pairing

The documentation says if you want to disable the powerline button so it cant be used to pair or reset the powerline adapter use this -L switch. Thats a handy feature for people with young kids around exploring the world and like to push buttons.

However in practice this option does not appear to work as we can see where the output remains the same for the DAK and NMK and I would expect a difference in the output. So probably best to use this -L switch in the program ModPib which we will use later in this process.
```
.\hapavkey -L [Security Level (button pairing & Reset), 0 is enabled, 1 is disabled]
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L1 -D HomePlugAV
689F074B8B0275A2710B0B5779AD1630
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L0 -D HomePlugAV
689F074B8B0275A2710B0B5779AD1630
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L0 -M HomePlugAV
50D3E4933F855B7040784DF815AA8DB7
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L1 -M HomePlugAV
50D3E4933F855B7040784DF815AA8DB7
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 1 -M HomePlugAV
50D3E4933F855B7040784DF815AA8DB7
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 0 -M HomePlugAV
50D3E4933F855B7040784DF815AA8DB7
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 1 -D HomePlugAV
689F074B8B0275A2710B0B5779AD1630
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 0 -D HomePlugAV
689F074B8B0275A2710B0B5779AD1630
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 0 -e -D "1 Much Longer Password!"
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -L 1 -e -D "1 Much Longer Password!"
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -D "1 Much Longer Password!" -e -L 0
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -D "1 Much Longer Password!" -e -L 1
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -D "1 Much Longer Password!" -e -L1
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -D "1 Much Longer Password!" -e -L0
5BAA38E36AFBD2AA7BA4F23861A9311D
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Device Access Key (DAK)

Its reported in the documentation that the DAK needs to be unique for each powerline adapter. Its supposed to be a unique static identifier which is used to authenticate and encrypt the sharing of the powerline adapters network main encryption key, the NMK.

Sometimes the DAK is derived from the powerline MAC ID, but doesnt have to be. During the pairing process, a Temporary Encryption Key (TEK) is generated and encrypted using the DAK to send the actual network password (NMK) to the new device safely.

```
.\hapavkey -D [Variable length password or pass phrase]

.\hapavkey -D HomePlugAV
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -D HomePlugAV
689F074B8B0275A2710B0B5779AD1630
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```

### Network Membership Key (NMK)

The NMK is the main encryption key used for sharing data amongst the powerline adapters.

Option -e enforces the Homeplug AV length and content rules which is:

The passphrase needs to be between 12 and 64 characters.

The passphrase must consist of 7-bit ASCII characters in the range 0x20 Hex aka 32 Decimal aka the Space character through to 0x7F Hex aka 127 Decimal aka the Delete character.

An ASCII table can be seen here https://commons.wikimedia.org/wiki/File:ASCII-Table-wide.svg

Whilst option -e is handy for enforcing minimum length passwords or pass phrases, because short passwords or pass phrases are always easier to brute force crack with a hacking program cycling through every combination, does the ASCII range restriction of only being able to use characters from 32 to 127 ie 63 different characters or combinations, also present a restriction making things easier to brute force crack? 

There's a couple points here at play, the first is the length of the password the other is the range. Put another way, if you used 100 characters that can only be the character 1 or 0, ie binary, that doesnt create many permutations to try again making it easy to brute force crack. But if you had 100 characters and each character or symbol could be from a range that is 150 different types of symbols, the number of permutations go up enormously. This then becomes harder to brute force crack. So in the scheme of things, being restricted to 63 combinations of symbols isnt much, its still enough to waste some hackers time. 

Its the key which is the weakspot and the slight of hand. Its a fixed length of 16bytes of 16 symbols which has far less permutations making things faster to brute force crack. In theory thats 2^128 possible combinations with experts reckoning this can take billions of years to crack in a best case situation, but as always the devil is in the detail... and dont think Wifi is any safer either, because decryption techniques used during WW2 can be effective in reducing this time, which might be discussed later on in this repo. Its not decided yet because it can be likened to arguing about theoretical things, like the existence of God.

And after all that, is it any better than just picking a bunch of random hexadecimal numbers?

```
.\hpavkey -e [Enforce password rules] -M [Variable length password or pass phrase]

.\hpavkey -M HomePlugAV
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -M HomePlugAV
50D3E4933F855B7040784DF815AA8DB7
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -e -M HomePlugAV
hpavkey.exe: Phrase "HomePlugAV" less than 12 characters: not supported
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>

.\hpavkey -e -M "1 Much Longer Password!"
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs> .\hpavkey -e -M "1 Much Longer Password!"
1D7441BBFA2ABF988DF89B8412124179
PS C:\Users\admin1\source\repos\open-plc-utils\VisualStudioNET\Programs>
```
