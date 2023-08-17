//command: rshell-server
rshelld = include_lib("/lib/librshell.so")
if not rshelld then
    rshelld = include_lib(current_path + "/librshell.so")
end if
if not rshelld then    
    get_shell.launch("/bin/apt-get", "update")
    get_shell.launch("/bin/apt-get", "addrepo $HACKSHOP_IP")
    get_shell.launch("/bin/apt-get", "update")
    get_shell.launch("/bin/apt-get", "install librshell.so")
    rshelld = include_lib("/lib/librshell.so")
end if
if not rshelld then exit("Error: Missing librshell.so library in the /lib path or the current folder")
output = rshelld.install_service
if output != true then exit(output)
print("<b>Type 'Browser.exe " + get_router.local_ip + ":8080' to access the router configuration to make sure the service it's accesible</b>")