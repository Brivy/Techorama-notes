# Authenticating in Azure Static Web Apps

Default auth stuff:

* Auth url for static websites is found under `https://.../.auth`.
* `UserId` that is found for authentication is different for each application.
* `UserDetails` kinda different based on authenticators.
* Every person gets the default roles: `anonymous` and `authenticated`.
* Extra header that specifies if the person is authenticated: `x-ms-client-principal`.

Code:

* Nuget `Components.Authentication` and `Http.Abstractions`.
* Different models for the library:
  * `ClientPrincipal` is the principal that you saw with the `/.auth` path.
  * `SwaClaims` are custom claims for custom authentication.
  * `AuthenticationData` holds the `ClientPrincipal` object.
* In the backend, verify the default header and deserialize it.
* In the frontend, call the `/.auth/me` url, deserialize it and check for the roles. If you have more roles than the default ones, add those to the principal.
* Checking the user roles for `Authorized` is the way.
* The `staticwebapp-config.json` can serve as a good way of authorizing requests. For example, only authorize a specific role for certain HTTP methods.
* You can turn off authentication by specifying in `staticwebapp-config.json` that `/.auth/*` should redirect to a 404.

Blazor:

* Wrap the `<Router></Router>` into a <CascadingAuthenticationState></CascadingAuthenticationState>`.
* Using the `<AuthorizeView></AuthorizeView>` and within that `<Authorized></Authorized>` and the `<NotAuthorized></NotAuthorized>`.

API:

* Just a simple `HttpTrigger`.
* Don't send the UserId over a request, use the principal from the library.

Debugging:

* `swa start http https://localhost:5000` to start a static web app.
* Using the `\.auth` locally, you can enter dummy information. Like adding a new role called `Authorized`.

Azure:

* `Role management` is needed for user identity. You can only have 25 users in this list.
