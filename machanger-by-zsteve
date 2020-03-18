#!/usr/bin/env python

import subprocess
import optparse
import re


def get_arguments():
    parser = optparse.OptionParser()

    parser.add_option("-i", "--interface", "--iface", dest="interface", help="Interface to change its MAC ADDRESS")
    parser.add_option("-m", "--new_mac", "--mac", dest="new_mac", help="New MAC ADDRESS")

    (options, arguments) = parser.parse_args()

    if not options.interface: # if user doesn't put a value for interface
        # code to handle the error
        parser.error("[-] Please specify an interface, use --help for more info")
    elif not options.new_mac: # if user doesn't put a value for mac address
        # code to handle the error
        parser.error("[-] Please specify a MAC address, use --help for more info")
    return options


def change_mac(interface, new_mac):
    print("[+] Changing MAC address for " + interface + " to " + new_mac + "\n")

    subprocess.call(["ifconfig", interface, "down"])
    subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
    subprocess.call(["ifconfig", interface, "up"])
    #subprocess.call("service network-manager restart", shell=True)


def get_current_mac(interface):
    ifconfig_result = subprocess.check_output(["ifconfig", interface])

    mac_address_search_result = re.search(r"\w\w:\w\w:\w\w:\w\w:\w\w:\w\w", ifconfig_result)

    if not mac_address_search_result:
        print("Can't find MAC ADDRESS")
    else:
        return (mac_address_search_result.group(0))



options = get_arguments()


current_mac = get_current_mac(options.interface)
print(("Current MAC ADDRESS: "+ str(current_mac))+"\n")

change_mac(options.interface, options.new_mac)


current_mac = get_current_mac(options.interface)
if current_mac == options.new_mac:
    print("[+] MAC ADDRESS was successfully changed to " + current_mac + "\n")
    print("[+] " + options.interface + " propieties: " + "\n")
    print(subprocess.check_output(["ifconfig", options.interface]))
    print("Thanks for using! :)")

else:
    print("[-] MAC ADDRESS did not get changed")


