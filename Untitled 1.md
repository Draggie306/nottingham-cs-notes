Compared to other institutional app requirements, this was surprisingly easy to follow. Device environment: Windows 11 Pro 25H2 Version 10.0.26200 Build 26200 

- From the start, there is a clear flow that makes sense. Enter email -> get an email with the code -> download the application.
- I like how the unique code was automatically entered in the Sophos account sign-up flow, saving time.
- I like how there was no need to sign into my account when opening the Sophos desktop app the first time, as it linked to the web account automatically.
- I did not encounter any Windows-level issues or UAC control prompts when installing the app.
- The app requiring the Windows account password to then access the web portal seems a bit odd, as I just created the Sophos account. But nonetheless it worked well and seems to communicate between Windows and the web view without issue.
- Not entirely sure how I feel about having a root level AV that supports remote management - what if someone gets into my online account? 2FA may help here.
- After ~20 minutes, I pressed "Manage" via a toast popup when it detected a threat. However it then opened another login window on login.sophos.com (different to the my.sophos.com to access the management UI) which said my credentials were incorrect (despite autofill). Upon pressing "Manage" again I was immediately let into the Sophos home management UI without issue.
- When pressing "More info" on a detected threat, it redirects to a website that is just 404'd and does not provide any information: https://www.sophos.com/en-us/threat-center/threat-analyses/viruses-and-spyware.aspx


- If useful, this is a recording of how I navigated through, signed up and installed it: [Desktop 2026.10.09 - 15.07.11.01.mp4](https://uniofnottm-my.sharepoint.com/:v:/g/personal/psyol1_nottingham_ac_uk/IQABNHbK_8HwQ7C8XgW0QAcdAVWKxKVlUvkaw_mKN6rxhQ8?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=OrENxW)