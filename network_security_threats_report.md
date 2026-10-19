# Research Report: Common Network Security Threats

**Internship:** Oasis Infobyte  
**Task:** Task 4 — Common Network Security Threats  
**Prepared by:** Syed Abdul Hannan  
**Topics:** Distributed Denial of Service (DDoS), Man-in-the-Middle (MITM), IP Spoofing, and DNS Poisoning/Spoofing

## 1. Introduction

Network security protects computers, servers, networks, and information from unauthorized access and malicious activities. Network threats can interrupt online services, expose sensitive information, redirect users to fraudulent websites, and affect an organization's reputation. Understanding these threats helps network administrators choose suitable security controls, monitor suspicious activity, and respond to incidents. This report explains Distributed Denial of Service (DDoS), Man-in-the-Middle (MITM), IP spoofing, and DNS poisoning/spoofing, with real-world examples, possible impacts, and defensive measures.

## 2. Distributed Denial of Service (DDoS)

### 2.1 Definition

A Distributed Denial of Service (DDoS) attack occurs when an attacker uses multiple devices or sources to send excessive traffic to a target server, network, or online service. This traffic consumes resources such as bandwidth, processing capacity, or connection limits, making the service slow or unavailable to legitimate users.

Attackers may use a group of compromised devices called a **botnet**. Some DDoS attacks also use amplification, in which publicly accessible services send large responses to a victim after receiving requests with a falsified source IP address.

### 2.2 How It Works

1. An attacker directs large amounts of traffic toward a target.
2. Traffic from many devices or services reaches the target.
3. The target's network or system resources become overloaded.
4. Legitimate users experience delays, errors, or loss of access.

### 2.3 Real-World Example

On February 28, 2018, GitHub experienced a major DDoS attack that peaked at approximately **1.35 terabits per second (Tbps)**. The attack used memcached amplification, where IP spoofing helped direct large responses toward GitHub. GitHub worked with its mitigation provider to redirect traffic and restore service.

