# Small Business Threat Model (Agra Textiles Pvt Ltd)


**Organisation:** Agra Textiles Pvt Ltd (Fictional Case Study)

---

## What the Project Is

This project is a full threat model and risk assessment for a fictional 20-person garment export company based in Agra, Uttar Pradesh. The idea was to simulate the kind of security work that gets done for small businesses not in a lab environment, but grounded in how these organisations actually operate.

The business runs on Microsoft 365, Tally ERP, a shared NAS file server, and relies heavily on WhatsApp for supplier communication. No dedicated IT staff, no security budget, and no formal policies in place. A setup that is extremely common for Indian SMBs in the export space, and one that carries real risk.

The goal was to work through the entire process end to end: identify what the business owns, figure out where the threats actually sit, score them by likelihood and impact, map them against security controls, and produce recommendations that a real business could act on  not a theoretical wishlist.

---

## Framework Used

### STRIDE Threat Modelling
STRIDE was used to structure the threat identification across six categories:

- **Spoofing** — impersonating users or systems to gain access
- **Tampering** — unauthorised modification of data or systems
- **Repudiation** — actions that cannot be traced or denied
- **Information Disclosure** — data exposed to parties that should not have it
- **Denial of Service** — disrupting availability of systems or data
- **Elevation of Privilege** — gaining access beyond what is authorised

STRIDE works well for SMB assessments because it forces you to think beyond just external attackers. Insider threats, data integrity failures, and availability risks all surface through this lens.

### Risk Matrix
Each threat was scored on two axes: Likelihood and Impact. Risk is the combined read of both. The matrix was used to visually group threats by priority and give the business a clear picture of where immediate action is needed versus what can wait.

---

## Key Findings

Twelve threats were identified across six asset categories. Six came out as HIGH risk.

| ID | Threat | Risk |
|---|---|---|
| T-01 | Phishing Email | HIGH |
| T-02 | Ransomware via Email Attachment | HIGH |
| T-03 | Weak or Reused Passwords | HIGH |
| T-04 | No MFA on Business Email | HIGH |
| T-09 | No Offsite Backup | HIGH |
| T-10 | Macro-Based Malware (Excel/Word) | HIGH |
| T-05 | Unpatched Third-Party Applications | MEDIUM |
| T-06 | Insider Data Theft | MEDIUM |
| T-07 | WordPress Plugin Exploit | MEDIUM |
| T-08 | USB Malware Drop | MEDIUM |
| T-11 | Router Default Credentials | MEDIUM |
| T-12 | Shadow IT — Personal Cloud Storage | MEDIUM |

### Biggest gaps identified:
- No MFA anywhere on the business, including email and banking portals
- Macros enabled by default across all Office installations
- All staff running with local administrator rights
- Backup exists only on a USB drive stored in the same office, never tested for restoration
- No application patching process for third-party software

### Most critical finding:
The combination of no MFA, macros enabled, and admin rights on every machine means a single phishing email could result in a full network compromise and ransomware deployment with no recovery path. Three separate control failures stacking on top of each other.

---

## What I Learned

**Threat modelling is about understanding the business first.** The threats that matter for a garment exporter are different from those for a hospital or a software company. Getting the business profile right before identifying threats made the whole assessment more realistic and more useful.

**The hardest part is not finding threats it is communicating risk clearly.** Writing findings in a way that a business owner with no technical background can read and act on is a skill that does not come naturally from a technical background. It requires deliberate effort to strip out jargon and lead with consequence rather than cause.

**Most high-risk gaps in SMBs are not complex to fix.** MFA takes 30 minutes and costs nothing. Disabling macros takes an hour. These are configuration decisions that have not been made, not engineering problems that need solving. Understanding that distinction changes how you approach recommendations.

**An untested backup is not a backup.** This was the finding that stuck with me most. The business had a USB backup sitting in the office and probably felt covered. But it had never been tested, it was co-located with the original data, and it would have been encrypted alongside everything else in a ransomware attack. The control existed on paper but provided no actual protection.

**STRIDE is worth using even for small assessments.** I initially thought it might be overkill for a 20-person business. It was not. The T-12 shadow IT finding only surfaced because STRIDE pushes you to think about information disclosure and repudiation, not just external attacks. Without that structure, I would have missed it.
