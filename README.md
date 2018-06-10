# AspNetCore2.1-Https

 ## Motivation
AspNetCore 2.1 Hosted In Kestrel using Embedded Certificate to achieve Https and Http to https redirection

## Pre-requisite
### Generate and let embed it to your asp net core 2.1 project 

If you are in Visual studio, the very first time you create an Asp net core 2.1 web api project with Option "Configure for HTTPS",  .NET Core SDK will install a "ASP.NET Core HTTPS Development Certificate".
And VS will ask you to trust it. Yes/No.

This is very equivanlent to do achieve above stuffs using command line:
or you run **dotnet new webapi**,

````
PS ...> dotnet tool install --global dotnet-dev-certs --version 2.1.0

  You can invoke the tool using the following command: dotnet-dev-certs
Tool 'dotnet-dev-certs' (version '2.1.0') was successfully installed.
````

````
PS ...> dotnet dotnet-dev-certs https --trust

Trusting the HTTPS development certificate was requested. A confirmation prompt will be displayed if the certificate was not previously trusted. Click yes on the prompt to trust the certificate.

````
### Export the certificate
Go to your Windows certificate store (c.f. https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in) and export the certificate in Current User> Personal > Certificates, the one with ASP.NET Core HTTPS development certificate named "development.pfx"... with your screte word ;)

### Use the exported certificate in your project
Put it on the foot of your web api root path.
Add the following in csproj:

````xml
  <ItemGroup>
    <EmbeddedResource Include="development.pfx" />
  </ItemGroup>
````

