# Useful Ubuntu Commands
This repo contains some useful and repetitive ubuntu commands (especially for data scientists).  

### Find total number of files in a folder and its subfolders:
`find . -type f | wc -l`  
`ls /folder_address/ | wc -l`  
--> [Reference1](https://askubuntu.com/questions/34099/find-number-of-files-in-folder-and-sub-folders)  
--> [Reference2](https://devconnected.com/how-to-count-files-in-directory-on-linux/)  

### Find and count total number of files in particular directory with specific extension and (ends with specific string):  
`find ./ -mindepth 1 -type f -name "*_mono.mp3" -printf x | wc -c`  

### Get list of all files in a folder, and put the output in a file:
`ls -R > output_list_all_files.txt`  
--> [Reference1](https://askubuntu.com/questions/188052/get-a-list-of-all-files-in-folder-and-sub-folder-in-a-file)  

### Get total length of mp3 files in a folder:
`for file in *.mp3; do mp3info -p "%S\n" "$file"; done | paste -sd+ | sed 's+\(.*\)+(\1)/60+' | bc`  
--> above command prints result in `minutes`  
--> [Reference1](https://superuser.com/questions/231950/export-total-length-of-mp3-files-in-a-folder)  
--> [Reference2](https://unix.stackexchange.com/questions/480375/how-to-find-accumulated-duration-on-several-mp3-with-command-line)  

### Get total length of wav files in a folder:
`soxi -D * | awk '{SUM += $1} END { printf "%d:%d:%d\n",SUM/3600,SUM%3600/60,SUM%60}'`  
or  
`ls|grep ".wav"|parallel -j$(nproc) soxi -D {}|awk '{SUM += $1} END { printf "%d:%d:%d\n",SUM/3600,SUM%3600/60,SUM%60}'`  
--> [Reference1](https://www.commandlinefu.com/commands/view/13459/get-the-total-length-of-all-videos-in-the-current-dir-in-hms)  
--> [Reference2](https://unix.stackexchange.com/questions/170961/get-total-duration-of-video-files-in-a-directory)  

### Merge and concat all mp3 & wav files in a folder into a single file via ffmpeg:
`find *.mp3 | sed 's:\ :\\\ :g'| sed 's/^/file /' > fl.txt; ffmpeg -f concat -i fl.txt -c copy output.mp3; rm fl.txt`  
or  
`ffmpeg -f concat -safe 0 -i <( for f in *.wav; do echo "file '$(pwd)/$f'"; done ) output.wav`  
--> [Reference1](https://stackoverflow.com/questions/28922352/how-can-i-merge-all-the-videos-in-a-folder-to-make-a-single-video-file-using-ffm)  
--> [Reference2](https://www.codegrepper.com/code-examples/shell/ffmpeg+merge+two+audio+files)  
--> [Reference3](https://superuser.com/questions/571463/how-do-i-append-a-bunch-of-wav-files-while-retaining-not-zero-padded-numeric)  
--> [Reference4](https://superuser.com/questions/587511/concatenate-multiple-wav-files-using-single-command-without-extra-file)  

### Split an audio file into some equal multiple parts:
`ffmpeg -i input_file.mp3 -f segment -segment_time 3 -c copy out%03d.mp3`  
--> [Reference1](https://unix.stackexchange.com/questions/280767/how-do-i-split-an-audio-file-into-multiple)  

### Split/Segment an audio file from `start_time` to `end_time`:  
`ffmpeg -i input.mp3 -acodec copy -ss START_TIME -to END_TIME output.mp3`  
or  
`ffmpeg -i input.mp3 -ss 1.9 -to 3.5 -c copy output.mp3`  
or for folder based usage of above command, one can use below command:  
`for i in *.mp3; do ffmpeg -i "$i" -ss 0.0 -to 20.0 -c copy "../mp3_files_first_20_seconds/$i"; done`  
--> [Reference1](https://unix.stackexchange.com/questions/280767/how-do-i-split-an-audio-file-into-multiple)  
--> [Reference2](https://askubuntu.com/questions/1264779/how-to-split-an-mp3-file-by-detecting-silent-parts)  

### Convert multiple audio files from `.mp3` to `.wav`:
`for i in *.mp3; do ffmpeg -i "$i" -f wav "${i%}.wav"; done`  
--> [Reference1](https://stackoverflow.com/questions/3255674/convert-audio-files-to-mp3-using-ffmpeg)  

### Convert multiple audio files from `.wav` to `.mp3`:
`for i in *.wav; do ffmpeg -i "$i" -f mp3 "${i%}.mp3"; done`  
--> [Reference1](https://stackoverflow.com/questions/3255674/convert-audio-files-to-mp3-using-ffmpeg)  

### Move (mv) milions of files of folder with extension `.wav` to another folder:
`find . -name '*.wav' | xargs mv --target-directory=/path/to/dest_dir/`  
--> [Reference1](https://tecadmin.net/mv-argument-list-too-long/)  

### Find & count one word or phrase in a txt/csv file ubuntu command:  
`grep "hello" train_data.csv`	--> will just show the results  
`grep -c "hello" train_data.csv`	--> will count number of results  

### List just 10 first files in a folder/directory:
`ls | head -10`  

--> [Reference1](https://www.freecodecamp.org/news/the-linux-ls-command-how-to-list-files-in-a-directory-with-options/) [great refrence for `ls` command]  

### List just 10 last files in a folder/directory:
`ls | tail -10`  

### Find and replace text within a file using commands:
--> Save in-place and replace all the word "original" to "new" word in "predictions_all.json" file.  
`awk '{gsub(/original/,"new phrase")}1' ./input_manifest.json > ./output_manifest.json`  
or  
`sed -i 's/original/new/g' predictions_all.json`  
--> [Reference1](https://askubuntu.com/questions/20414/find-and-replace-text-within-a-file-using-commands)  

### Show specific line of file:
`head -13 file_name | tail +13`  
or  
`sed -n '13p' file.txt`  
or  
`sed -n '20,25p' lines.txt`  
or  
`awk 'NR==5' lines.txt`  
or  
`awk 'NR>=20 && NR<=25' lines.txt`  

--> [Reference1](https://linuxhandbook.com/display-specific-lines/)  
--> [Reference2](https://stackoverflow.com/questions/191364/quick-unix-command-to-display-specific-lines-in-the-middle-of-a-file)  

### Using `ffmpeg` to cut audio file from start to stop time:
`ffmpeg -ss 1 -i input.wav -to 20 -c copy output.wav`  
--> above command, will cut from second 1 to 20.  

--> [Reference1](https://stackoverflow.com/questions/46508055/using-ffmpeg-to-cut-audio-from-to-position)  
--> [Reference2](https://unix.stackexchange.com/questions/182602/trim-audio-file-using-start-and-stop-times)  

### Using `ffmpeg` to convert `stereo` to `mono` audio file:
`ffmpeg -i stereo_input.wav -ac 1 mono_output.wav`  

### Using `ffmpeg` to convert `stereo` to `mono` audio files (convert multiple files in a folder):
`find . -name '*.mp3' -exec ffmpeg -i '{}' -ac 1 'mono_{}' \;
for i in *.mp3; do ffmpeg -i "$i" -ac 1 "./output_folder/$i"; done`  
or  
`find . -name '*.mp3' -exec ffmpeg -i '{}' -ac 1 '{}_mono.mp3' \;
for i in *.wav; do ffmpeg -i "$i" -ac 1 "${i%.*}.wav"; done`  

--> [Reference1](https://stackoverflow.com/questions/39487643/how-to-convert-stereo-sound-to-mono-with-ffmpeg)  
--> [Reference2](https://trac.ffmpeg.org/wiki/AudioChannelManipulation)  
--> [Reference3](https://stackoverflow.com/questions/70698436/how-to-convert-multiple-stereo-audio-files-to-mono-using-ffmpeg)  

