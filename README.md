# dotnet-6-signup-verification-api

.NET 6.0 - Boilerplate API with Email Sign Up, Verification, Authentication & Forgot Password

Documentation at https://jasonwatmore.com/post/2022/02/26/net-6-boilerplate-api-tutorial-with-email-sign-up-verification-authentication-forgot-password

Documentación en español en https://jasonwatmore.es/post/2022/02/26/net-6-tutorial-de-api-estandar-con-registro-de-correo-electronico-verificacion-autenticacion-y-contrasena-olvidada

##### Configure your smtp using
https://ethereal.email/create

const transporter = nodemailer.createTransport({
    host: 'smtp.ethereal.email',
    port: 587,
    auth: {
        user: 'liam.herman@ethereal.email',
        pass: 'gVyX7BR8MDcPBT1U5w'
    }
});

POST /accounts/authenticate - public route that accepts POST requests containing an email and password in the body. On success a JWT access token is returned with basic account details, and an HTTP Only cookie containing a refresh token.
POST /accounts/refresh-token - public route that accepts POST requests containing a cookie with a refresh token. On success a new JWT access token is returned with basic account details, and an HTTP Only cookie containing a new refresh token (see refresh token rotation just below for an explanation).
POST /accounts/revoke-token - secure route that accepts POST requests containing a refresh token either in the request body or in a cookie, if both are present priority is given to the request body. On success the token is revoked and can no longer be used to generate new JWT access tokens.
POST /accounts/register - public route that accepts POST requests containing account registration details. On success the account is registered and a verification email is sent to the email address of the account, accounts must be verified before they can authenticate.
POST /accounts/verify-email - public route that accepts POST requests containing an account verification token. On success the account is verified and can now login.
POST /accounts/forgot-password - public route that accepts POST requests containing an account email address. On success a password reset email is sent to the email address of the account. The email contains a single use reset token that is valid for one day.
POST /accounts/validate-reset-token - public route that accepts POST requests containing a password reset token. A message is returned to indicate if the token is valid or not.
POST /accounts/reset-password - public route that accepts POST requests containing a reset token, password and confirm password. On success the account password is reset.
GET /accounts - secure route restricted to the Admin role that accepts GET requests and returns a list of all the accounts in the application.
POST /accounts - secure route restricted to the Admin role that accepts POST requests containing new account details. On success the account is created and automatically verified.
GET /accounts/{id} - secure route that accepts GET requests and returns the details of the account with the specified id. The Admin role can access any account, the User role can only access their own account.
PUT /accounts/{id} - secure route that accepts PUT requests to update the details of the account with the specified id. The Admin role can update any account including its role, the User role can only update there own account details except for role.
DELETE /accounts/{id} - secure route that accepts DELETE requests to delete the account with the specified id. The Admin role can delete any account, the User role can only delete their own account.


###### Enpoints with base url: https://localhost:4000

###### Register POST https://localhost:4000/accounts/register

```
{
    "email": "test@g.com",
    "firstName": "test",
    "lastName": "test",
    "title": "test",
    "password": "test-1234-spicy-le!",
    "confirmPassword": "test-1234-spicy-le!",
    "acceptTerms": true
}
```