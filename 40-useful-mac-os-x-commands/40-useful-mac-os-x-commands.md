40 Useful Mac OS X Shell Scripts and Terminal Commands
Here are a bunch of Mac OS X terminal commands sorted into general categories. I
have intentionally omitted long bash scripts and AppleScripts and focussed
instead on small useful commands that can be plugged into bigger scripts or used
on their own… enjoy!

System

Restart Mac OS X:

shutdown - r now
Shutdown Mac OS X:

shutdown now
Power Management / Energy Saving

Get overview of current Power Management Settings:

pmset -g
Put display to sleep after 15 minutes of inactivity:

sudo pmset displaysleep 15
Put Computer to sleep after 30 minutes of inactivity:

sudo pmset sleep 30
…Also see my post about hibernate mode and Safe Sleep on the Mac

OS X Look and Feel

Permanently disable Dock icon bouncing

Disable Dashboard (don’t forget to drag the Dashboard Dock icon off the Dock
too):

defaults write com.apple.dashboard mcx-disabled -boolean YES
killall Dock
Enable Dashboard:

defaults write com.apple.dashboard mcx-disabled -boolean NO
killall Dock
Force the Finder to show hidden files (very useful for Web Developers who need
to edit .htaccess files, for example):

defaults write com.apple.finder AppleShowAllFiles TRUE
Force the Finder to hide hidden files (ie: back to the default setting):

defaults write com.apple.finder AppleShowAllFiles FALSE
Networking

Ping a host to see whether it’s available:

ping -o leftcolumn.net
Troubleshoot routing problems to a host using traceroute:

traceroute leftcolumn.net
Check whether a host is running an HTTP server (ie: check that a Web Site is
available):

curl -I www.leftcolumn.net | head -n 1
Automatically enable Internet Sharing at startup

Manage Windows networks (a drop-in for the NET command on Windows). Too many
options to list here, so run this for details:

man net
Use dig to discover Domain information:

dig www.leftcolumn.net A
dig www.leftcolumn.net MX
Who is logged in to your Mac?

w
Show routing table:

netstat -r
Show active network connections:

netstat -an
Show network statistics:

netstat -s
Troubleshooting

List all open files (this will take a few seconds to complete on most Macs):

lsof
Restart Bonjour – handy when a Mac ‘disappears’ from the Network:

sudo launchctl unload
/System/Library/LaunchDaemons/com.apple.mDNSResponder.plist
sudo launchctl load /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist
Eject a CD… it’s never happened to me but you can eject a stuck cd with the
following. Note that it won’t always be ‘disk1′:

diskutil eject disk1
Text Manipulation commands

Sometimes you need to take some text from the clipboard or a file, transform it
somehow and then use it. Here are a bunch of commands that do text manipulation.
I’ve assumed you want to transform text from the clipboard and back again, see
the notes at the end of the article for info on how to write to and from files
instead.

Count number of lines in the text in the Clipboard:

pbpaste | wc -l
Count number of words in the text in the Clipboard:

pbpaste | wc -w
Sort lines of text in the Clipboard and copy them back to the Clipboard:

pbpaste | sort | pbcopy
Reverse each line of text in the Clipboard (ie: make each line appear backwards)
and copy them back to the Clipboard:

pbpaste | rev | pbcopy
Strip duplicate lines from lines of text in the Clipboard and copy only one
instance of each duplicate line back to the Clipboard (output is sorted):

pbpaste | sort | uniq | pbcopy
Find duplicate lines from lines of text in the Clipboard and copy only one
instance of each duplicate line (stripping non-duplicates) back to the Clipboard
(output is sorted):

pbpaste | sort | uniq -d | pbcopy
Strip duplicate lines from lines of text in the Clipboard and copy only one
instance of each line (stripping duplicates entirely) back to the Clipboard
(output is sorted):

pbpaste | sort | uniq -u | pbcopy
Tidy up HTML in the Clipboard and copy it back to the Clipboard:

pbpaste | tidy | pbcopy
Display the first 5 lines from the Clipboard:

pbpaste | head -n 5
Display the last 5 lines from the Clipboard:

pbpaste | tail -n 5
Convert tabs to spaces for the lines in the Clipboard:

pbpaste | expand | pbcopy
Other useful commands

Password protect your web site! Create a CRYPTed user/password for using in a
.htpasswd file. Save the outputted results of A below to a file called .htpasswd
in the directory you want to secure. Then save the contents of B to a file
called .htaccess in the same folder.

A:

htpasswd -nb username password
B:

AuthType Basic
AuthName "restricted area"
AuthUserFile /path/to/your/site/.htpasswd
require valid-user
Display a history of commands used in the terminal by the current user:

history
Convert a file to HTML. Support formats are Text, .RTF, .DOC.

textutil -convert html file.extension
Nano is a very easy-to-use text editor for quick changes to text files. It is
less powerful than VIM but has the advantage of clearly showing you the common
editing commands:

nano [file_to_edit]
…In nano, use ctrl+o to Save and ctrl+x to quit.

Greg shared a way of tidying the terminal window. Essentially this command
scrolls down a page, clearing the current view:

clear
iTunes

Change iTunes link behaviour to point at local iTunes Library instead of iTunes
Store:

defaults write com.apple.iTunes invertStoreLinks -bool YES
Change iTunes link behaviour to point at iTunes Store instead of local iTunes
Library (ie: back to the default):

defaults write com.apple.iTunes invertStoreLinks -bool NO
Other Mac OS X Terminal Resources

Mac OS X Hacking Tools (old but detailed list for the obsessive only).

Cameron Hayne’s Bash Scripts

Mac OS X Hints

Apple Forums

Note: For commands where I’ve used pbcopy to get the contents of the Clipboard
as input, you can use the contents of a file as input instead. Swap pbpaste for:

cat [/path/to/filename]
And to put the results into a file on your desktop, just swap | pbcopy for:

> ~/Desktop/filename.txt
… hope you find them useful!

