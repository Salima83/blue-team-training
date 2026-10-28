# Lab 04: Windows Event Log Analysis & Brute Force Incident Response

## Overview
This laboratory covers the analysis of Windows Event Logs during a simulated Remote Desktop Protocol (RDP) Brute Force attack, followed by the execution of the **S.I.E.R.A** incident response methodology.

## Key Artifacts & Event IDs
* **Event ID 4625**: An account failed to log on (Brute Force indicator).
* **Event ID 4624**: An account was successfully logged on (Successful breach).
* **Logon Type 10**: RemoteInteractive (RDP session).
* **Event ID 4720**: A user account was created (Persistence check).

## Incident Scenario
* **Target System**: `AD-SERVER-01`
* **Alert**: High volume of Event ID 4625 logs on `Administrator` account from external IP `185.220.101.5`, followed by Event ID 4624 (Logon Type 10).

## Incident Response (S.I.E.R.A Protocol)
1. **Signalement (Detection)**: Identified 300+ failed logon attempts (`4625`) followed by a successful RDP login (`4624`, Type 10) from an unverified external IP.
2. **Isolation (Containment)**: 
   * Terminated active RDP session.
   * Blocked source IP `185.220.101.5` at the edge firewall.
   * Locked and reset credentials for the `Administrator` account.
3. **Éradication (Eradication)**:
   * Checked for unauthorized persistence mechanisms (audited Event ID `4720` for suspicious account creation).
   * Verified no backdoor services were registered during the compromised window.
4. **Restauration (Recovery)**:
   * Enforced Account Lockout Policy after 5 failed attempts.
   * Restricted RDP access to internal VPN connections only.
   * Restored normal server operations.
5. **Analyse (Post-Incident Report)**:
   * Documented attack timeline, IoCs (IP `185.220.101.5`), and implemented long-term MFA mitigation.
