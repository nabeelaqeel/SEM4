1. What is the key difference between IDS and IPS in terms of network deployment?

| **Feature**           | IDS (Intrusion Detection System)                                                | IPS (Intrusion Prevention System)                                  |
| --------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Deployment Mode**   | Passive (out-of-band)                                                           | Active (in-line)                                                   |
| **Network Position**  | Connected to a span port, mirror port, or network tap (monitors copied traffic) | Directly in the traffic path (all packets must pass through it)    |
| **Traffic Handling**  | Analyzes copies of traffic (does not process live traffic)                      | Inspects and modifies live traffic in real-time                    |
| **Response Action**   | Alerts only (logs and notifies administrators)                                  | Automatically blocks/drops malicious traffic (e.g., stops attacks) |
| **Impact on Network** | No risk of disrupting legitimate traffic (since it's passive)                   | May cause false positives, blocking good traffic if misconfigured  |
| **Latency**           | **No added latency** (only monitors copies)                                     | Adds slight latency (since it processes every packet)              |
| **Use Case**          | Best for monitoring & forensic analysis                                         | Best for real-time threat prevention                               |

2. What is a zero-day attack and why is it dangerous?

	A zero-day attack (or 0-day exploit) is a cyberattack that takes advantage of a previously unknown software/hardware vulnerability—meaning the vendor or developer has "zero days" to fix it before attackers exploit it.
	
	It is dangerous because  No patch available , Hard to detect and Highly effective

3. What are the two main types of IPS solutions? Give one example of each.

	1. Network-Based IPS (NIPS)
		- Example: Cisco Firepower NGIPS

	2. Host-Based IPS (HIPS)
		- Example: Trend Micro Deep Security

4. What does Cisco Snort IPS do when a traffic pattern matches a known signature?

	When Cisco Snort IPS detects traffic matching a known attack signature, it either logs an alert (passive detection) or actively blocks/drops malicious packets, terminates connections via TCP reset, or blacklists attacker IPs (inline prevention), depending on whether it's configured in IDS (monitoring) or IPS (active protection) mode; for example, upon detecting a SQL injection attempt, Snort can simply record the event or immediately stop the attack in real-time.

3. How is traffic mirrored to a network-based IDS for monitoring?

	Traffic is mirrored to a network-based IDS (like Snort or Suricata) using port mirroring (SPAN) on switches, which copies all packets from specified source ports/VLANs to a destination port where the IDS is connected, or via **network taps** that passively duplicate traffic for analysis without affecting the original data flow, enabling the IDS to monitor traffic without being in-line.

3. What is the purpose of an IPS signature in detecting malicious traffic?

	IPS signatures are predefined patterns or rules that identify known malicious traffic, such as exploits, malware, or attack techniques. They enable the IPS to detect and block threats by matching network traffic or behavior against these signatures.

3. Differentiate between atomic and composite signatures in IPS.

	- **Atomic signatures** detect attacks in a single packet or session (e.g., a malicious payload in one HTTP request).
	    
	- **Composite signatures** analyze multiple packets or sessions over time (e.g., a multi-step attack like a brute-force login attempt).

3. What is the difference between a true positive and a false positive in IPS alerts?

	- A true positive occurs when the IPS correctly identifies and blocks actual malicious traffic.
	    
	- A false positive happens when the IPS mistakenly flags legitimate traffic as malicious, potentially disrupting normal operations.

3. What is the role of Snort in Cisco IPS deployments?

	Snort, integrated into Cisco’s IPS solutions (like Firepower), provides signature-based detection and real-time traffic analysis, enabling threat prevention through customizable rules and open-source intelligence.

3. List two actions that a Snort IPS can take when it detects a matching rule.

	- Drop the malicious packet to block the attack.
	- Generate an alert to notify administrators without stopping traffic.