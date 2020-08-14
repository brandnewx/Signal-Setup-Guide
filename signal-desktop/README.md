# Signal Desktop
This guid is written by using Signal Desktop on branch Master version 1.30.0-beta.4

## Requirement
* NVM 12.4.0

## How To
1. Install requirement

on MacOS, Install xcode
```
xcode-select --install # Install Command Line Tools if you haven't already.
sudo xcode-select --switch /Library/Developer/CommandLineTools # Enable command line tools
```

On Win7, Install .Net 4.5.1 & Windows SDK 8.1 & Windows Build Tools
```
npm install --global --production --add-python-to-path windows-build-tools
```

On Linux, Install python, gcc, g++, make
```
sudo apt-get install python, gcc, g++, make
```

2. Clone signal-desktop

3. Mount signal desktop directory
```
cd Signal-Desktop
```

4. Install yarn
```
npm install --global yarn
```

5. Install & build with yarn
```
yarn install --frozen-lockfile
```

6. Generate final JS & CSS
```
yarn grunt
```

7. Generate full-set icon
```
yarn icon-gen
```

8. Build with webpack
```
yarn build:webpack
```

9. You can test with
```
yarn test 
```

10. Start the app
```
yarn start
```

11. To connect to own production server, `create local-development.json`, the value is the same as `production.json` but without `updateEnabled`.
```
{
  "serverUrl": "https://domain.com",
  "cdnUrl": "https://cdn-domain.com",
  "serverTrustRoot": "public-key-generated-in-signal-server-step-4",
  "updatesEnabled": true
}
```

## Using own Server
1. Update `config/deafult.json`, set serverUrl & cdnUrl by using your Server URL & your CDN url, **don’t include trailing slash on serverUrl and cdnUrl**.

2. Update `config/default.json`, set certificateAuthority using CA’s SSL Certificate.

3. Update `config/default.json`, set serverTrustRoot using your CAPublicKey (Also used in android as UNIDENTIFIED SENDER TRUST ROOT).

4. Update `js/modules/web_api.js`, find functions called `getAttachment` and `putAttachment`, then replace `${cdnUrl}/attachments/${id}` with `${cdnUrl}/` **(Do this if you do the same in android client)**.

5. Still on the same functions, set a default value for `certificateAuthority` variable (see below) **new line in your certificateAuthority needs to be formatted to “\n”**.

**change this**
```
...
certificateAuthority,
...
```


**to this**
```
...
certificateAuthority: "-----BEGIN CERTIFICATE----- ... -----END CERTIFICATE-----\n",
...
```


6. `yarn generate`

7. `yarn build`

8. `yarn start`


## FAQ
Q: How could I get certificate authority?

A: I called it the certificate of the certificate issuer. You can try browsing a https web using chrome, click on lock pad beside the URL address bar, then click on "Certificate (Valid)", you will see the top most & orange certificate, that is what you need, drag it to your desktop to save it.



Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@brandnewx 
signalapp
/
Signal-Desktop
303
6k1.1k
Code
Issues
1.1k
Pull requests
6
Actions
Projects
Security
Insights
You’re making changes in a project you don’t have write access to. We’ve created a fork of this project for you to commit your proposed changes to. Submitting a change will write it to a new branch in your fork, so you can send a pull request.
Signal-Desktop
/
CONTRIBUTING.md
 

Spaces

2

Soft wrap
1
# Contributor Guidelines
2
​
3
## Advice for new contributors
4
​
5
Start small. The PRs most likely to be merged are the ones that make small,
6
easily reviewed changes with clear and specific intentions. See below for more
7
[guidelines on pull requests](#pull-requests).
8
​
9
It's a good idea to gauge interest in your intended work by finding the current issue
10
for it or creating a new one yourself. You can use also that issue as a place to signal
11
your intentions and get feedback from the users most likely to appreciate your changes.
12
​
13
Once you've spent a little bit of time planning your solution, it's a good idea to go
14
back to the issue and talk about your approach. We'd be happy to provide feedback. [An
15
ounce of prevention, as they say!](https://www.goodreads.com/quotes/247269-an-ounce-of-prevention-is-worth-a-pound-of-cure)
16
​
17
## Developer Setup
18
​
19
First, you'll need [Node.js](https://nodejs.org/) which matches our current version.
20
You can check [`.nvmrc` in the `development` branch](https://github.com/signalapp/Signal-Desktop/blob/development/.nvmrc) to see what the current version is. If you have [nvm](https://github.com/creationix/nvm)
21
you can just run `nvm use` in the project directory and it will switch to the project's
22
desired Node.js version. [nvm for windows](https://github.com/coreybutler/nvm-windows) is
23
still useful, but it doesn't support `.nvmrc` files.
24
​
25
Then you need `git`, if you don't have that yet: https://git-scm.com/
26
​
27
### macOS
28
​
29
1.  Install the [Xcode Command-Line Tools](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/).
30
2.  Ensure [git-lfs](https://github.com/git-lfs/git-lfs/wiki/Installation) is installed. You'll need it to to checkout and install the node requirements. Install with `brew install git-lfs`
31
​
32
### Windows
33
​
34
1.  **Windows 7 only:**
35
    - Install Microsoft .NET Framework 4.5.1:
36
      https://www.microsoft.com/en-us/download/details.aspx?id=40773
37
    - Install Windows SDK version 8.1: https://developer.microsoft.com/en-us/windows/downloads/sdk-archive
38
1.  Install _Windows Build Tools_: Open the [Command Prompt (`cmd.exe`) as Administrator](<https://technet.microsoft.com/en-us/library/cc947813(v=ws.10).aspx>)
39
    and run: `npm install --vs2015 --global --production --add-python-to-path windows-build-tools`
40
​
41
### Linux
42
​
43
1.  Pick your favorite package manager.
@brandnewx
Propose changes
Commit summary
Update CONTRIBUTING.md
Optional extended description
Add an optional extended description…
 
© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
