- [terms of use](https://fhir.epic.com/Resources/Terms) of open.epic.
- https://fhir.epic.com/Documentation?docId=patientfacingfhirapps
- https://fhir.epic.com/Documentation?docId=developerguidelines
- https://fhir.epic.com/FAQ


> The app should protect authentication credentials provided by Epic or Epic Community Members, such as user names, user passwords, access tokens, or refresh tokens. Credentials used to access Epic Community Member’s Epic systems should be unique to each Epic Community Member, should only be used in conjunction with Epic APIs, and should never be passed to non-Epic systems. If the app needs to persist this data to non-volatile storage, it should use approved secure storage functionality provided by the host platform/operating system.

> If the app prompts the user for credentials such as passwords or biometric data, or other sensitive information such as credit card numbers or financial account information, you should take care to protect this data. If the data must be written to non-volatile storage, it should never be stored in clear text. The app should make use of one-way hashing algorithms such as SHA-256 or secure storage functionality provided by the host platform/operating system to persist this data. Your app should secure all data on an end-user’s device(d)(7) (d)(8), and enforce inactivity time-outs.(d)(5)

>  1.3 Privacy and Data Use Guidelines
>  
>  You should provide users (e.g., the Epic Community Member or end user that uses your app) with a clear and understandable data use or privacy policy that includes an explanation of any data elements that your app obtains from or writes to an Epic Community Member’s Epic system and how and where that data is used. If you or your app do any of the following, then, for each, you should disclose such action to, and obtain appropriate consent from, the user: obtaining data from or writing data to an Epic Community Member's Epic system, retaining data processed by your app (including the length of time for which the data is retained), making any secondary uses of the data, providing any other party or product any access to the data, transferring the data to any other party or product.
>  
>  A patient-facing app should obtain such consent from end users and provide end users with an option to decline consent or to revoke their consent in the future. A patient-facing app should not circumvent the display of any end user authentication or authorization mechanisms from Epic or any Epic Community Member.
>  
>  When you use, retain, or distribute data that you obtained from an Epic Community Member’s Epic system, you should document who used, retained, or distributed what data, when they did so, and for what purpose they did so. You should provide users access to that documentation upon request.
>  
>  You should provide clear and prominent notice to users how they may stop the app from reading, writing, or retaining data.


> 1.5 Data and System Integrity Guidelines
>
>  The app should appropriately manage end users’ assumptions and expectations of healthcare software to avoid negative outcomes. If the app permits end users to input data that is typically input and stored in an Epic system, or if the app uses an API to look up data from an Epic system and also permits end users to edit that data, then end users are likely to assume or expect that the app will file the new or updated data to Epic. If the app facilitates part of a workflow, then end users are likely to assume or expect the app to trigger downstream steps in the workflow (e.g., trigger a message to another end user, trigger an interface message, etc.).
>  
>  You and your apps should not corrupt or otherwise cause material inconsistencies in any data used by your apps.(d)(2)