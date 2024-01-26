---
title: Apple Store
parent: Marketplace
grand_parent: Technical
---

# Register Developer Account - Enrolling as an Organization

## Requirements:

1. **An Apple device**, such as an iPhone, iPad, or Mac computer to complete Apple’s two-factor authentication process. Apple requires two-factor authentication for all Apple IDs and requires Developer Account Holders to sign in to their Apple Developer account using two-factor authentication. Two-factor authentication is built directly into iOS, macOS, tvOS, watchOS, and Apple websites which all require an Apple device such as an iPhone, iPad, or iPod touch with iOS 9 and later, or a Mac with OS X El Capitan or later. See, [Apple’s Support: Two-Factor Authentication](https://developer.apple.com/support/authentication/) to learn how to set up two-factor authentication on your Apple device.
1. **An Apple ID**. You can create an Apple ID using either your personal email address or an email address associated with your business. When creating an Apple ID, keep in mind that Apple will use the email address you choose to bill the annual $99 (USD) publisher fee and email you app updates. Follow this link to learn [how to create your Apple ID](https://support.apple.com/en-ca/HT204316). Be aware that creating an Apple ID is not the same as creating an Apple Developer account.
1. **An email address**. You can begin your enrollment in the Apple Developer Program using a personal email address, such as yourname@gmail.com, but Apple will eventually require you to provide a private email that uses the domain name associated with your business’s website, such as email@yourbusiness.com.
1. **D-U-N-S® Number**. A D-U-N-S Number is a unique numeric identifier assigned to a business by Dun & Bradstreet (D&B). It is used by Apple to validate your business’s identity and legal status. You cannot enroll in the Apple Developer Program without a D-U-N-S Number. To acquire a D-U-N-S, see [Requesting a D-U-N-S Number](https://developer.apple.com/support/D-U-N-S/) on the Apple Developer website. Keep in mind that the information you submit when requesting a D-U-N-S Number must match the information you submit when enrolling in the Apple Developer Program. For example, the legal entity name for your business must be spelled and stylized the same way in both enrollment forms. After you acquire a D-U-N-S Number, you can use the [D-U-N-S look up tool](https://www.dnb.com/duns-number/lookup.html) to pull up your D-U-N-S Number and related information at any time.
1. **A business website URL**. We recommend using a publicly available website with a domain name associated with your organization.
1. **Verification call**. After you submit the necessary information to enroll in the Apple Developer Program, Apple will call you to verify your information. During this call, you must be able to provide Apple with your D-U-N-S Number and the information you used to request a D-U-N-S Number. You must also be able to show Apple your business information (such as your business location addresses and business hours) on your own website. 

## Enrolling as an Organization

1.  Go to the [Apple Developer Program enrollment page](https://developer.apple.com/programs/enroll/) and click **Start Your Enrollment**.
2.  Log in with your Apple ID and password.
3.  Apple will prompt you to complete two-factor authentication. Click **Allow** on your mobile device to receive a verification code.
4.  Under **Two-factor Authentication** on your browser, enter the verification code sent to your mobile device and click **Continue**.
5.  Read the Apple Developer Agreement, select the **By checking this box I confirm that I have read and agree to be bound by the Agreement above** checkbox and click **Submit**.
    *   If Apple updates the license agreement for the Apple Developer Program before your App is launched, you must accept the new agreement.
6.  Click **Continue enrollment on the web.**
7.  Under **I develop apps as**, select **Company / Organization** and click **Continue.**
8.  Under **Authority to Sign Legal Agreements**, select the appropriate option:
    *   **I am the owner/founder and have the authority to bind my organization to legal agreements**
        *   If you select this option, enter your email address in the **Work Email** The email address you enter must match the one you provided when requesting a D-U-N-S Number.
    *   **My organization has given me the authority to bind it to legal agreements**
        *   If you select this option, in the **Verification Contact** field, enter a senior employee’s contact information. Apple will use this information to contact the senior employee at your organization and confirm enrollment in the Apple Developer Program.
9.  Under **Organization Information**, enter the information for your organization:
    *   In the **Legal Entity Name** field, enter the name of your business as it appears in the D-U-N-S lookup.
        *   Your enrollment will not be successful if the legal entity name does not match the one in the D&B profile.
    *   In the **D-U-N-S Number** field, enter the nine-digit D-U-N-S Number assigned to your business. 
    *   In the **Website** field, enter the website URL for your organization.
        *   The website URL can be a publicly available website with a domain name associated with your organization
    *   In the **Headquarters Phone** field, enter a phone number where Apple can reach you to verify enrollment.
    *   In the **Tax ID/National ID** field, enter your organization’s Tax ID/National ID.
        *   This is an optional field.
    *   Type the correct characters in the CAPTCHA.
10.  Click **Continue**.
     *   If you receive an error message under the **Legal Entity Name** field, click **update your D&B profile** and submit your business’s information. You may continue this procedure once your profile has been updated.
11.  On the **Summary for Review** page, review and confirm the information. Select the **This is the correct headquarters address for my organization** checkbox and click **Submit**.
12.  After submitting your application, Apple will contact you to verify your enrollment information.
     *   During this call, you must be able to provide Apple with your D-U-N-S Number and the information you used to request a D-U-N-S Number.
13. Apple will send a confirmation email to your Apple ID email address with a link enclosed to confirm and pay for your developer membership. The $99 (USD) membership is billed annually.
     *   We strongly suggest you sign up for Automatic Renewal payments to prevent service disruption. When you are paying for your Apple Developer Program membership, review your purchase details and select **Automatic Renewal**. If you do not select **Automatic Renewal**, please set an annual reminder to renew your membership. Your app will be removed from the App Store within 24 hours upon the expiration of your membership.

# Signing Credentials

Beginning with macOS Catalina (10.15), Apple is [requiring all software distributed outside of the Mac App Store (Direct Distribution) to be signed and notarized](https://developer.apple.com/news/?id=10032019a). 
Software that isn't properly signed or notarized will be shown an error message with the only actionable option being to "Move to Bin". The software cannot be run even from the command-line.

![gatekeeper.png](/img/marketplace/apple/gatekeeper.png)

Apps submitted to TestFlight need to be signed with an [App Store Distribution Profile](https://developer.apple.com/forums/thread/733942).

For information on how to set up these code signing identities, see [Developer Account Help](https://help.apple.com/developer-account/).

This means you will need to create the following certificates and profiles:
- **1x [Application Identifier](https://developer.apple.com/account/resources/identifiers/list)** - This contains your Bundle ID(e.g. `com.example.app`) and associated Capabilities
- **2x [Certificates](https://developer.apple.com/account/resources/certificates/list)** 
  - 1x **Developer ID Application Certificate** for Direct Distribution
  - 1x **Apple Distribution** for App Store Distribution
- **2x [Provisioning Profiles](https://developer.apple.com/account/resources/profiles/list)**
  - 1x **Developer ID Application Profile** for Direct Distribution
  - 1x **App Store Distribution Profile** for App Store Distribution

|  | TestFlight/App Store Distribution | Direct/External Distribution |
| --- | --- | --- |
|  Certificate | `Apple Distribution: TTT` | `Developer ID Application: TTT` |
|  Provisioning Profile | `App Store Distribution: TTT` | `Developer ID Application: TTT` |

{: .important }
> See [Which certificate should I use to sign my Mac OS X application?](https://stackoverflow.com/questions/29039462/which-certificate-should-i-use-to-sign-my-mac-os-x-application) for more information about the various Certificate types

## Create a Signing Certificate

{: .important }
> You may need to create 2 of these (depending on your distribution methods)

We start by obtaining the certificates. After logging to your developer account and selecting `Certificates`, you should be able to create a new certificate. 
From all the listed types, select `Developer ID Application` as per its description.

![create-new-certificate.png](/img/marketplace/apple/create-new-certificate.png)

To be able to obtain the certificate, you need to create a Certificate Signing Request (CSR) first, which you can easily get by opening Keychain Access and going to `Certificate Assistant` -> `Request a Certificate from a Certificate Authority`

![keychain-access-request-certificate.png](/img/marketplace/apple/keychain-access-request-certificate.png)

Fill in the necessary information and select your request to be `Saved to disk`. Note that the email address should be the same as the one you’re logging to the developer account. For an organization you can use something like `marketplace@example.com`

![keychain-access-certificate-assistant.png](/img/marketplace/apple/keychain-access-certificate-assistant.png)

You can then upload the CSR request file to the web which should successfully create a new certificate for you. Download it and add it to your Keychain Access by simply opening it. The certificate should be added to one of your default keychains and not to the system; otherwise you might later have troubles exporting it.

![keychain-access.png](/img/marketplace/apple/keychain-access.png)

{: .warning }
> If you see a "certificate is not trusted" error for the Certificate in your Keychain, you will need to install the [Apple Worldwide Developer Relations Certification Authority](https://developer.apple.com/support/expiration/) certificate.
> ![keychain-intermediate.png](/img/marketplace/apple/keychain-intermediate.png)
> 
> - <https://developer.apple.com/account/resources/certificates/add>
> - [Developer ID Intermediate Certificate](https://www.apple.com/certificateauthority/DeveloperIDG2CA.cer)
> - [Distribution Intermediate Certificate](https://www.apple.com/certificateauthority/AppleWWDRCAG3.cer)

To be able to use the certificate for automated code signing, we need some format which would allow us to store the certificate as 
a string, so we can later add it to Github Secrets as an environment variable. For that purpose, we’ll make use of a little 
trick by encoding it to base64 first and then decoding it during the workflow. Let’s export the certificate by selecting 
both the certificate and its private key, invoke its context menu and select `Export 2 items …`. 
From the available formats pick `Personal Information Exchange (.p12)`. Then it will ask you to create a password for it. 
Generate it and note it down, we’ll need it shortly.

![keychain-export-certificate.png](/img/marketplace/apple/keychain-export-certificate.png)


> Developer ID signing identities are precious. Anyone with access to one can ship code as you. Given that, you should treat them with care:
> - You should not create them unnecessarily. Most folks only need to create one (well, one each for Developer ID Application and one Developer ID Installer). For a large organisation it might make sense to create a few, one for sub-units within the organisation.
> - You should carefully manage access to them. Remember, if one leaks then folks will be able to start shipping code as you.
>
> If you’re trying to create a new Developer ID signing identity because you’ve misplaced your previous ones, I encourage you to look harder. If you can find the previous ones, it’ll save you a whole bunch of hassle.
>
> <https://developer.apple.com/forums/thread/659545?answerId=631425022#631425022>

### Confirm Your Code Signing Identity

To sign code for distribution you need a code signing identity. Choose the right identity for your distribution channel:
- If you’re distributing an app on the Mac App Store, use an Apple Distribution code signing identity. This is named `Apple Distribution: TTT`, where `TTT` identifies your team.
- Alternatively, you can use the old school Mac App Distribution code signing identity. This is named `3rd Party Mac Developer Application: TTT`, where `TTT` identifies your team.
- If you’re distributing a product independently, use a Developer ID Application code signing identity. This is named `Developer ID Application: TTT`, where `TTT` identifies your team.

```bash
% security find-identity -p codesigning -v
1) A06E7F3F8237330EE15CB91BE1A511C00B853358 "Apple Distribution: …"
2) ADC03B244F4C1018384DCAFFC920F26136F6B59B "Developer ID Application: …"
   2 valid identities found
```

# Create an Application Identifier (App ID) & Provisioning Profiles

1. Use [Developer > Account > Identifiers](https://developer.apple.com/account/resources/identifiers/list) to create an App ID for your app. Remember that your App ID is the combination of an App ID prefix and your app’s bundle ID. For new App IDs, use your Team ID as the App ID prefix.

    ![identifier.png](/img/marketplace/apple/identifier.png)
    ![identifier-type.png](/img/marketplace/apple/identifier-type.png)

2. Use [Developer > Account > Profiles > Distribution](https://developer.apple.com/account/resources/profiles/list) to create a `Developer ID` distribution provisioning profile for that App ID.

    ![profile-store-distribution.png](/img/marketplace/apple/profile-direct-distribution.png)

3. Use [Developer > Account > Profiles > Distribution](https://developer.apple.com/account/resources/profiles/list) to create an `App Store` distribution provisioning profile for that App ID.

    ![profile-direct-distribution.png](/img/marketplace/apple/profile-store-distribution.png)

# CICD Pipeline

The following `Github Secrets` are required when attempting to sign a macOS application for Direct Distribution:

- `APPLE_DEVELOPER_CERTIFICATE_P12_BASE64`
- `APPLE_DEVELOPER_CERTIFICATE_PASSWORD`
- `APPSTORE_ISSUER_ID`
- `APPSTORE_KEY_ID`
- `APPSTORE_PRIVATE_KEY`

## Developer Certificate Secret

`APPLE_DEVELOPER_CERTIFICATE_P12_BASE64` is generated by using the `Certificate.p12` file you exported from Keychain Access, and then base64 encoding it:

```bash
base64 Certificates.p12 | pbcopy 
```

Go to your Github project and navigate to `Settings -> Secrets` where you can add new secrets. 
Create a new repository secret, I’ve called it `APPLE_DEVELOPER_CERTIFICATE_P12_BASE64`, and paste the encoded certificate. 
Create another secret name, for example `APPLE_DEVELOPER_CERTIFICATE_PASSWORD`, where you store the certificate password you’ve created earlier.

![github-certificate-secret.png](/img/marketplace/apple/github-certificate-secret.png)

## App Store Connect API Secrets

We'll be using the App Store Connect API to automate our application workflow (signing the application via Notary Service, uploading the application to App Store Connect, and submitting the application for review).

Here are the official instructions for [Generating an API Key for App Store Connect API](https://developer.apple.com/help/app-store-connect/get-started/app-store-connect-api):

1. From [Users and Access](https://appstoreconnect.apple.com/access/users), click Keys. The page opens with the App Store Connect API selected.
1. Click Generate API Key.
    {: .important }
    > If you already have an Active API key generated, you can click the add button (+) to add more.
1. Enter a name for the key. The name is used for your reference only and isn’t part of the key itself.
1. Under Access, select the [role permissions](https://developer.apple.com/help/app-store-connect/reference/role-permissions) to determine what the API can be used for. API keys are applied across all apps so app access can’t be limited for an API key.
    {: .important }
    > Note: you should create your API key with the `App Manager` role, which will allow you to upload applications to App Store Connect, but will not allow you to submit the application for review.
1. Click Generate.
    {: .important }
    >Once you generate an API key, you won't be able to edit its name or access level. If you need to make changes, revoke the API key and generate a new one.

![app-store-connect-api-key.png](/img/marketplace/apple/app-store-connect-api-key.png)

## Build and Sign Binaries using Github Actions & Gon

**TODO**

- [Automatically bump version](https://medium.com/passei-direto-product-and-technology/from-xcode-to-testflight-using-command-line-288c3a85bd93)
- https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/customizing_the_notarization_workflow
- [Private Key location for notary tool ](https://developer.apple.com/forums/thread/701859)
- [Common Notization Issues](https://developer.apple.com/documentation/security/notarizing_macos_software_before_distribution/resolving_common_notarization_issues#3087721)
- [A Peek Behind the Code Signing Curtain](https://developer.apple.com/forums/thread/702351)
- 

## Upload Application to TestFlight using Transport

**TODO**


- https://developer.apple.com/help/app-store-connect/manage-builds/upload-builds
- https://help.apple.com/itc/transporteruserguide/en.lproj/static.html
- <https://developer.apple.com/forums/thread/685723>


# Extract Provisioning Profile
- <https://maniak-dobrii.com/extracting-stuff-from-provisioning-profile/>
- <https://developer.apple.com/documentation/technotes/tn3126-inside-code-signing-hashes>
- <https://developer.apple.com/help/account/reference/provisioning-with-managed-capabilities/>
- [TestFlight for Mac shows "Not Available for Testing"](https://developer.apple.com/forums/thread/689377)
- 

# Apple Small Business Program

> The App Store Small Business Program is designed to accelerate innovation and help propel your small business forward with the next generation of groundbreaking apps on the App Store. It features a reduced commission rate of 15% on paid apps and in-app purchases, so you can invest more resources into your business to continue building quality apps that customers love.
>
> https://developer.apple.com/app-store/small-business-program/

- [x] Join Apple Small Business Program ✅ 2023-11-17

# Frequent Issues:

1. ITMS-90242: The product archive is invalid - The Info.plist must contain a LSApplicationCategoryType key, whose value is the UTI for a valid category. For more details, see 'Submitting your Mac apps to the App Store'.
    - https://developer.apple.com/documentation/bundleresources/information_property_list/lsapplicationcategorytype

1. ITMS-90869: Invalid bundle - The “fasten.app” bundle supports arm64 but not Intel-based Mac computers. Your build must include the x86_64 architecture to support Intel-based Mac computers. To support arm64 only, your macOS deployment tar
    - https://dev.to/thewraven/universal-macos-binaries-with-go-1-16-3mm3

1. https://stackoverflow.com/questions/30301179/missing-required-icons-when-submitting-app-with-application-loader



# Badges

https://tailwindcomponents.com/component/store-buttons-badge

# References

- <https://developer.apple.com/programs>
- <https://developer.apple.com/app-store/small-business-program>
- <https://wails.io/docs/guides/signing#macos>
- <https://wails.io/docs/guides/mac-appstore>
- <https://www.wellnessliving.com/knowledge-sharing/knowledge-base/enrolling-apple-developer-program-organization/>
- <https://localazy.com/blog/how-to-automatically-sign-macos-apps-using-github-actions>
- [Packaging Mac Software for Distribution](https://developer.apple.com/forums/thread/701581)
- [Creating Distribution-Signed Code for Mac](https://developer.apple.com/forums/thread/701514)
- [About Developer ID Application Certificates](https://developer.apple.com/forums/thread/659545?answerId=631425022#631425022)
- [TestFlight, Provisioning Profiles, and the Mac App Store](https://developer.apple.com/forums/thread/733942)
- [TestFlight Transporter](https://help.apple.com/itc/transporteruserguide/en.lproj/static.html)
- <https://github.com/mitchellh/gon>
- <https://github.com/create-dmg/create-dmg>
- [App Specific Passwords](https://support.apple.com/en-us/102654)
- [App-specific password not available from Managed Apple ID](https://developer.apple.com/forums/thread/128251)
-
