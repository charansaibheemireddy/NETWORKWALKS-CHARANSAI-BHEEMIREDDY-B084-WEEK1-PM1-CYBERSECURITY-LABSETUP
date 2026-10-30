# Cybersecurity Lab Environment Setup (Week 1)

## 📌 Project Overview
Building an isolated virtual lab environment for cybersecurity analysis and penetration testing using Oracle VirtualBox and Kali Linux on a private NAT Network[span_9](start_span)[span_9](end_span)[span_10](start_span)[span_10](end_span).

## ⚙️ Environment Specifications
- **Hypervisor:** Oracle VirtualBox (Latest Version)[span_11](start_span)[span_11](end_span)
- **Guest OS:** Kali Linux[span_12](start_span)[span_12](end_span)
- **Network Mode:** NAT Network (`NatNetwork`)[span_13](start_span)[span_13](end_span)[span_14](start_span)[span_14](end_span)
- **Subnet Prefix:** 10.0.0.0/24[span_15](start_span)[span_15](end_span)[span_16](start_span)[span_16](end_span)
- **Kali IP Configuration:** 10.0.0.2 / 24 (Default Gateway: 10.0.0.1, DNS: 8.8.8.8)[span_17](start_span)[span_17](end_span)[span_18](start_span)[span_18](end_span)
- **Integration:** Bidirectional Shared Clipboard, Drag-and-Drop, and Host Shared Folders enabled[span_19](start_span)[span_19](end_span)

## 🛠️ Implementation Steps
1. Configured a dedicated `NatNetwork` in VirtualBox using subnet `10.0.0.0/24` with DHCP enabled[span_20](start_span)[span_20](end_span)[span_21](start_span)[span_21](end_span).
2. Attached the Kali Linux virtual machine network adapter to `NatNetwork` with promiscuous mode set to allow all[span_22](start_span)[span_22](end_span).
3. Configured static IPv4 addressing (`10.0.0.2/24`) using `nmcli`[span_23](start_span)[span_23](end_span)[span_24](start_span)[span_24](end_span)[span_25](start_span)[span_25](end_span).
4. Fixed Duplicate Address Detection (DAD) timeout handling to ensure seamless external internet routing[span_26](start_span)[span_26](end_span).
5. Verified external reachability via ICMP echo requests to Google DNS[span_27](start_span)[span_27](end_span)[span_28](start_span)[span_28](end_span).
6. Created a baseline clean state snapshot in VirtualBox for disaster recovery[span_29](start_span)[span_29](end_span)[span_30](start_span)[span_30](end_span).

## 📸 Lab Evidence & Screenshots
*(Upload your terminal screenshot showing `ip a` and `ping google.com`, along with your VirtualBox snapshot and network settings screenshots directly here)*[span_31](start_span)[span_31](end_span)[span_32](start_span)[span_32](end_span)[span_33](start_span)[span_33](end_span)[span_34](start_span)[span_34](end_span)[span_35](start_span)[span_35](end_span)

## 🔧 Troubleshooting Experience
- **Issue:** After configuring the static IP (10.0.0.2), Kali Linux lost outbound internet connectivity and DNS resolution failed due to DAD conflict behavior on VirtualBox v7[span_36](start_span)[span_36](end_span)[span_37](start_span)[span_37](end_span).
- **Resolution:** Resolved by executing `sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0` followed by restarting the connection (`nmcli connection down/up`), restoring normal network operation[span_38](start_span)[span_38](end_span).
-
