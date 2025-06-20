# Twin Protocol Platform SSO Link Generation

Using the sdk, you can generate single-sign-on links in order to access Twin Protocol Platform seamlessly, without having to undergo the sign up/login process on the platform.

This is a 2 step process:

## 1. User Creation
The existence of the user/email (for which the sso link is to be generated) in the Twin Platform DB is necessary. This can be done using the createUser endpoint of the sdk. Please refer to Twin Associated Operations/Sso Related Operations/Twin User Creation.


### 2. SSO Link Generation
Once the user is injected into the Twin Platform DB, the next step is to generate the SSO link. This can be done using the generateSsoLink endpoint of the sdk. This would grant access to the Twin Platform itself. Please refer to Twin Associated Operations/Sso Related Operations/Sso Link Generation.