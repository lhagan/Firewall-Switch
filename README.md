# Firewall Switch

Firewall Switch is a simple utility that allows you to turn OS X Lion's built-in firewall on or off without opening Preferences.

Just run the app and it'll detect whether or not the Firewall is turned on. If so, it'll ask you to confirm that you want to turn the firewall off, otherwise it'll ask for confirmation to switch the firewall back on (in "Block all incoming connections" mode).

That's it! [Download Firewall Switch](https://github.com/lhagan/Firewall-Switch/zipball/master) to try it out.

## Acknowledgements

Thanks to Charles Edge for a [very detailed article on scripting the Lion firewall](http://krypted.com/mac-os-x/the-os-x-application-layer-firewall-part-3-lion/) and to Mac OS X Hints commenter dsanfili for the [script](http://hints.macworld.com/comment.php?mode=view&cid=106657) on which this one is based.

## How

Firewall Switch is an AppleScript application that runs shell commands to control the firewall:
	
	# check firewall status
    defaults read /Library/Preferences/com.apple.alf globalstate
	
	# turn firewall on (Block all incoming connections)
	/usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on --setblockall on
	
	# turn firewall off (Allow all incoming connections)
	/usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate off

By default, Firewall Switch sets the firewall to block everything ('System Preferences > Security > Firewall > Advanced > Block all incoming connections') when switched on. It's really a good idea to use this mode any time you're on a public network.

If you do need to allow access through the firewall to specific applications, you can edit the script to do so. Open 'Applications > Utilities > AppleScript Editor', then go to 'File > Open' and select the Firewall Switch application. Find `--setblockall on` in the script, delete it, and save the file. 