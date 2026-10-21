DISCLAIMER: This was made before other SB info sheets were shared. I know there are others being shared but this one is an adaptation of my [original notes](https://notes.oling.dev/Misc/Jobs/Smart%20Bar%20Notes) from last year.

This is designed to be completely searchable with CTRL + F, and shareable with other SBAs.

### Admin
Fill in after each interaction: [SB staff page](https://forms.cloud.microsoft/pages/responsepage.aspx?id=7qe9Z4D970GskTWEGCkKHrD7NcXXkf9CvFlZEZD7gIVUM0lRVklGODQ4OExFUko2TzRINTBVWjdORCQlQCN0PWcu)

Customer survey: [Customer survey](https://forms.office.com/pages/responsepage.aspx?id=7qe9Z4D970GskTWEGCkKHrD7NcXXkf9CvFlZEZD7gIVUNkZYUDdZV0dVUTQ4WVhUTzVKOTNZS0NQMyQlQCN0PWcu)
![Pasted image 20251210134426](../../Images/Pasted%20image%2020251210134426.png)


IT Service Desk: https://www.nottingham.ac.uk/dts/help/it-support.aspx

https://uniofnottm.saasiteu.com/Modules/SelfService/



## Internet access

### Eduroam
> tags: connection, wifi, wi-fi, internet, signal, strength, disconnecting, Chromebook 

- Eduroam needs the **full university account email address** (not username) and password.
- The correct configurations for all devices is available at https://www.nottingham.ac.uk/dts/connect-to-wifi.aspx

#### Windows
- Many devices say "Couldn't connect to this network". A typical fix is to forget the network and sign in again.
- A good way to debug this is to sign in to your own account (**remember to forget immediately afterwards!**) to determine if this is a laptop/hardware issue, or an account issue.
	- If your own credentials do not work, then check for 

#### MacOS (and Linux)

- Biggest issue is users not typing password correctly. Open Notes app and copy and paste from plaintext where possible.
- CAT Tool is highly recommended to connect users on MacOS, use either the guest network or hotspot: https://cat.eduroam.org/
	- Accounts **should have local MacOS/Apple Account administrator permissions** otherwise this may not work. When installing, look carefully for the **macOS account/email/password versus the University account/email/password**.

- Can internet be accessed with the current network DNS? Run `dig google.com`. Failures point to DNS issues/incorrectly configured/changed eduroam settings
- Can internet be accessed at all? Run `dig @1.1.1.1 google.com`. Failures point to authentication, connection, VPN/tunnel overrides, or MDM policy. 

Linux commands:
- nmcli -f IP4 device show \<wlp-whatever\>

##### Some websites work but others don't?
> tags: error code, `DNS_PROBE_FINISHED_NXDOMAIN`, `ERR_NAME_NOT_RESOLVED` `DNS_PROBE_FINISHED_BAD_CONFIG`.

This is likely an issue with **DNS being changed from default**, or **VPN active** even if none appear open (check background processes).

Confirm/check DNS server with the command: `scutil --dns | grep nameserver`. There should be 2 DNS servers starting with IP `128.243`.

Run these commands in Terminal to reset DNS to defaults:
1. `sudo networksetup -setdnsservers Wi-Fi Empty`
2. `sudo ipconfig set en0 DHCP`
3. `sudo dscacheutil -flushcache`
4. `sudo killall -HUP mDNSResponder

#### In halls
> tags: uon guest, guest network, halls network, UoN-Halls


- You can register devices that cannot connect to Eduroam via the UoN-Halls network: https://nottingham.campuswifi.net/accounts/Nottingham/device/ or scan the qr code below:

![](../../Images/campus_wifi_uon_halls.svg)


### Ethernet
Ethernet is not supported, even though there may be ports present, and support was removed from halls of residence (**EXCEPT Florence Boot Hall, where Ethernet may work completely fine across all rooms**) during the summer of 2025.

If some rooms work but others do not, this is unintended (and keep this quiet!).

## Office Application Suite
> tags: word, excel, access, powerpoint, pptx, docx, xlsx, ms365, copilot



### MacOS

Utilities:
- Office License Removal Tool: https://go.microsoft.com/fwlink/?linkid=849815

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



## Tools


### Usercheck
#### Novell (Nottingham tree) - user not found
If everything else passes but this shows not found, then the student started their studies in China or Malaysia. Should not be an issue.

### Raise a ticket
This can be done on https://uniofnottm.saasiteu.com/ or by scanning the QR code below.

![QR preview](https://public-api.qr-code-generator.com/v1/create/extended?image_format=PNG&image_width=300&qr_code_text=https%3A%2F%2Funiofnottm.saasiteu.com%2F&foreground_color=%23000000&background_color=%23FFFFFF&frame_name=no-frame)


- Windows
- MacOS
- Linux/Ubuntu
- iOS
- iPadOS
- GrapheneOS