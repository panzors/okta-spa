# okta-spa
Figure out how to do user access control with okta and claims

## Journey
This follows the guide at [https://github.com/panzors/okta-spa.git]

A bit of pre-reading on oauth helps too [https://oauth.net/getting-started/]

### Pre req

Sign up with a developer account with Okta. I chose to auth with my private google email and it gave me `dev-29183989-admin.okta.com` for a domain name

## Goals

- React front end
- .net api
- Authenticate with okta (both)
- Group authentication in claims

## Okta

- Create an app with OIDC - OpenID connect + SPA 
- Use the default setup with localhost:8080 and /login/callback as the signin redirect uri
- Create a new group `SPA-Default` and assign yourself to it
- Be given `clientId`

## Dotnet

Create a new mvc app [WeatherForecast](https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-7.0&tabs=visual-studio-code)

```sh
> cd ~/src/bff
> dotnet new webapi -o .
> dotnet dev-certs https --trust
> dotnet run --launch-profile https
```
- To test the api go to [localhost:abcd/WeatherForecast]
- For swagger go to [localhost:abcd/swagger]

```json
[
    {
        "date": "2023-11-20",
        "temperatureC": -16,
        "temperatureF": 4,
        "summary": "Hot"
    },
    {
        "date": "2023-11-21",
        "temperatureC": 15,
        "temperatureF": 58,
        "summary": "Chilly"
    },
    {
        "date": "2023-11-22",
        "temperatureC": 31,
        "temperatureF": 87,
        "summary": "Hot"
    },
    {
        "date": "2023-11-23",
        "temperatureC": 24,
        "temperatureF": 75,
        "summary": "Hot"
    },
    {
        "date": "2023-11-24",
        "temperatureC": -8,
        "temperatureF": 18,
        "summary": "Bracing"
    }
]
```

### Authentication
To make this authenticate with okta, we need to do a few things to it. First, we need to secure the controller end points to make it require bearer tokens and what not