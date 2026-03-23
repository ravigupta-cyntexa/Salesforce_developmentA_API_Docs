## step1:- create a connected app
#### setup->setting(external client app setting)->new Connected App
Imppp Here only changes from Oauth previous  - inside Selected OAuth Scopes	select 2 things
```
Full access (full)
Perform requests at any time (refresh_token, offline_access)
````

## step2 Now copy the bwlow data from connected app 
#### setup-> app manager-> view you connected app-> manage consumer details-> verify-> copy consumer key and consumer secret
client_id=consumer key , client_secret=consumer secret

## create Brower url to generate the token see below 
#### by help of -> 
```
instanceUrl+ /services/oauth2/authorize?client_id=consumerKey&client_secret=consumer_secret&response_type=code&redirect_url=urlentered_in_connected_app&code_challenge=ql0Arf5B4VZ8nK7jL9k2ZpTQn7QmW6XxYzExample
&code_challenge_method=S256
```
### see below
#### code_challenge is random string and method will be S256 
#### client secret is optional 
```
https://orgfarm-6a4e00e053-dev-ed.develop.my.salesforce.com/services/oauth2/authorize
?response_type=code
&client_id=3MVG9dAEux2v1sLtBiUzgKX_jZlixXJvtv4NGKyniao8cv3hP9p7EgamLGPVSwm.5ngKrEbNYfMghPNdljmWw
&redirect_uri=https://cyntexa.com
&code_challenge=ql0Arf5B4VZ8nK7jL9k2ZpTQn7QmW6XxYzExample
&code_challenge_method=S256
```

## step3 Now Hit that Api Url in browser
