#!/bin/bash

#script to create web page from markdown
#and automatically add it to the Pi-Display
#10DEC2022 KM4ACK

tmp_dir=$HOME/pi-display/tmp
mkdir -p $tmp_dir

HEADER(){
clear;echo;echo
echo "######################"
echo "# Web page generator #"
echo "######################"
echo
}

FIRST(){
HEADER
echo "Name this file or enter the"
echo "name of a previous file to edit."
echo "Enter \"?\" to see a list of"
echo "previous files."
echo
read -p "Filename? " file
if [ "$file" = '?' ]; then
	CK=$(ls $tmp_dir)
	if [ -z "$CK" ]; then
		HEADER
		echo "no previous files found";echo
		read -n 1 -s -r -p "Press any key to continue"
		FIRST
	else
		HEADER
		echo "File list"
		echo "---------"
		for i in $tmp_dir/*; do
			i=$(echo $i | sed 's/\.tmp//' | awk -F "/" '{print $NF}')
			echo $i
		done
		read -n 1 -s -r -p "Press any key to continue"
		FIRST
	fi
fi
}
FIRST
#remove file name extensions
if echo $file | grep "."; then
	file=$(echo $file | sed 's/\..*//')
fi

#replace spaces with dashes
file=$(echo $file | sed 's/ /-/g')


HEADER
read -p "Header for the page? " header
HEADER
echo "A simple text editor will open."
echo "It supports markdown text"
echo "When done, press ctrl+s to save"
echo "Then ctrl+x to exit"
read -n 1 -s -r -p "Press any key to continue"

nano ${tmp_dir}/${file}.tmp

echo "# $header" > /run/user/$UID/${file}.txt
echo >> /run/user/$UID/${file}.txt
cat ${tmp_dir}/${file}.tmp >> /run/user/$UID/${file}.txt

HEADER
echo "Generating HTML file"
cat /run/user/$UID/${file}.txt | pandoc -s -o /run/user/$UID/${file}.html >/dev/null 2>&1
sed -i "s/title>-/title>${file}/" /run/user/$UID/${file}.html
mv /run/user/$UID/${file}.html $HOME/pi-display/files/
read -p "How many seconds should the page be displayed? " sec
#remove file from links if exist
if grep ${file} $HOME/pi-display/links; then
		sed -i "/${file}/d" $HOME/pi-display/links
fi
echo "${file}.html,${sec}" >> $HOME/pi-display/links
echo "The page will now display for $sec seconds"
echo "This can be changed in $HOME/pi-display/links"
