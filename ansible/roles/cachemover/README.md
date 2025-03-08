# Role: cachemover

Installs custom script to move data off cache drive to data pool. Utilizes mover.py from [StuffAnThings](https://github.com/StuffAnThings/qbit_manage/blob/master/scripts/mover.py) to pause torrents with data that will be moved, then resumes them afterwards. Davocache.py script is created that does the moving and preserving hardlinks. Added a healthchecks ping as well. 

This davocache.py script was created by Davo in the TRaSH guides discord. Credit to him. Slightly modified for my own use. 
