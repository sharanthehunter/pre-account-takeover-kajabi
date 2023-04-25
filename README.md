# pre-account-takeover-kajabi

Vulnerability name : Misconfigured oauth leads to Pre account takeover

Weakness :  Business Logic Errors

Description :

While testing kajabi I have noticed that users can use SSO to create and login to kajabi accounts. Now there are two ways of registering into kajabi
By email registration (without verification)  and by signing in using google SSO (OAUTH LOGIN).
Now here Kajabi has a weak auth verification which does not check if a previous account was created with the same email when we use Google to login to our accounts. SO basically what it means is that someone can register using the unregistered victims account. After that, the victim will log in using the OAuth. in this case, the verification process is bypassed and the attacker can log in using the password after that.

1. In some cases, After victim login with sso , the attacker session (logged in with password will be deleted) and the account with sso only remains
But here that also not followed.

Steps to reproduce :

1. Go to this url https://communities.kajabi.com/

![image](https://user-images.githubusercontent.com/84071887/234295748-b372b26f-084d-413c-bfa1-1c29a5b03adb.png)

2. You will see the login page . Enter VICTIM mail address and password to create an account.
3. And you will be successfully logged in to the account using the victim email address.
4. Update some details in the settings page ( upload profile picture )
5. Now open another browser and navigate to the page , and go to login page.
6. Click continue with google SSO option to login.
7. You will be successfully logged in to the same account.
Account takeover was done successfully !!!

For Verification upload some details in the Browser1(log in using email address) and save. Now check the Browser2(login in using Google SSO) and refresh it and you will see the updated details.
  
Fix :
Either don't let the user enter with oauth when there's already another account created with the same email or let the user enter but let him know someone else has already created an account and if it was him or not then ask him to change the password.
  
Impact
Only one thing we need here and that is an email address. Just by knowing that we can take over the victim's account so the impact here is quite high. Imagine an email address is something you can even get if you ask so it's not a hard task. But since the oauth does not authenticate the real user, attackers can easily take over the account.
  
  POC VIDEO ATTACHED DRIVE LINK  =   https://drive.google.com/file/d/1pWIyhiaI9i2aQ6Lo1wFNPxKLXHKaNK4B/view?usp=share_link

References :
1. https://hackerone.com/reports/1074047
2. https://hackerone.com/reports/740989


REPLY FROM KAJABI:

Hello,

Thank you again for providing us with your disclosure. Based on our evaluation, we would like to reward you with Kajabi Swag for this finding. Please let us know your DOB, and what name and address that you would like this sent to.

Please let us know if you have any questions or any other vulnerabilities you would like to disclose.

Thanks,
Information Security Team
Kajabi, LLC



