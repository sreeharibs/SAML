# Configuring SSO using SAML in DDFS

1. Enable SSO by Setting `IS_SSO_ENABLED = true ` in `Configuration.java`
2. Copy the `onelogin.saml.properties` in `DDFS/resources` to `resources` in Current Project (say `KMRL`)

##Before moving on...

* SP	: Service Provider 	-	The one which serve some service to the users	(eg: DDFS)
* IDP	: Identity Provider 	-	The one which manage identity information	(ie. Okta)

* Please Refer to `https://github.com/onelogin/java-saml` for more details.

## Configuring `onelogin.saml.properties`

The file can be divided into three sections:
1. Service Provider Configurations
2. Identity Provider Configurations
3. Security Settings

### 1. Service Provider Configurations

* Almost all the fields (starting with `onelogin.saml2.sp.`) in this section need to be configured based on our application.
* These information need to be shared with the IDP.
* Remember to replace `localhost:8080` with our `IP` and `Port`.
* The SAML Requests send by the SP provider need to be signed. For the same, a `Private Key` and `Certificate` need to be generated . You can generate the same using `openssl` or `https://developers.onelogin.com/saml/online-tools/x509-certs/obtain-self-signed-certs` . (openssl is preferred) .
* A `key and cert` pair has already generated and is included in `onelogin.saml.properties`. The same may be used for testing. But in Production, It is highly recommended to generate a new pair.
* IMPORTANT : DO NOT SHARE PRIVATE KEY TO ANYONE. WHILE SHARING `Service Provider Configurations` to IDP, CARE MUST BE GIVEN TO MASK THE PRIVATE KEY.

### 2. Identity Provider Configurations

* Almost all the fields (starting with `onelogin.saml2.idp.`) in this section need to be configured based on our Idp.
* These information need to be obtained from the IDP.
* Note : The `onelogin.saml2.idp.x509cert` is not the same as `onelogin.saml2.sp.x509cert`. The public key certificate need to be shared by the Idp.

### 3. Security Settings

* This section deals with the security configurations such as whether some fields are encrypted or not , signed or not etc...
* These need to be configured based on the Idp. 
* The Authentication may fail if these information is configured incorrectly. So please cross check with the Idp


## Tesing SSO using SAML in DDFS

1. Create an `okta` developer account at `https://developer.okta.com/signup/`
2. You may follow this blog @ `https://developer.okta.com/blog/2017/03/16/spring-boot-saml` to create an application in okta IDP.
3. Try Logging in using `.../ddfs/sso.do`

Feel Free to create an issue if you find any difficulty in implementing SSO

#FAQs
