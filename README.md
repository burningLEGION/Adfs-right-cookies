# Adfs-right-cookies

Description of the issue: Sometimes it is necessary for the developer to make use of session variables in the application and this interferes with the cookies in Microsoft.Owin.Host.SystemWeb, i.e. Response.Cookies collection will overwrite any cookies set via the OWIN response headers. This causes the subsequent log-ins to fail.

Resolution: There is a workaround to fix the issue. The objective of the workaround is to not use the default cookie manager here, but create a new custom one – SystemWebCookieManager.

This is then brought into use by the below code in ConfigureAuth() in the file Startup.auth.cs

app.UseCookieAuthentication(new CookieAuthenticationOptions
{
CookieManager = new SystemWebCookieManager()
});
