---
title: Windows Store
parent: Marketplace
grand_parent: Technical
---

# Register Developer Account

# Signing Credentials

This may not be required when using MSIX files

> `Automatic Digital Signing - MSIX requires digital signing and, by publishing it to Microsoft Store, your app gets signed automatically. Therefore, you don’t need to buy a third-party CA (certification authority), and your app will have the credibility of being secure in case you use your own certification`
> 
> https://stackoverflow.com/questions/76982311/microsoft-windows-app-store-digital-signing-requirements

# CICD Pipeline


# MakeAppx.exe

included in:
- Microsoft Visual Studio
- Windows Software Development Kit (SDK) for Windows 8
- Windows Software Development Kit (SDK) for Windows 8.1 and newer. 
- Visit [Downloads for developers](https://msdn.microsoft.com/windows/apps/br229516.aspx)

## Package Manifest (AppxManifest.xml)

https://learn.microsoft.com/en-us/windows/msix/desktop/desktop-to-uwp-manual-conversion

> If you've reserved your application name in the Microsoft Store, you can obtain the Name and Publisher by using [Partner Center](https://partner.microsoft.com/dashboard). If you plan to sideload your application onto other systems, you can provide your own names for these as long as the publisher name that you choose matches the name on the certificate you use to sign your app.

```xml
<Identity Name="MyCompany.MySuite.MyApp"
          Version="1.0.0.0"
          Publisher="CN=MyCompany, O=MyCompany, L=MyCity, S=MyState, C=MyCountry"
		ProcessorArchitecture="x64">
```



## Mapping File Structure

https://learn.microsoft.com/en-us/windows/win32/appxpkg/make-appx-package--makeappx-exe-#to-create-a-package-using-a-mapping-file

- Create a valid package manifest, AppxManifest.xml.
- Create a mapping file. The first line contains the string **[Files]**, and the lines that follow specify the source (disk) and destination (package) paths in quoted strings.
```
[Files]
"C:\MyApp\StartPage.htm"     "default.html"
"C:\MyApp\readme.txt"        "doc\readme.txt"
"\\MyServer\path\icon.png"   "icon.png"
"MyCustomManifest.xml"       "AppxManifest.xml"
```
- Run this command: `**MakeAppx pack /f** _mapping_filepath_ **/p** _filepath_**.appx**`


# Upload Application

https://github.com/marketplace/actions/upload-microsoft-store-msix-package-to-github-release



# References
