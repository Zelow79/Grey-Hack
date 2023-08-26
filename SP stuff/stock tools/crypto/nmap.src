//command: nmap
if params.len != 1 or params[0] == "-h" or params[0] == "--help" then exit(command_info("nmap_usage"))	
if not is_valid_ip(params[0]) then exit("nmap: invalid ip address")
if not get_shell.host_computer.is_network_active then exit("nmap: No internet access.")

ipAddress = params[0]
isLanIp = is_lan_ip( ipAddress )

if isLanIp then
   router = get_router;
else 
   router = get_router( ipAddress )
end if

if router == null then exit("nmap: ip address not found")
ports = null

if not isLanIp then
   ports = router.used_ports
else
   ports = router.device_ports(ipAddress)
end if

if ports == null then exit("nmap: ip address not found")
if typeof(ports) == "string" then exit(ports)
      
info = "PORT STATE SERVICE VERSION LAN"   
print("\nStarting nmap v1.1 at " + current_date)
print("Interesting ports on " + params[0] + "\n")
if(ports.len == 0) then exit("Scan finished. No open ports.")

for port in ports
   service_info = router.port_info(port)
   lan_ips = port.get_lan_ip
   port_status = "open"

   if(port.is_closed and not isLanIp) then
      port_status = "closed"
   end if
   info = info + "\n" + port.port_number + " " + port_status + " " + service_info + " " + lan_ips
end for
print(format_columns(info) + "\n")