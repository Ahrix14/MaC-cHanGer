import subprocess
import optparse
import re

print("\t\t\tMaC cHanGer\n\t\t\t By AnKiT\n\n")

def get_arguments():
    parser = optparse.OptionParser()
    parser.add_option("-i", "--interface", dest="interface", help="Interface to change its mac")
    parser.add_option("-m", "--mac", dest="new_mac", help="new mac address")
    (options, arguments) = parser.parse_args()
    if not options.interface:
        parser.error("[-] please specify the interface, write --help for more info")
    elif not options.new_mac:
        parser.error("[-] please specify the new mac, write --help for more info")
    else:
        return options

def change_mac(interface, new_mac):
    print("[+] changing mac address of " + interface + " to " + new_mac)
    # more secure:
    subprocess.call(["ifconfig", interface, "down"])
    subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
    subprocess.call(["ifconfig", interface, "up"])

def get_current_mac(interface):
    check_output = subprocess.check_output(["ifconfig", interface])
    check_mac = re.search(r"\w\w:\w\w:\w\w:\w\w:\w\w:\w\w", str(check_output))
    if check_mac:
        return check_mac.group(0)
    else:
        print("[-] cannot read the mac")

options = get_arguments()

current_mac = get_current_mac(options.interface)
print("Current MAC = " + str(current_mac))

change_mac(options.interface, options.new_mac)

current_mac = get_current_mac(options.interface)
if current_mac == options.new_mac:
    print("[+] MAC address is successfully changed to " + current_mac)
else:
    print("[-] MAC address did not changed")

