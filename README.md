# MySecurityInfo

Public repository for sharing information and app content about My Security Info using Azure AD Authentication Methods

Important! Read this README file before you import the PowerApp to your environment.

## Language Support

The PowerApp is created for Norwegian / Scandinavian organizations, but I have included a language selector in the PowerApp so you can switch to English.

## Requirements

This PowerApp is built on retrieving the user's authentication methods via Microsoft Graph API. These methods are currently (May 2021) in the Beta endpoint, and not yet GA (Generally Available).

This means that it should be safe to use the API for test and insights, but you should not rely on this in Production environment, as beta API changes can be done before GA.

The usage of the authentication methods API, depends on your Organizations Microsoft 365/Azure AD licenses, settings and policies made available for the users.

The PowerApp uses a Custom Connector to send requests to Graph API, this is a Premium feature in Power Platform. You will need licenses for user or app, or trial licenses to be able to use this feature.

You also need permissions in Azure AD and Power Platform environment, or get help from IT to perform the below steps.
 
The high level steps to complete the import is the following:

1. Create an Azure AD App Registration for Microsoft Graph permissions to be used by Custom Connector.
1. Import the Yaml file in this repo to create the Custom Connector.
1. Import the PowerApp package.
1. Test and share in your organization.

## Security Concerns

The PowerApp and Custom Connector uses Delegated Permissions, this means that the App does not include more permissions than the user already has and can see using the security information portal (https://myprofile.microsoft.com). The app is stateless and does not save any of the authentication methods data outside the running values.

## Instructions

Follow these steps for preparing and importing the PowerApp:

### Create App Registration

Depending on the settings in your organization, you might not have permission to do the following, contact your IT admin for assistance.

1. In the Azure AD Portal, create a new App Registration, use any naming standard you might have, or call it something like: "MSGraph Authentication Methods". Select single tenant for account types.
1. For Redirect URI, add the following "https://global.consent.azure-apim.net/redirect", and click Register.
1. Under API Permissions, click "Add a permission" and then select Microsoft Graph. Click on Delegated Permissions and add the "UserAuthenticationMethod.Read" permission. You can also optionally add the "Organization.Read.All" permission if you want users to be able to read Organization name and contact details in the PowerApp. This is not required, but something that could be useful in large organizations.
1. Next, you need an Admin to Grant Admin consent for these permissions.
1. Next, go to Overview, and click to copy the Application (client) ID. Save this for later.
1. Proceed to Certificates & Secrets, and click to create a new Client Secret. Give this a description and selected expiry, and then add. You will need to copy this value also and save for later. 

After these steps are successfully created, proceed to the next step.
### Create the Power Platform Custom Connector via YAML import

In this
