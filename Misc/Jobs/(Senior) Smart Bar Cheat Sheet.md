# (Senior) Smart Bar Cheat Sheet

DISCLAIMER: This was made before other SB info sheets were shared. I know there are others being shared but this one is an adaptation of my [original notes](https://notes.oling.dev/Misc/Jobs/Smart%20Bar%20Notes) from last year.

This is designed to be completely searchable with CTRL + F, and shareable with other SBAs.

## Admin
Fill in after each interaction: [SB staff page](https://forms.cloud.microsoft/pages/responsepage.aspx?id=7qe9Z4D970GskTWEGCkKHrD7NcXXkf9CvFlZEZD7gIVUM0lRVklGODQ4OExFUko2TzRINTBVWjdORCQlQCN0PWcu)

### Complete the Smart Bar Customer Survey below!
[Customer survey](https://forms.office.com/pages/responsepage.aspx?id=7qe9Z4D970GskTWEGCkKHrD7NcXXkf9CvFlZEZD7gIVUNkZYUDdZV0dVUTQ4WVhUTzVKOTNZS0NQMyQlQCN0PWcu)
![Pasted image 20251210134426](../../Images/Pasted%20image%2020251210134426.png)
Rate us 5 stars!!
---

### Quick Links

- IT Service Desk Info Page: https://www.nottingham.ac.uk/dts/help/it-support.aspx
	- Phone number: **0115 95 16677**
		- Option 1 for **anything to do with printing**/Xerox.
		- Option 2 for general student/other inquiries.
		- Option 4 for staff and associates.
	- For room assistance:  **0115 74 87777**
- Raise a ticket: https://uniofnottm.saasiteu.com/Modules/SelfService/
- SEAtS Online: https://uon.seats.cloud/ (attendance)
- Halls WiFi for unsupported devices: https://nottingham.campuswifi.net/
- Resource Booker for rooms: https://resourcebooker.nottingham.ac.uk/

## Internet access

### Wireless/eduroam
> tags: connection, wifi, wi-fi, internet, signal, strength, disconnecting, Chromebook 

- Eduroam needs the **full university account email address** (not username) and password.
- The correct configurations for all devices is available at https://www.nottingham.ac.uk/dts/connect-to-wifi.aspx

#### Windows
- Many devices say "Couldn't connect to this network". A typical fix is to forget the network and sign in again.
- When signing in (and credentials are correct), Windows will prompt with a certificate for eduroam, which must be trusted. If you do not get to the certificate stage, make sure they are typing their password correctly - this can be done by having the user write it in plaintext in e.g. a notes app or Word, and cutting/pasting this into the login field (**please take security seriously when doing this**).
- If there are still issues, ensure a usercheck is carried out. Another reasonable way to debug this is to sign in to your own account (**remembering to forget immediately afterwards**) to determine if this is a laptop/hardware issue, or an account issue.
	- If there are further issues, ITSD (via a Senior or Manager) can be asked with the MAC address to determine an issue. 
	- There are a small number of known NIC incompatibilities with particularly older Intel devices, drivers may need to be updated.

#### Android
Different Android devices have different ways of connecting and expose different fields when connecting. However, the most common way to resolve any issue is by using the following configuration:

- EAP method: PEAP
- Phase 2 authentication: MSCHAPv2
- CA Certifcates: Use system certificates (*n.b. would also recommend **Trust on first use** for stubborn devices.*)
- Domain: `nottingham.ac.uk` (old `radius.nott...` no longer works)
- Identity: `username@nottingham.ac.uk`
	- If users have other emails e.g. `firstname.lastname@nottingham.ac.uk` these may not always work; so always use the short `username` first. Exceptions: staff and postgrads who were not here for undergraduate.
- Anonymous identity: `anonymous@nottingham.ac.uk`
- Password: user's university password
- Privacy settings: use device MAC address (you can use fixed/rotating, but make sure it works with the device's own one first)


##### OnePlus and Oppo devices specific weird issue
There have been a few cases of OnePlus/Oppo devices not connecting to eduroam even with the connect settings and confirmed working authentication, retrying various geteduroam app and manual configs. Symptoms of this include it just working one day and then suddenly stopping working, or only working in Halls and not teaching buildings.

Unfortunately I have not been able to diagnose why aside from that the device does not appear in any eduroam connection log even from the ITSD. The only solution is to **reset all network settings**. *It may be worth digging through installed CA/other certificates and revoking them.*


#### MacOS (and Linux)

- Biggest issue is users not typing password correctly. Using the usercheck tool to make sure they are inputting this correctly, or cut and paste from password manager/temp document is a good diagnosis step (**be aware of security implications**).
- CAT Tool is highly recommended to connect users on MacOS, use either the guest network or hotspot: https://cat.eduroam.org/
	- Accounts **should have local MacOS/Apple Account administrator permissions** otherwise this may not work. When installing, look carefully for the **macOS account/email/password versus the University account/email/password**.

- Can internet be accessed with the current network DNS? Run `dig google.com`. Failures point to DNS issues/incorrectly configured/changed eduroam settings
- Can internet be accessed at all? Run `dig @1.1.1.1 google.com`. Failures point to authentication, connection, VPN/tunnel overrides, or MDM policy. 

Linux commands:
- `nmcli -f IP4 device show <wlp-whatever>`

##### Some websites work but others don't on Mac?
> tags: error code, `DNS_PROBE_FINISHED_NXDOMAIN`, `ERR_NAME_NOT_RESOLVED` `DNS_PROBE_FINISHED_BAD_CONFIG`.

This is likely an issue with **DNS being changed from default/split DNS issues**, or **VPN active** even if none appear open (check background processes).

1. Go to **System Preferences**
2. **then Network**
3. Click **Advanced.** 
4. Click the **DNS** tab
5. Highlight the static DNS number you wan to remove
6. Click the little **- (minus)** sign at the lower left to add a new DNS server
7. Click **OK** and **Apply**
8. For newer Macbooks, go to settings, type IPV4 and set the option to Using DHCP

This can also be checked with the terminal:
Confirm/check DNS server with the command: `scutil --dns | grep nameserver`. There should be 2 DNS servers starting with IP `128.243`.

Run these commands in Terminal to reset DNS to defaults:
1. `sudo networksetup -setdnsservers Wi-Fi Empty`
2. `sudo ipconfig set en0 DHCP`
3. `sudo dscacheutil -flushcache`
4. `sudo killall -HUP mDNSResponder

### Wired/Ethernet connection
Ethernet is not supported, even though there may be ports present, and support was removed from halls of residence (**EXCEPT Florence Boot Hall, where Ethernet may work completely fine across all rooms**) during the summer of 2025.

If some rooms work but others do not, this is unintended (and "keep this quiet" - manger's words not mine!!).

For use in teaching buildings, ethernet is not universally "plug and play". Requests must be sent by a professor to authorise a specific NIC's MAC address at a given port via the selfservice portal (there are exceptions to this, and Ethernet may work fine in some buildings with any device or cable, but this is the official recommndation.)

### In halls
> tags: uon guest, guest network, halls network, UoN-Halls, eduroam in halls, halls eduroam, halls connection

eduroam/wireless in halls can be unreliable due to distance from the AP, interference, and there being many other devices nearby. This is largely expected - WiFi signals have to come FROM the AP and be broadcast back TO it by a weaker device. If the problem is significant, students can raise a self service request or use a WiFi extender plugged into their laptop/device (can be bought for cheap online).

==Ethernet/wired connection: is unfortunately **NOT SUPPORTED IN HALLS except for Florence Boot**; see the Ethernet section above for more details.==

#### For devices that don't support Eduroam
You can register devices that cannot connect to Eduroam via the UoN-Halls network: https://nottingham.campuswifi.net/accounts/Nottingham/device/ or by scanning the qr code below:

![](../../Images/campus_wifi_uon_halls.svg)


## Office & MS Application Suite
> tags: word, excel, access, powerpoint, pptx, docx, xlsx, ms365, copilot, sharepoint


### Online services
#### SharePoint
If users cannot access a SharePoint (Access Denied) for their department, the Software Library, or any other SharePoint site **that they should have access to**, they should submit a ticket with a link to the site. (User groups, especially after recent changes in course/transition from UG to PGT or PGR/campus switch may cause this).



### Windows

#### Organisation has deleted this device

This is because the user is **attempting to sign in to a "work or school account" from Windows Settings**, or selecting **"Allow my organisation to manage this device"** which the University does not allow. 

To fix this:
- Close all Office apps
- From Settings (shortcut: Windows + I) search for "Accounts"
- Select the "Work & School" accounts
- Find any UoN account and remove it
- Open an Office app (Word, Excel, etc.) and re-sign in without selecting "Allow my organisation to manage my device"


### MacOS
- Mac Office License Removal Tool: https://go.microsoft.com/fwlink/?linkid=849815

#### 0x0 unknown error
> tags: 0x0, unknown error, excel, word, edit access, reduced functionality, open documents, editing documents, activate office, doesn't allow editing, contact your administrator

Even if Office has been used in previous years, there may be an issue with "An unknown error has occurred" when signing in. Error message may include "doesn't allow editing on a Mac".

A Microsoft certificate expired in July 2026 so symptoms include previously working but not any more.

1. Identify the version of Office. Word -> About Microsoft Word
2. If the version is **below 16.83, the fix is to update Office**
	- note: standalone Office 2019 is no longer supported
3. Go to Word -> Help -> Check for Updates
	- Look in `/Library/Application Support/Microsoft/MAU2.0/` for the Microsoft AutoUpdate app and run it.
	- If installed via the App Store, check the App Store and update from there.
4. Use the [Office License Removal Tool on https://go.microsoft.com/fwlink/?linkid=849815](https://go.microsoft.com/fwlink/?linkid=849815) to eradicate any and all records. Signing in again regenerates the local records. 
5. Should be resolved by now, but stale records can be removed in Spotlight -> Keychain Access -> search for "Office" and removal of: `Microsoft Office Identities Cache 3`, `Microsoft Office Identities Settings 3`, `Microsoft Office Ticket Cache`.
6. Reinstall Office via https://support.microsoft.com/en-us/office/lifecycle/officeinstall/uninstall-office-for-mac


## University Services

### LLR
> tags: LLR, laptop loan, loaned laptop, rent laptop, free supplied laptop

All laptops loaned come with full admin rights. There is a laminated sheet on the LLR laptop bag loan that contains the user account password. 

Repairs: need to be booked; software repairs free; hardware repairs charged at-cost based on the component(s) that need replacing.

### MFA
> tags: 2fa, reset, new phone

MFA can be reset by following these steps:
1. Confirming their identity. This can be done with a physical document - passport, driving license, or student ID card.
2. Verify the full name, student ID number and username.
3. Ask a Senior SBA confirming an ID check has been done alongside these 3 details.

It is recommended to use Microsoft Authenticator, but other authenticator apps can be used with such as KeePassXC, Bitwarden, Authy etc.

### SEAtS
> tags: attendance, qr, seats, monitoring

After completing all registration steps, the SEAtS system may take up to 3 (working) days to sync and allow login/timetable/etc.

Escalation with niche SEAtS queries can be done by contacting SSBA/ITSD with the ID of the student and asking if it can be checked.

#### Error: access_denied
This is a common error, particularly at the start of session when students have just joined. There are 2 reason:
1. The system takes 3 working days to sync.
2. Students have not completed their online AND in-person registration. **Many students believe they have completed this, particularly online registration, but haven't.** Before advancing with this issue, check the Online Registration tile in NottinghamHub (campus.nottingham.ac.uk) and help them complete this. (then wait for the 3 days to elapse.)


#### Error: no tenant identifying information found
This is a common issue when **students autofill their email and password**. Manually typing it out will fix this!

### GitLab
The CS department has 2 gitlab instances: `git` and `projects` as subdomains on `cs.nott.ac.uk`. The `git.cs.nott.ac.uk` can only be accessed by staff HOWEVER is the one that appears when searching for UoN gitlab. Once a sign in is attempted on `git`, students will not be able to sign in to `projects` without clearing **BOTH** caches and cookies for `login.microsoftonline.com` and `*.cs.nott.ac.uk`!


### ExamSys

ExamSys papers may be given to students by lecturers outside of exam season so it is normal to have requests for this.

#### Everything works but ExamSys!
> tags: access denied, authentication with examsys has failed

If the user is getting "Access denied" with a message saying "Authentication with ExamSys has failed" and nothing to do with an IP block (*this is for when accessing the main ExamSys server, not the specific lecturer's exam*) then this is a known weird error - **resetting the password on itaccounts usually fixes this issue.**


### Account

#### Security lockout
> tags: security lockout, locked, lock, account locked

An account lock means there has been suspicious activity (most commonly, password inputted wrong a lot on sensitive pages e.g. itaccounts). To resolve this, an valid ID check must be carried out, with the same details as an MFA reset (confirming Student ID, username, full name) and message a Senior SBA/ITSD to clear the lockout. 

## SBA Tools
### Usercheck
#### Novell (Nottingham tree) - user not found
If everything else passes but this shows not found, then the student (likely) started their studies in China or Malaysia and should not be an issue in isolation.

If there are other issues, e.g. accessing Outlook, with this present, then raising a ticket (http://selfservice.nottingham.ac.uk/) should be done. 

#### Failed to check password (unwilling to perform)
If you are inputting in the user password into the usercheck and **some, but not all** services come back with a `? Error: Failed to check password (unwilling to perform - please try again)` then this may be any number of issues - message a senior/manager who will forward this to ITSD alongside the username.

### Raise a ticket
This can be done on https://uniofnottm.saasiteu.com/ or by scanning the QR code below.

![QR preview](https://public-api.qr-code-generator.com/v1/create/extended?image_format=PNG&image_width=300&qr_code_text=https%3A%2F%2Funiofnottm.saasiteu.com%2F&foreground_color=%23000000&background_color=%23FFFFFF&frame_name=no-frame)


### List of OS given help to
(this is just a personal list and not the officially supported OS list)
- Windows
- MacOS
- Linux/Ubuntu
- iOS
- iPadOS
- GrapheneOS
- Void Linux