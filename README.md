# Xiaomi Router 10000 setup guide

An independent guide to checking firmware and configuring the Xiaomi Router 10000 for Ethernet WAN, PPPoE with VLAN tagging, IPv6, local DNS, and Wi-Fi. Results apply to the model, hardware revision, region, and firmware listed with each test.

## Compatibility status

| Feature | Status | What to verify |
| --- | --- | --- |
| Four 2.5 GbE ports and two 10 GbE interfaces | Documented | Identify the ports and their selectable roles on your unit. |
| Internet PPPoE with an 802.1Q tag on a 2.5 GbE WAN port | Pending hardware test | Confirm the tag on the selected physical port and establish a real ISP session. |
| DHCPv6 prefix delegation and custom IPv6 DNS | Pending hardware test | Confirm IPv6 routing and inspect the DNS settings received by actual clients. |
| Local administrative SSH | Pending hardware test | Confirm a supported administrator-access method for the exact firmware. |
| Wi-Fi features and coverage | Pending hardware test | Record regional settings, client capabilities, channel width, and measurements. |

## 1. Identify the router and check firmware

Connect one computer to the router by Ethernet on an isolated bench. Record the model code, hardware revision, firmware build, and firmware region. Check the router's built-in updater for the latest stable version available for that exact unit. Use the vendor's update and recovery instructions and keep a configuration export or a record of settings needed to restore access. Recheck port assignments and saved settings after reboot. [Xiaomi firmware update guide](https://www.mi.com/global/support/faq/details/KA-348402/).

## 2. Verify supported local SSH access

Check the device's administration panel and documentation for a supported SSH option. If available, verify the host key on first connection, use key-based authentication where supported, and restrict access to the management network. Test login after a reboot and verify that the management port is unreachable from WAN and guest networks. Record the model and firmware used. Some vendor developer interfaces grant limited application access, so verify that the account actually supports the administration tasks you need.

## 3. Set up PPPoE and VLAN tagging

Choose a physical 2.5 GbE port as WAN if your firmware exposes that assignment. This leaves the 10 GbE interfaces available for LAN use or future expansion. Obtain the VLAN ID, credentials, and any special MTU settings from your ISP. Set the VLAN on the **Internet WAN** interface and confirm that the PPPoE discovery frame on the chosen port carries the expected 802.1Q tag. If the tag appears absent in a capture, check whether the receiving NIC or capture setup strips tags. An IPTV VLAN setting alone does not establish how Internet PPPoE is tagged.

Verify link negotiation, successful PPPoE authentication, a working default route, and Internet access from a wired client. [Qualcomm hardware overview](https://www.qualcomm.com/networking-infrastructure/device-finder/xiaomi-router-10000).

## 4. Configure IPv6 and local DNS

Use your ISP's documented IPv6 connection mode. Confirm DHCPv6 prefix delegation where required, a valid routed prefix on the LAN, and working IPv6 Internet access. For local resolvers, inspect DHCPv4 DNS option 6 and the IPv6 Router Advertisement RDNSS option. If DHCPv6 also advertises DNS, check that it advertises the intended resolvers. Query each advertised resolver directly for A and AAAA records. Then repeat using the client's normal DNS settings on Ethernet and Wi-Fi. Verify the settings survive a router reboot and client lease renewal. [IPv6 Router Advertisement DNS options](https://www.rfc-editor.org/rfc/rfc8106.html).

## 5. Tune Wi-Fi and verify the change

Use the regulatory profile for your location and the supported channel and power settings for the hardware. Start with a compatible configuration. Compare the same client at the same locations before and after a channel, width, placement, or power change. Record signal strength, local throughput, and any disconnects. Check that phones reconnect after sleep and that older Wi-Fi devices still work.

For a live cutover, keep the previous router and its settings ready. If wired Internet, local DNS, or management access fails within your maintenance window, reconnect the previous router and verify service from a fresh client lease.

## Contribute a test result

Include the exact model code, hardware revision, firmware build, region, feature tested, and observed result. Note whether you used an isolated setup or an ISP connection. Use placeholders in screenshots and examples. Remove credentials, serial numbers, MAC addresses, public IP addresses, device identifiers, and customer-specific network details before posting.
