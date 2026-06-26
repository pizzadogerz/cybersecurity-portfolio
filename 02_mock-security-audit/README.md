# Security Audit — Botium Toys

## What's this?

This is a security audit I completed as part of the Google Cybersecurity Professional Certificate. The activity gave me a fictional company called Botium Toys and asked me to go through their current security setup, check what controls they have (or don't have), and see if they're compliant with key regulations.

**Frameworks used:** NIST CSF, PCI DSS, GDPR, SOC

---

## Quick Background on Botium Toys

Botium Toys is a small U.S. toy company that's been growing its online presence. Their IT manager got worried because the company was expanding without a clear security plan — especially since they're processing online payments and dealing with customer data from E.U. customers.

So they needed an audit. That's where I came in.

**Risk Score: 8/10** — pretty high, mostly because a lot of basic controls are just... not there yet.

---

## Controls Assessment

Basically went through each control and asked: does Botium Toys actually have this in place?

| Control | In Place? |
|---|---|
| Least Privilege | No |
| Disaster Recovery Plans | No |
| Password Policies | No |
| Separation of Duties | No |
| Firewall | Yes |
| Intrusion Detection System (IDS) | No |
| Backups | No |
| Antivirus Software | Yes |
| Manual Monitoring for Legacy Systems | No |
| Encryption | No |
| Password Management System | No |
| Locks (offices, storefront, warehouse) | Yes |
| CCTV Surveillance | Yes |
| Fire Detection/Prevention | Yes |

Honestly the physical security is fine — locks, CCTV, fire systems are all good. But the technical and admin side has a lot of gaps.

---

## Compliance Checklist

### PCI DSS (Payment Card Industry)

| Best Practice | Adhered To? |
|---|---|
| Only authorized users can access credit card info | No |
| Card data stored and transmitted securely | No |
| Encryption used for credit card data | No |
| Secure password management in place | No |

### GDPR (for E.U. customers)

| Best Practice | Adhered To? |
|---|---|
| E.U. customer data is kept private | No |
| Plan to notify E.U. customers within 72 hours of a breach | Yes |
| Data is properly classified and inventoried | No |
| Privacy policies enforced | Yes |

### SOC (type 1 & 2)

| Best Practice | Adhered To? |
|---|---|
| User access policies established | No |
| PII/SPII data is confidential | No |
| Data integrity is maintained | Yes |
| Data available to authorized users | Yes |

---

## My Recommendations

The biggest issues here are access control and data protection — those need to be fixed first before anything else.

Right now every employee can access all internal data including credit card info and customer PII. That's a serious problem. And there's zero encryption on that data. So even if someone got in, there's nothing protecting it.

### Fix these first (High Priority)
- **Least privilege + separation of duties** — not everyone needs access to everything
- **Encryption** — especially for credit card and customer data
- **IDS** — the firewall alone isn't enough, they need something to detect threats that slip through
- **Disaster recovery plan + backups** — if something goes wrong right now, they have no way to recover
- **Password management system** — the current password policy is too weak and there's no system enforcing it

### Next up (Medium Priority)
- **Formalize legacy system monitoring** — it's being monitored but there's no actual schedule or process
- **Data classification** — they need to know what data they have before they can properly protect it

### Lower Priority
- Tighten up the password policy requirements
- Extend privacy policy enforcement beyond just the IT department

Bottom line — Botium Toys has the physical side covered but the technical and admin controls need a lot of work. Getting the high priority items done would make a huge difference in bringing that risk score down.
