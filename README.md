# sdapi

Python script that interacts with SlamData's security API

## Assumptions

Using this Python script comes with the following assumptions:

* You understand this is open source software.  There is no
  guarantee of ANY kind.

* You should *NOT* use this in your production environments,
  it is only meant for testing and to familiarize yourself with
  the SlamData API.

* This will only work with SlamData Advanced Edition.

* You have already configured SlamData Advanced OIDC providers

## Installation

Clone this repository:

```
git clone https://github.com/damonLL/sdapi.git
```

Install the "Requests" Python module:

```
pip install requests
```

## Execution

Simply execute it by typing ```./sdapi``` on the command line.


## Setup

The first time that sdapi is executed, or if the `sdapi.json`
file is not found, it will ask 3 questions.

1. The base URL of the SlamData web application

	If you installed locally this is most likely something
	like ```http://localhost:20223``` or some other port.

2. The email address of a user that belongs to the
   administrators group.

	This group was created when you originally ran the `bootstrap`
	function when installing SlamData Advanced Edition.

3. A Bearer Token

sdapi runs on the assumption that you have obtained a bearer
ID, and it passes this bearer ID along for authorization.
The Bearer token needs to be associated with the email
address from step 2.  

As an example, if you have created a Google Oauth 2.0
Open ID Provider and stored it in the quasar-config.json
file, then you can relatively easily create this bearer token.

1. Go to the Google OAuth 2.0 playground https://developers.google.com/oauthplayground

2. Click on *Step 1 Select & Authorize APIs*

3. Below the list of APIs, enter the string ```openid email``` and click *Authorize APIs*

4. Authenticate with Google based on the email address you specified above.

5. You'll be taken to *Step 2 Exchange authorization codes for tokens*

6. Click the *Exchange authorization code for tokens* button

7. Copy the ```id_token``` value (it's really long, scroll to the right)

8. Use this value for the sdapi script

## Notes

The script in its current form is very rough, could certainly be unstable,
and does not provide much error checking.  That being said, it makes it
very easy for a SlamData administrator to call all of the
SlamData security APIs through a simple menu system.

Responses will be shown from the calls it makes.  These responses typically
include an HTTP response code, sometimes a JSON response as well.  When
possible it prints both.

Whether a call succeeds or fails, you'll be shown the HTTP response code.
It is up to you to understand these codes (i.e. 403 Forbidden, 404 Not Found, etc)

You can also find out more about the Security APIs by visiting the
SlamData Administration Guide

http://docs.slamdata.com/en/v3.0/administration-guide.html#additional-apis

