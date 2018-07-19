![profiq OpenID PORTAL](/readmeGraphic/profiqLogo.png "profiq OpenID PORTAL")

[Based on Android client SDK for communicating with OAuth 2.0 and OpenID Connect providers.](https://openid.github.io/AppAuth-Android)
AppAuth for Android is a client SDK for communicating with
[OAuth 2.0](https://tools.ietf.org/html/rfc6749) and
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) providers.
It strives to
directly map the requests and responses of those specifications, while following
the idiomatic style of the implementation language. In addition to mapping the
raw protocol flows, convenience methods are available to assist with common
tasks like performing an action with fresh tokens.

# profiq OpenID PORTAL demo app for Android
 ![playPORTAL icon](/readmeGraphic/playPORTAL.png "playPORTAL icon")
 - for communication with [Dynepic playPORTAL](https://partner.iokids.net) through [Dynepic playPORTAL API](https://github.com/Dynepic/api-documentation)
  
This app demonstrates the AppAuth library by performing an authorization code
flow with an authorization service Dynepic playPORTAL. The configuration contained in `res/raw/auth_config.json`
must be modified in order for the app to function. Warnings are supplied when the app is run
with an invalid configuration.

The configuration file MUST contain a JSON object. The following properties can be specified:

  - `redirect_uri` (required): The redirect URI to use for receiving the authorization response.
    This can either be a custom scheme URI (com.example.app:/oauth2redirect/example-provider) or 
    an https app link (https://www.example.com/path). Custom scheme URIs are better supported 
    across all versions of Android, however many authorization server implementations require an 
    https URI. Consult the documentation for your authorization server.

    The value specified here should match the value specified for `appAuthRedirectScheme` in the
    `build.gradle` (Module: app), so that the demo app can capture the response.

  - `authorization_scope` (required): The scope string to use for the authorization request.
    For the purposes of the demo, we recommend the value "openid profile email", though any value
    understood by your authorization server can be used.

  - `client_id`: The OAuth2 client id used to identify the client to the authorization server.
    If this property is omitted, or an empty value is provided, dynamic client
    registration will be attempted using the registration URI in the discovery document referenced by
    `discovery_uri` below, or in the value `registration_endpoint_uri`.

  - `discovery_uri`: The OpenID Connect discovery URI for your authorization service, if available.
    If the IDP you wish to test does not support discovery, this value can be omitted or set
    to an empty string.

  - `authorization_endpoint_uri`: The authorization endpoint URI for your authorization service. If
    `discovery_uri` above is not specified, then this value is required. Otherwise, it can be
    omitted or set to an empty string.

  - `token_endpoint_uri`: The token endpoint URI for your authorization service. If `discovery_uri`
    above is not specified, then this value is required. Otherwise, it can be omitted or set to
    an empty string.

  - `registration_endpoint_uri`: The dynamic client registration endpoint URI for your authorization
    service. If client_id and discovery_uri above are not specified, this value MUST be specified.

  - `https_required`: Whether HTTPS connections are required for registration and token requests.
    If omitted, this defaults to true.

  - more info [here](https://github.com/openid/AppAuth-Android/blob/master/app/README-Gluu.md)
  
## Screenshots

![profiq OpenID PORTAL icon](/readmeGraphic/Screenshot_2018-07-18-18-14-37-611_com.miui.securitycenter.png "profiq OpenID icon")
![profiq OpenID PORTAL start](/readmeGraphic/Screenshot_2018-07-18-18-02-56-042_net.openid.appauthdemo.png "profiq OpenID start")
![profiq OpenID PORTAL login](/readmeGraphic/Screenshot_2018-07-18-18-03-03-838_com.chrome.beta.png "profiq OpenID login")
![profiq OpenID PORTAL profile](/readmeGraphic/Screenshot_2018-07-18-18-03-17-598_net.openid.appauthdemo.png "profiq OpenID profile")

## Requirements

AppAuth supports Android API 16 (Jellybean) and above. Browsers which provide a custom tabs
implementation are preferred by the library, but not required.
Both Custom URI Schemes (all supported versions of Android) and App Links (Android M / API 23+) can
be used with the library.

## Modifying AppAuth

This project requires the Android SDK for API level 25 (Nougat) to build,
though the produced binaries only require API level 16 (Jellybean) to be
used. We recommend that you fork and/or clone this repository to make
modifications; downloading the source has been known to cause some developers
problems.

### Building from the Command line

AppAuth for Android uses Gradle as its build system. In order to build
the library and app binaries, run `./gradlew assemble`.
The library AAR files are output to `library/build/outputs/aar`, while the
demo app is output to `app/build/outputs/apk`.
In order to run the tests and code analysis, run `./gradlew check`.

### Building from Android Studio

In AndroidStudio, File -> New -> Import project. Select the root folder
(the one with the `build.gradle` file).