Source: [GitHub's February 28, 2018 DDoS Incident Report](https://github.blog/news-insights/company-news/ddos-incident-report/).

### 2.4 Impact

- Websites and online services may become unavailable.
- Organizations may lose revenue and productivity.
- Customers may be unable to access important services.
- Emergency or business operations may be disrupted.
- An organization's reputation may suffer.

### 2.5 Prevention and Mitigation

1. **Use DDoS protection services:** Work with suitable cloud or network providers to detect and filter malicious traffic.
2. **Monitor network traffic:** Set alerts for unusual traffic increases, abnormal packet rates, and unexpected connection patterns.
3. **Apply rate limiting and traffic filtering:** Configure appropriate controls to reduce abusive requests without blocking legitimate users.
4. **Coordinate with service providers:** Maintain emergency contacts for the internet service provider (ISP), hosting provider, or DDoS mitigation provider.
5. **Prepare an incident response plan:** Document how to detect, report, mitigate, and recover from an attack.

A host firewall can enforce traffic rules, but it cannot independently guarantee protection against every volumetric DDoS attack.

## 3. Man-in-the-Middle (MITM)

### 3.1 Definition

A Man-in-the-Middle (MITM) attack occurs when an attacker places themselves between two communicating parties and attempts to intercept, observe, or modify their communication without their knowledge.

Possible scenarios include malicious Wi-Fi access points, compromised network devices, and attacks that exploit weaknesses in certificate validation or communication security.

### 3.2 How It Works

1. A user communicates with a website, server, or another device.
2. An attacker gains a position that allows them to interfere with the communication.
3. The attacker attempts to intercept or modify the exchanged information.
4. If the security protections are insufficient or bypassed, sensitive information may be exposed or altered.

Strong encryption and correct certificate validation make many MITM attacks significantly more difficult.

### 3.3 Real-World Example

In 2011, the DigiNotar certificate authority was compromised, and fraudulent digital certificates were issued, including a certificate for Google. These certificates could enable attackers to impersonate websites and carry out MITM attacks against affected users. The incident demonstrated the importance of trustworthy certificate authorities and reliable certificate validation.

Source: [Microsoft Security Advisory 2607712 — Fraudulent Digital Certificates Could Allow Spoofing](https://learn.microsoft.com/en-us/security-updates/securityadvisories/2011/2607712).

### 3.4 Impact

- Login credentials or other sensitive information may be exposed.
- Communication may be modified in certain circumstances.
- Users may be redirected to fraudulent websites.
- Stolen information may be used for identity theft or unauthorized access.
- Organizations may face financial losses and reduced customer trust.

### 3.5 Prevention and Mitigation

1. **Use HTTPS and secure protocols:** Prefer websites and applications that use correctly configured TLS encryption.
2. **Validate security certificates:** Do not ignore browser certificate warnings; investigate unexpected certificate errors.
3. **Verify Wi-Fi networks:** Confirm the correct network name and avoid unknown or suspicious access points.
4. **Keep systems updated:** Install security updates for operating systems, browsers, and network devices.
5. **Use a trusted VPN when appropriate:** A reputable VPN can protect traffic across an untrusted network, but it does not replace HTTPS or protect against every endpoint-level attack.

HTTPS protects browser-to-website communication when configured and validated correctly. No single measure guarantees protection against every MITM scenario.

## 4. IP Spoofing

### 4.1 Definition

IP spoofing is a technique in which the source IP address in a network packet is falsified so that the packet appears to come from a different address. The source address is a claim in the packet; it does not necessarily identify the device or person that actually sent it.

IP spoofing is sometimes used in denial-of-service attacks, particularly reflection and amplification attacks.

### 4.2 How It Works

1. A sender constructs a network packet.
2. The sender places a falsified address in the source IP field.
3. The packet travels toward its destination.
4. The receiving system sees the claimed source address, which may not identify the real sender.

Spoofing an IP address does not automatically give an attacker access to the device or account associated with that address.

### 4.3 Real-World Example

During the February 2018 DDoS attack against GitHub, attackers used a memcached amplification technique. Spoofed source IP addresses caused vulnerable memcached servers to send large responses toward GitHub, contributing to the attack's enormous traffic volume.

Source: [Cloudflare — The Real Cause of Large DDoS Attacks: IP Spoofing](https://blog.cloudflare.com/the-root-cause-of-large-ddos-ip-spoofing/).

### 4.4 Impact

- Identifying the true source of traffic becomes more difficult.
- Spoofing can support reflection and amplification attacks.
- Network logs may contain misleading source addresses.
- Incident investigation and traffic filtering may become more complicated.
- Systems that trust IP addresses alone may make unsafe access decisions.

### 4.5 Prevention and Mitigation

1. **Apply ingress filtering:** Filter incoming packets at network boundaries when their source addresses are invalid or inconsistent with expected routes.
2. **Apply egress filtering:** Prevent outbound packets from leaving a network with source addresses that should not originate from that network.
3. **Configure routers and firewalls correctly:** Use appropriate access control lists and anti-spoofing controls.
4. **Monitor suspicious traffic:** Investigate unusual packet patterns, unexpected source addresses, and traffic spikes.
5. **Use stronger authentication:** Do not rely on an IP address alone to verify a user's identity or authorize sensitive actions.

Ingress filtering checks traffic entering a network, while egress filtering checks traffic leaving it. Both can help reduce IP spoofing, although their effectiveness depends on correct deployment.

## 5. Bonus Topic: DNS Poisoning/Spoofing

### 5.1 Definition

The Domain Name System (DNS) translates domain names, such as `example.com`, into IP addresses that computers use to communicate. DNS poisoning, also called DNS cache poisoning, occurs when false DNS information is inserted into a resolver's cache. DNS spoofing can also refer to forged DNS responses intended to mislead a client or resolver.

If false information is accepted, users may be directed to an incorrect or malicious destination instead of the intended website.

### 5.2 How It Works

1. A user's device requests the IP address for a domain name.
2. An attacker attempts to make a DNS resolver accept a forged or manipulated response.
3. The resolver may store incorrect information in its cache.
4. Users relying on the affected resolver may be directed to the wrong destination.

### 5.3 Real-World Example

In 2008, security researcher Dan Kaminsky disclosed a serious DNS cache-poisoning vulnerability affecting DNS resolver implementations. The issue prompted coordinated security updates and increased attention to DNS security. DNS Security Extensions (DNSSEC) help detect tampering by enabling validation of digitally signed DNS data.

Source: [Internet Systems Consortium — CVE-2008-1447: DNS Cache Poisoning Issue](https://kb.isc.org/docs/aa-00924).

### 5.4 Impact

- Users may be redirected to fraudulent websites.
- Login credentials or financial information may be stolen.
- Organizations may experience service disruption.
- Incorrect DNS records may affect multiple users of a shared resolver.
- Trust in online services may be damaged.

### 5.5 Prevention and Mitigation

1. **Deploy DNSSEC validation:** Use DNSSEC-capable resolvers and validate signatures where supported to help detect forged DNS data.
2. **Keep DNS software updated:** Apply security patches to DNS servers, resolvers, and related systems.
3. **Secure DNS infrastructure:** Restrict administrative access, use strong authentication, and monitor configuration changes.
4. **Use trusted resolvers:** Configure devices and networks to use reputable DNS services with suitable security controls.
5. **Monitor and investigate suspicious changes:** Check unexpected DNS responses, domain redirects, and unauthorized record modifications.

DNSSEC helps verify the authenticity and integrity of signed DNS data, but it does not prevent every DNS-related attack or secure a compromised endpoint by itself.

## 6. Comparison of Network Security Threats

| Threat | Attack vector | Who is at risk? | Difficulty to execute | Ease of mitigation |
|---|---|---|---|---|
| DDoS | Flooding a target with traffic or using reflection/amplification | Websites, online services, businesses, and their users | Varies; large attacks often require significant resources or abused infrastructure | Moderate to difficult during a large attack; upstream filtering and specialized protection help |
| MITM | Intercepting or altering communication between parties | Users and organizations using vulnerable or improperly secured connections | Varies; depends on network access and security weaknesses | Easier when strong encryption and certificate validation are correctly implemented; harder in compromised environments |
| IP Spoofing | Falsifying the source IP address in packets | Networks and services that receive spoofed traffic; potential DDoS victims | Varies; basic spoofing may be straightforward on some networks, while useful attack scenarios require additional conditions | Filtering helps, but protection depends on deployment across relevant network boundaries |
| DNS Poisoning/Spoofing | Introducing false DNS responses or cache records | Users and organizations relying on affected DNS infrastructure | Varies; modern protections make successful attacks more difficult | DNSSEC validation, updates, and secure resolver configuration reduce risk |

*Note: Difficulty and mitigation ratings are qualitative. They depend on the target environment, attacker capabilities, network configuration, and existing security controls.*

## 7. Role of Firewalls and Network Monitoring

Firewalls control network traffic according to configured rules. Network monitoring helps administrators identify unusual activity and investigate potential security incidents.

Tools such as **Nmap** help authorized administrators discover hosts, open ports, and exposed services. **UFW (Uncomplicated Firewall)** provides a way to configure firewall rules on supported Linux systems.

These tools are useful for learning and managing network security, but their roles differ:

- Nmap is primarily a network discovery and scanning tool, not a complete defense against DDoS, MITM, IP spoofing, or DNS poisoning.
- UFW can enforce host-level traffic rules, but it cannot independently prevent every form of these attacks.
- Effective defense requires layered controls, secure configurations, appropriate monitoring, timely updates, and an incident response plan.

Security testing should only be performed on systems and networks for which permission has been granted.

## 8. Conclusion: Three Key Takeaways for Network Administrators

1. **Understand the threat:** DDoS primarily threatens service availability, MITM targets communication, IP spoofing falsifies packet source addresses, and DNS poisoning can redirect users through false DNS information.
2. **Use layered security controls:** Apply appropriate traffic filtering, secure protocols, strong authentication, DNS protections, updates, and monitoring rather than relying on a single tool.
3. **Prepare to respond:** Maintain an incident response plan, review logs, coordinate with service providers, and test defensive controls in authorized environments.

Learning how these threats work helps network administrators make informed security decisions and reduce the likelihood and impact of network incidents.

## 9. References

1. **Cybersecurity and Infrastructure Security Agency (CISA).** *UDP-Based Amplification Attacks.*  
   https://www.cisa.gov/ncas/alerts/ta14-017a

2. **GitHub.** *February 28th DDoS Incident Report* (2018).  
   https://github.blog/news-insights/company-news/ddos-incident-report/

3. **Microsoft.** *Security Advisory 2607712: Fraudulent Digital Certificates Could Allow Spoofing* (2011).  
   https://learn.microsoft.com/en-us/security-updates/securityadvisories/2011/2607712

4. **Cloudflare.** *The Real Cause of Large DDoS Attacks: IP Spoofing* (2018).  
   https://blog.cloudflare.com/the-root-cause-of-large-ddos-ip-spoofing/

5. **Internet Systems Consortium (ISC).** *CVE-2008-1447: DNS Cache Poisoning Issue.*  
   https://kb.isc.org/docs/aa-00924

6. **Internet Corporation for Assigned Names and Numbers (ICANN).** *DNSSEC — What Is It and Why Is It Important?*  
   https://www.icann.org/resources/pages/dnssec-what-is-it-why-important-2019-03-05-en

---

**Disclaimer:** This report is prepared for educational purposes as part of the Oasis Infobyte internship. It describes network threats and defensive practices; all security testing should be conducted only with proper authorization.
