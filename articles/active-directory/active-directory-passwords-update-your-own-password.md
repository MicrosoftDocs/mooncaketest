---
title: How to update your own password using Azure Active Directory| Azure
description: Learn that ways you can register for password reset, how to change your password, and how to reset your own password in case you ever forget it.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand

ms.assetid: 7ba69b18-317a-4a62-afa3-924c4ea8fb49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
wacn.date: ''
ms.author: joflore
---

# How to update your own password
If you are unsure how to manage your work or school account password, you've come to the right place! Read below to learn how to perform common steps, like changing a password, resetting a password, or registering for password reset.

- [**How to change your password from Office 365**](#how-to-change-your-password-from-o365)
- [**How to change your password from the access panel**](#how-to-change-your-password-from-the-access-panel)
- [**How to reset your password**](#how-to-reset-your-password)
- [**How to unlock your account**](#how-to-unlock-your-account)
- [**Common problems and their solutions**](#common-problems-and-their-solutions)

## How to change your password from the access panel
Follow the steps below to change your work or school account password from the [Access Panel](https://login.partner.microsoftonline.cn). If you have forgotten your password and want to reset it, follow the steps [here](#how-to-reset-your-password).

1. Sign into https://login.partner.microsoftonline.cn with your work or school account.
2. Click the **profile** tab.
3. Click the **change my password** tile on the right-hand side of the screen.
4. Type your old password, and then type a new password and confirm it.
5. Click **Submit**.

   Run into a problem changing your password?  Read about [common problems and their solutions](#common-problems-and-their-solutions).

## How to reset your password <a name="how-to-reset-your-password"></a>
Follow the steps below to reset your work or school account password from any work or school account sign in screen.

> [!IMPORTANT]
> This feature is only available to you if your admin has turned it on. If it's not turned on, you will see a message indicating your account is not enabled for this feature.  You can use the "contact your administrator" link in this case to get in touch with your admin to unlock your account.
>
> If your admin has enabled you for this feature, you are required to sign up before you can use it. You can do that here: http://aka.ms/ssprsetup.
>
>

1. On any work or school account sign-in page, click the "can't access your account?" link, or navigate to https://passwordreset.microsoftonline.com directly.

    ![][110]

2. On the "who are you?" page, enter your work or school account ID and prove you aren't a robot by passing the CAPTCHA challenge.

    ![][111]

3. Click the "next" button.
4. Choose an option to reset your password. Depending on how your admin has configured the system, you might see one or more of the following choices:

   - **Email my alternate email** - sends an email with a 6-digit code to either your **alternate email** or **authentication email** (you choose).
   - **Text my mobile phone** - texts your phone with a 6-digit code to either your **mobile phone** or **authentication email** (you choose).
   - **Call my mobile phone** - calls your **mobile phone** or **authentication phone** (you choose) - press the *#* key to verify the call.
   - **Call my office phone** - calls your **office phone** - press the *#* key to verify the call.
   - **Answer my security questions** - displays your pre-registered security questions for you to answer.

    ![][109]
5. We'll use the "text my mobile phone" option as an example. If you are using a phone-based option, you need to verify your phone number before we send a text. Enter your full phone number and then click **Text** to verify it's correct and send a text.

6. When you receive the text, make sure you use the verification code in the message body, not the number the code was sent from. It might take several minutes to get the text.

7. Now, enter the code you just received on your phone into the input box on the page and choose **Next**.

8. Your administrator may require an additional verification step, in which case repeat step 4 with a different option selected.
9. On the "choose a new password" screen, select a new password and confirm your choice, then click **Finish**.

    ![][107]

10. Once your password is accepted, you can sign in with the new password.

    ![][108]

Run into a problem resetting your password? Read about [common problems and their solutions](#common-problems-and-their-solutions).

## How to unlock your account
Follow the steps below to unlock your local account from any work or school account sign in screen. 

> [!NOTE]
> You are only able to unlock your account if it has been locked on-premises.

> [!IMPORTANT]
> This feature is only available to you if your admin has turned it on. If it's not turned on, you'll see a message indicating your account is not enabled for this feature. You can use the "contact your administrator" link in this case to get in touch with your admin to unlock your account.
>
> If your admin has enabled you for this feature, you'll first need to sign up before you can use it. You can do that here: http://aka.ms/ssprsetup.
>
>

1. On any work or school account sign in page, click the "can't access your account?" link, or navigate to https://passwordreset.microsoftonline.com directly.

    ![][110]

2. On the "who are you?" page, enter your work or school account ID and prove you aren't a robot by passing the CAPTCHA challenge.

    ![][111]

3. Click the "next" button.
4. Choose an option to unlock your account. Depending on how your administrator has configured the system, you might see one or more of the following choices:

   - **Email my alternate email** - sends an email with a 6-digit code to either your **alternate email** or **authentication email** (you choose).
   - **Text my mobile phone** - texts your phone with a 6-digit code to either your **mobile phone** or **authentication email** (you choose).
   - **Call my mobile phone** - calls your **mobile phone** or **authentication phone** (you choose) - press the *#* key to verify the call.
   - **Call my office phone** - calls your **office phone** - press the *#* key to verify the call.
   - **Answer my security questions** - displays your pre-registered security questions for you to answer.

    ![][112]
5. We'll use the "Answer my security questions" option as an example. Fill in the answers to your security questions and select **Next** to verify your identity.

6. Your administrator may require an additional verification step, in which case you must repeat step 4 with a different option selected.
7. Once you see the success page, you are good to go! Your on-premises account has been unlocked and you can now sign in once more.

    ![][113]

    > [!IMPORTANT]
    > Make sure you update all your devices to your newest password, as often times a rogue app with an old password (like your phone email client) can be the culprit behind why your account got locked out in the first place.
    >
    >

Run into a problem unlocking your account? Read about [common problems and their solutions](#common-problems-and-their-solutions).

## Common problems and their solutions
Here are some common error cases and their solutions:

<table>
          <tbody><tr>
            <td>
              <p>
                <strong>Error Case</strong>
              </p>
            </td>
            <td>
              <p>
                <strong>What error do you see?</strong>
              </p>
            </td>
            <td>
              <p>
                <strong>Solution</strong>
              </p>
            </td>
          </tr>
          <tr>
            <td>
              <p>I get a "please contact your admin" page after entering my user ID</p>
            </td>
            <td>
              <p>Please contact your admin <br><br>We've detected that your user account password is not managed by Microsoft. As a result, we are unable to automatically reset your password. <br><br>You will need to contact your admin or helpdesk for any further assistance. </p>
            </td>
            <td>
              <p>You are seeing this message because your administrator manages your password in your on-premises environment and does not allow you to reset your password from the <b>Can't access your account link</b>. <br><br> To reset your password, please contact your administrator directly for help, and let him or her know you want to reset your password from Office 365 so he or she can enable this feature for you.</p>
            </td>
          </tr>
          <tr>
            <td>
              <p>I get a "your account is not enabled for password reset" error after entering my user ID</p>
            </td>
            <td>
              <p>Your account is not enabled for password reset<br><br>We're sorry, but your administrator has not set up your account for use with this service.<br><br> If you'd like, we can contact an administrator in your organization to reset your password for you.</p>
            </td>
            <td>
              <p>You are seeing this message because your administrator has not enabled password reset for your organization from the <b>Can't access your account</b> link, or hasn't licensed you to use the feature. <br><br> To reset your password, click the <b>contact an administrator</b> link to send an email to your company's admin, and let him or her know you want to reset your password from Office 365 so he or she can enable this feature for you.</p>
            </td>
          </tr>
          <tr>
            <td>
              <p>I get a "we could not verify your account" error after entering my user ID</p>
            </td>
            <td>
              <p>We could not verify your account<br><br>If you'd like, we can contact an administrator in your organization to reset your password for you. </p>
            </td>
            <td>
              <p>You are seeing this message because you are enabled for password reset, but you have not registered to use the service.  To register for password reset, go to http://aka.ms/ssprsetup after you have regained access to your account. <br><br> To reset your password, click the <b>contact an administrator</b> link to send an email to your company's admin.</p>
            </td>
          </tr>
        </tbody></table>

## Next steps
If you have further questions about Self Service Password Rest (SSPR), please contact your Administrator or follow the links below.

- [Need to register your SSPR information?](https://login.partner.microsoftonline.cn)
- [Can't access your account?](https://passwordreset.microsoftonline.com)
- [Office 365 password reset info](https://support.office.com/en-us/article/Reset-user-passwords-in-Office-365-3254c031-04c9-44f1-8fda-2563847a6b31?ui=en-US&rs=en-US&ad=US)
- [Access Panel](https://login.partner.microsoftonline.cn)

[101]: ./media/active-directory-passwords-update-your-own-password/password-1-dont-lose-access.png "password-1-dont-lose-access.png"
[102]: ./media/active-directory-passwords-update-your-own-password/password-2-verification-response.png "password-2-verification-response.png"
[103]: ./media/active-directory-passwords-update-your-own-password/password-2-verification-text.png "password-2-verification-text.png"
[104]: ./media/active-directory-passwords-update-your-own-password/password-3-registration-complete.png "password-3-registration-complete.png"
[105]: ./media/active-directory-passwords-update-your-own-password/password-4-reset-cant-access.png "password-4-reset-cant-access.png"
[106]: ./media/active-directory-passwords-update-your-own-password/password-4-reset-captcha.png "password-4-reset-captcha.png"
[107]: ./media/active-directory-passwords-update-your-own-password/password-4-reset-change.png "password-4-reset-change.png"
[108]: ./media/active-directory-passwords-update-your-own-password/password-4-reset-finished.png "password-4-reset-finished.png"
[109]: ./media/active-directory-passwords-update-your-own-password/password-4-reset-verification.png "password-4-reset-verification.png"
[110]: ./media/active-directory-passwords-update-your-own-password/password-5-unlock-cant-access.png "password-5-unlock-cant-access.png"
[111]: ./media/active-directory-passwords-update-your-own-password/password-5-unlock-captcha.png "password-5-unlock-captcha.png"
[112]: ./media/active-directory-passwords-update-your-own-password/password-5-unlock-verification.png "password-5-unlock-verification.png"
[113]: ./media/active-directory-passwords-update-your-own-password/password-5-unlock-finished.png "password-5-unlock-finished.png"