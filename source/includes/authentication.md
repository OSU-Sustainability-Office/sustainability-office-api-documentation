# Authentication
The authentication API allows our applications to authenticate users with CAS, using their ONID credentials. For more information about CAS at Oregon State University, refer to [this document](http://onid.oregonstate.edu/docs/technical/cas.shtml).

## Login
Users must navigate to [https://api.sustainability.oregonstate.edu/v2/auth/login](https://api.sustainability.oregonstate.edu/v2/auth/login) to begin the authentication process. Optionally, a return URI can be specified: [https://api.sustainability.oregonstate.edu/v2/auth/login?returnURI=https://myco2.sustainability.oregonstate.edu/#/](https://api.sustainability.oregonstate.edu/v2/auth/login?returnURI=https://myco2.sustainability.oregonstate.edu/#/). The return URI parameter specifies a destination for the user once they have authenticated with ONID.

A typical login looks like this:

1. The user navigates to the Carbon Calculator homepage at [https://myco2.sustainability.oregonstate.edu/#/](https://myco2.sustainability.oregonstate.edu/#/)
2. The user clicks the "Sign In" button. Their browser is redirected to [https://api.sustainability.oregonstate.edu/v2/auth/login?returnURI=https://myco2.sustainability.oregonstate.edu/#/](https://api.sustainability.oregonstate.edu/v2/auth/login?returnURI=https://myco2.sustainability.oregonstate.edu/#/)
3. The user successfully authenticates with CAS using ONID and Duo
4. The OSU Sustainability Office's authentication API stores a JSON Web Token (JWT) cookie in the user's browser
5. The user's browser is redirected to the specified return URI (in this case, it is [https://myco2.sustainability.oregonstate.edu/#/](https://myco2.sustainability.oregonstate.edu/#/))
6. Subsequent API calls are made using the JWT.

## Logout
Simply direct the user's browser to [https://api.sustainability.oregonstate.edu/v2/auth/logout](https://api.sustainability.oregonstate.edu/v2/auth/logout). They will be securely logged out of ONID.
