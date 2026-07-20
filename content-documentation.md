---
layout: page
title: Content Documentation
description: Documentation for Content TAs on website updates, assignment generation, and release workflows.
permalink: /content-documentation/
nav_exclude: true
---

# **Content Documentation**

*Data 8, Summer 2026*

*Written by Richard Villagomez*  
*Contributions from Ella Guzman, Brandon Su, Isaac Chung and others*

{:.no_toc}

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Cloning Repositories

* Content TAs will have access to 3 repositories
  * **su26**: for making changes to the website
  * **assignments_new**: for making new assignments per semester
  * **materials-su26**: student-facing repo for all assignments
    * create git puller links with this repository
* It is recommended that you make a folder (called "data8") that contains folders with each of these repositories

## Website Cloning

1. Install Homebrew:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. [Set-up](https://github.com/berkeley-cdss/berkeley-class-site) (README)
   1. Follow setup instructions in the README, under "Local Install"
3. Install jekyll and ruby following [these steps](https://jekyllrb.com/docs/installation/macos/)
   1. If you already have ruby installed, simply run `gem install jekyll`
4. `bundle install`
   1. If you get an error like: `Your Ruby version is 3.4.1, but your Gemfile specified 3.3.9`
      1. Install rbenv: `brew install rbenv ruby-build`
      2. Run `rbenv install 3.3.9`
5. To view website locally, run `bundle exec jekyll serve`!

## Website Updates

* Always git pull first (to avoid merge conflicts!!!): `git pull`
* Make updates to the Home Page
  * Adding links to Homeworks, Projects, Labs
* Nice shortcuts:
  * `cmd+f:` Find text in current file
  * `cmd+shift+f:` Find text in ALL files
  * `cmd+p`: Look for file name
* *For Website Suggestions*: create Website Suggestions Doc
* *For reference:* [Seamless Learning Web Accessibility a11y](https://docs.google.com/presentation/d/1X05oNONc3sxL3vcmUUKTCO7tYpAMiU1LNhiL_dHQRf0/edit#slide=id.g24f26c19f5f_0_141)
* To view local copy of website: `bundle exec jekyll serve`

## Assignments Repo Setup

1. Install **python3.10** by following the [documentation](https://wiki.python.org/moin/BeginnersGuide/Download)
   1. *Note*: I (Richard) ran into issues using both python 3.14 and python 3.9. To check your python version, run `python3 --version`
   2. For Mac, download from [python.org](https://www.python.org/downloads/macos/)
2. Clone the [assignments_new](https://github.com/data-8/assignments_new) repository
   1. Open up a terminal on your computer
   2. Go to data8 folder
   3. Type in `git clone <repository-url>`
      1. Fill in the URL by going to the repository page on GitHub → Click the green Code button → Select the HTTPS url
3. Navigate to your folder: `cd assignments_new`
4. Open the folder on a code editor such as Visual Studio Code
5. Create a new file called **.env**
   1. Paste this in:

```
USERNAME = #fillwithgithubemail
PASSWORD = #fillwithgithubpassword

# fill with path to regrade-creds.json
# note: I believe this is not needed for Pensive setup
REGRADE_CREDS = "/Users/richardvillagomez/Documents/data8/assignments_new/regrade-creds.json"
```

6. Open up a terminal
   1. Run these commands to create a **virtual environment**, activate it, and install requirements
      1. `python3 -m venv env`
         1. or `python3.10 -m venv env`
      2. `source env/bin/activate`
      3. `pip install -r requirements.txt`
7. Update `compose.sh` file for current semester
   1. Update `SEMESTER` to the current semester, i.e. `"fa26"`
8. Update `copy.sh` file for current semester
   1. For `SRC`, update to the current semester, i.e. `SRC="semester_assignments/su26/$ASSIGNMENT_TYPE/$ASSIGNMENT/student"` → `SRC="semester_assignments/fa26/$ASSIGNMENT_TYPE/$ASSIGNMENT/student"`
   2. For `DEST`, update to the current semester, i.e. `DEST="$HOME/Desktop/data8/materials-su26/$ASSIGNMENT_TYPE/$ASSIGNMENT"` → `DEST="$HOME/Desktop/data8/materials-fa26/$ASSIGNMENT_TYPE/$ASSIGNMENT"`
9. In `generate.py`, update `SEM` to current semester

## Notebook Generation

1. Open up **assignments_new**
2. Go to the **semester_components** tab to go to the assignment you want to edit
   1. The **materials** file has all the notebooks that are being combined for that assignment
   2. The **preamble** file has the intro of the notebook
   3. Check all of these to make the updates necessary for the semester
      1. Check all links
      2. Check all deadlines
      3. Add borders:
         1. Thick border:

```html
<hr style="border: 5px solid #003262;" />
<hr style="border: 1px solid #fdb515;" />
```

         2. Thin border (three dashes):

```html
---
```

3. Once you finished making the edits:
   1. Generate notebook/autograder/solution notebook: `./generate.sh lab01`
      1. Confirm that all test cases passed
      2. If you run into this error, double-check that all test cases have been specified in the spec:
4. Git add/commit/push to assignments_new
   1. If you want to [get rid of `.DS_store`](https://stackoverflow.com/questions/9750606/git-still-shows-files-as-modified-after-adding-to-gitignore)
5. Copy over to materials-su26 folder: `./copy.sh lab01`
   1. *Alternatively, manually copy materials from "student" folder and paste into respective materials-su26 folder*
6. Git add/commit/push to materials-su26 so students can see the assignment!

## Assignment Review

1. Review the assignment and [solutions](https://drive.google.com/drive/folders/1IQZubyS-lkmnLE0RrzWYHJt0J-UzazHW?usp=drive_link).
2. Download and prepare the assignment:
   1. Download the assignment zip file named [assignment].zip (Richard will send them for each assignment)
      1. Go to your [DataHub](https://data8.datahub.berkeley.edu/hub/) directory and upload the zip file inside materials-su26.
   2. Open a terminal
   3. Unzip the file
   4. Open assignment.ipynb where assignment corresponds to the proper assignment ie. lab01
3. Try to "break the autograder" by considering edge cases we may have missed.
   1. Suggest any additional test case
   2. Ensure all links are working properly and dates are updated
4. Propose changes: write down the changes from step 3 and proposed corrections for errors, grammatical fixes, clarifications for confusing instructions, or adding useful textbook links. Make these suggestions in their respective thread.

## Assignment Release

1. Update website with gitpuller link of assignment (watch [gitpuller_links.mov](https://drive.google.com/file/d/1oPeRJYbLtZ0LU32-T9Cm579dt12NOhrj/view?usp=sharing) for reference!)
2. Post on Staff Ed
   1. Make an announcement that Assignment will be posted
   2. Provide link to solution notebook
   3. Write a list of changes made to this semester's notebook
3. Post on Student Ed
   1. Use last semester as a guide for what the Ed post should look like
   2. Assignment releases need to be an **ANNOUNCEMENT** check all the boxes at the bottom BEFORE posting
      1. **Note**: When you click the "Email" checkbox, just wait after you click the Post button. It takes a while to send all the emails to the students. **Don't press Post again!!**
         ![Ed announcement checkboxes]({{ site.baseurl }}/assets/images/content-documentation-ed-announcement.png)
      2. Make sure to create new question threads as a **POST** and link it to the main assignment post

## Upload + Test Autograders

* Watch [Autograder_Tutorial.mp4](https://drive.google.com/file/d/1S0yE4sTO2X1YtenKlowsL2uBGrMRscXj/view?usp=sharing) :0

## Regrades

* Watch this [video](https://drive.google.com/file/d/1Oi4sRvcmq1XDIHj1PCoPRSNiDmV0HxBs/view?usp=sharing) :0

* 'Invalid JWT Signature' - If running into this error, you may need to obtain new credentials for the Google Cloud API (i.e. update regrade-creds.json)
  * Source 1: [Google Sheets Grade Override — Otter-Grader documentation](https://otter-grader.readthedocs.io/en/latest/plugins/builtin/grade_override.html)
  * How to set up the regrade-creds.json: [Authentication — gspread 6.1.2 documentation](https://docs.gspread.org/en/latest/oauth2.html#enable-api-access)

## Important Videos

* [Generate Gitpuller Links](https://drive.google.com/file/d/1oPeRJYbLtZ0LU32-T9Cm579dt12NOhrj/view?usp=sharing)
  * Gitpuller link → copies code from a repo and gives you a copy yourself (for jupyter notebooks)
  * [Nbgitpuller](https://nbgitpuller.readthedocs.io/en/latest/link.html)
    * https://datahub.berkeley.edu/ is the jupyterhuburl
    * Copy repo to work on for Git repo url
    * Branch should be main
    * File to open
      * Ex: hw/hw01/hw01.ipynb
    * Using nbgitpuller is a Google extension
    * Go to the folder and the open extension to generate the link
  * **Alternatively, if paths are the same just update semester in URL** (i.e. su26 → fa26)
* [Uploading the autograder](https://drive.google.com/file/d/1X6ueZh_9cL8XgcJdvGUy-pOT-8wevmjt/view?usp=drive_link)
  * Click assignment
  * Configure autograder
  * Replace autograder with a more updated one → Pick zip file
  * Then press update autograder
* [Testing the autograder](https://drive.google.com/file/d/1aEBi0ymq1lWY6XfE-2Y1cFH3dhdhOS1k/view?usp=drive_link)
  * Once autograder has successfully built:
    * Check the very bottom for success
    * Click **test autograder** and upload the solutions notebook
    * Regrade request links will also be there in a spreadsheet
    * Fill in **assignment id** and the **number of points** to change to
* [Changing auto grader scores](https://drive.google.com/file/d/11WZfNXD29EAUnR7hZVdG2TLCuMEe07bG/view?usp=drive_link) (grading will use this, but it's nice to know)
  * Rerun autograder on Pensive and it will change the score based on the spreadsheet

## Contacts

* **[Silas Santini](mailto:silascs@berkeley.edu)**: Your first point of contact when things break and you're not sure what to do. You can message them in the slack channels UC Tech, DS Crosswords, or Otter-Grader
* **Otter-Grader Slack** & **Chris Pyles** ([chrispyles.99@gmail.com](mailto:chrispyles.99@gmail.com)): Whenever you run into issues regarding the autograder and generating the otter notebooks.
* **Richard Villagomez** ([rvill04@ucsc.edu](mailto:rvill04@ucsc.edu)): Summer 2026 content lead; always happy to help :]
