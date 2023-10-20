Shellbags are a set of registry keys that maintain view, icon, position, size, etc. of folders when using Windows Explore  

Shellbag entries are created when a user performs following activities:
- Create a folder  
- Copy a folder  
- Delete a folder  
- Rename a folder  
- Click & right-click a folder

Shellbags can be found in the `NTUSER.dat` and `UserClass.dat` hives:  
```
USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU
USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags
NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU
NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags
```
