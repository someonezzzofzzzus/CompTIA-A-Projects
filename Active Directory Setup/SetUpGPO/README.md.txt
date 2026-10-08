# Group Policy Object (GPO) Configuration

## Overview

This project demonstrates the creation, configuration, deployment, and verification of a **Group Policy Object (GPO)** within a Windows Server Active Directory environment.

The purpose of this lab was to understand how Group Policy can be used to centrally manage Windows computers and users within a domain.

Instead of configuring each workstation individually, a GPO allows administrators to define settings centrally and apply them to computers or users within a specific Organizational Unit (OU).

---

## Lab Environment

| Component | Configuration |
|---|---|
| Domain Controller | Windows Server |
| Domain | `mynetwork.com` |
| Client | `PC-2` | `PC-1` |
| Directory Services | Active Directory Domain Services |
| Policy Management | Group Policy Management |
| Target OU | `Workstations` |

---

## Objectives

The objectives of this lab were to:

- Create an Organizational Unit
- Create a Group Policy Object
- Configure policy settings
- Link the GPO to an Organizational Unit
- Apply the policy to a domain-joined computer
- Force a Group Policy update
- Verify that the policy was successfully applied
- Understand the relationship between Active Directory, OUs, and GPOs

---

# 1. Organizational Unit

An **Organizational Unit (OU)** was created within Active Directory to contain the domain-joined workstation.

Example structure:

```text
mynetwork.com
│
├── Users
├── Computers
├── Domain Controllers
│
└── Workstations
    └── PC-1
    └── PC-2
```

The `Workstations` OU provides a dedicated location where workstation-related Group Policy settings can be applied.

---

# 2. Creating the GPO

The **Group Policy Management** console was opened through:

```text
Server Manager
    → Tools
        → Group Policy Management
```

A new GPO was created and named:

```text
Workstation Security Policy
```

The GPO was initially created under:

```text
Group Policy Objects
```

Creating the GPO separately allows it to be configured before being linked to the required Organizational Unit.

---

# 3. Configuring the GPO

The GPO was opened using:

```text
Right-click GPO
    → Edit
```

The Group Policy Management Editor provides two main configuration areas:

```text
Computer Configuration
User Configuration
```

For this lab, the policy was configured under the appropriate configuration section depending on whether the setting was intended to apply to the computer or the user.

Example structure:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
```

Only settings relevant to the purpose of the lab were configured.

---

# 4. Linking the GPO

After configuration, the GPO was linked to the `Workstations` Organizational Unit.

The resulting structure was:

```text
Workstations OU
       │
       ▼
Workstation Security Policy
       │
       ▼
      PC-2
```

This means that the policy can be applied to computers located within the `Workstations` OU.

---

# 5. Updating Group Policy

After linking the GPO, the client computer was updated manually.

On `PC-2`, the following command was executed from an elevated Command Prompt or PowerShell session:

```powershell
gpupdate /force
```

This forces the computer and user Group Policy settings to be refreshed.

A successful update should produce output indicating that the computer and/or user policy update completed successfully.

---

# 6. Verifying the GPO

The applied Group Policy settings were verified using:

```powershell
gpresult /r
```

The output can be used to identify which Group Policy Objects were successfully applied.

The expected result includes:

```text
Applied Group Policy Objects
----------------------------
Workstation Security Policy
```

This provides evidence that the GPO was successfully processed by the client.

---

# 7. Group Policy Results

For additional verification, the **Group Policy Results Wizard** in Group Policy Management can be used.

The report provides information about:

- Applied GPOs
- Denied GPOs
- Computer configuration
- User configuration
- Security filtering
- Group Policy processing

This provides a more detailed view of how Group Policy was processed on the client.

---

# 8. Troubleshooting

If the GPO does not appear to apply, the following checks can be performed:

### Check the computer's OU

Verify that `PC-2` is located inside:

```text
Workstations
```

### Check the GPO link

Verify that:

```text
Workstations
    └── Linked Group Policy Objects
        └── Workstation Security Policy
```

### Check domain membership

Verify that the client is joined to:

```text
mynetwork.com
```

### Check DNS

The client should use the internal DNS server associated with the Active Directory environment.

This can be checked with:

```powershell
ipconfig /all
```

### Refresh Group Policy

```powershell
gpupdate /force
```

### Check applied policies

```powershell
gpresult /r
```

---

# Evidence

The following screenshots document the configuration and verification process:

```text
screenshots/
│
├── 01-workstations-ou.png
├── 02-gpo-created.png
├── 03-gpo-configuration.png
├── 04-gpo-linked-to-ou.png
├── 05-gpupdate.png
├── 06-gpresult.png
└── 07-policy-result.png
```

Each screenshot provides evidence of a different stage of the process, from creating the GPO through to verifying that it was successfully applied to the client.

---

# Skills Demonstrated

This project demonstrates practical experience with:

- Active Directory
- Organizational Units
- Group Policy Management
- Group Policy Objects
- GPO configuration
- GPO linking
- Windows Server administration
- Windows client administration
- Centralized configuration management
- `gpupdate`
- `gpresult`
- Group Policy troubleshooting
- Basic Active Directory administration

---

# Conclusion

This lab provided hands-on experience with centralized Windows administration using Group Policy.

The process demonstrated the complete lifecycle of a GPO:

```text
Create OU
   ↓
Create GPO
   ↓
Configure GPO
   ↓
Link GPO to OU
   ↓
Update Client
   ↓
Verify Policy
   ↓
Troubleshoot if Required
```

The key objective was not simply to create a GPO, but to understand how **Organizational Units, Group Policy, Active Directory, and domain-joined clients work together to centrally manage Windows environments**.