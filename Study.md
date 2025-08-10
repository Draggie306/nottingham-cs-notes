
STUDY Brief

The site must allow users to view, sort by and filter exam scripts, NEAs, personal statements. Users must be able to quickly search by subject, tier, exam board, grade obtained etc. Users must be able to create an account and upload their own resources.

STUDY Comprehensive
```
REQUIREMENTS

1. PAGE STRUCTURE/CONTENT. 
1.1 ALL PAGES: All site pages contain a header with the clickable logo on the left (hovering over gives a dropdown to all iBaguette projects). On the right is the accounts menu, which is an icon that is clickable that shows "manage account". 
There will also be (an)other button(s) like "Search" in the top header.

1.2. LANDING PAGE: The landing page should show a bold "mission statement" with an icon/logo to the left (desktop)/below (mobile). It should read "The best place for the best resources.". This occupies ~1/3 of the vertical height and 1/2 on mobile. Immediately below this is a distinc section with text on the top-left of the section that reads "Featured resources". The section, again 1/3 of page height, contains a carousel (see 1.3) of featured resources.

1.3. RESOURCE CAROUSEL: A resource carousel contains around ~5 (lower on mobile) resources. 

1.3.1 RESOURCE PREVIEW: A resource preview must have rounded corners, may have a yellow star label containing text along the top (for standout resources), may have a small preview of the content, and must have a title "synopsis" of the content. "Tags" should be displayed in rounded, grey pill containers: it must have the tier, must have the subject, may have the grade (if known). Below this, it may have the author's name. 


1.4. RESOURCE PAGE: A resource page is one dedicated to the resource. Along the top (below the header) 


2. UPLOAD FUNCTIONALITY
2.1. AUTHENTICATION: The user must be required to log in to access the pages associated with account and resource management.

2.2. USER PAGE: The user shall have a sidebar with options including "Account Management" and "Resource Management". The main user page site upon logging in must show these and default to "Resource Managemen"

2.3. RESOURCE MANAGEMENT PAGE: Below a top "Search" bar, there shall be an ordered list of all the user's uploaded resources, vertically descending on the main page's content.
2.3.1 SORT: The user shall be able to search for a specific selection of their resources, including by name and any tags.
2.3.2 SELECTION: The user shall be able to select any number of resources on the page.
2.3.3 EDIT OPTIONS: The user shall see a menu with different options available for all selected resources. This menu shall include: "Delete", "Make Private/Public", "Change Settings"

3. DEFAULT API
3.1. ALL PAGES: All site pages that do not require an account with dynamic content shall be routed through `study-api.ibaguette.com`

4. AUTHENTICATED API
4.1. ACCOUNT PAGES: All site pages that require account access shall be on `/account/<pageName>`.

4.2. ACCOUNT SYSTEM: All account requests, including register, login, delete, update, shall be routed through `accounts-api.ibaguette.com`. Ideally



5. BACKEND

# NONFUNCTIONAL REQUIREMENTS
1.1.1 All public pages will be on the website `study.ibaguette.com`
1.1.2 Developer testing pages will be on the website `stage-study.ibaguette.com`
1.1.3 Beta testing pages will be on the website `beta-study.ibaguette.com`
1.1.4 All developer and beta testing pages will have an authentication wall before viewing the content.

1.2.1 All user content (not site layout) shall be fetched dynamically via a JSON API request.
1.2.2 Featured resources shall be fetched by an API request to endpoint `/featured`, returning 

2.1.1 The user shall be required to enter an email and password to log in.
2.1.2 The password shall be validated to contain a capital letter and symbol.
2.1.3 The password shall be checked with a pwned API to disallow any public/breached passwords.
2.1.4 The password shall be salted and stored securely in a database.

2.2.1 The maximum file size allowed shall be 100MiB.
2.2.2 

4.1.1 The rate limit for the authenticated API shall be 20 requests per IP per minute.

# USER STORIES

1. As a student, I want to search for all A Level OCR Computer Science Paper 1 exam scripts that received a grade B or higher so I can see exemplar answers.
2. As a resource author, I want to upload my EPQ so I can have my name linked to my work online.
3. As a contributor, I want to change the visibility of all GCSE resources I have uploaded to private so that my friends can't find them.
4. As a developer, I want to review all recent uploads so I can check if any need extra information or should be published directly.

```

Change cache to a flag here:

![](https://cdn.sa.net/2024/05/16/hqs2dreoxfz5Wti.png)

