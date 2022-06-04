# Useful Ubuntu Commands
This repo contains some useful and repetitive ubuntu commands (especially for data scientists).  

### Find total number of files in a folder and its subfolders:
`find . -type f | wc -l`  
`ls /folder_address/ | wc -l`  
--> [Reference1](https://askubuntu.com/questions/34099/find-number-of-files-in-folder-and-sub-folders)  
--> [Reference2](https://devconnected.com/how-to-count-files-in-directory-on-linux/)  

### Find and count total number of files in particular directory with specific extension and (ends with specific string):  
`find ./ -mindepth 1 -type f -name "*_mono.mp3" -printf x | wc -c`  
