## Step1 first go to here 
###### click on this link :- https://www.twilio.com/docs/messaging/api/message-resource

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/42a6f64d-3713-43df-9bf6-6605f95ff798" />

## step 2 -> copy the curl url of sending sms 
```
curl -X POST "https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json" \
--data-urlencode "From=+15557122661" \
--data-urlencode "Body=Hi there" \
--data-urlencode "To=+15558675310" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN

```

<img width="1166" height="543" alt="Image" src="https://github.com/user-attachments/assets/df19e35e-4d95-45c6-943d-776702f9a5e9" />


## step 3-> copy that curl and Import it on Postman

<img width="1893" height="959" alt="Image" src="https://github.com/user-attachments/assets/28264cdf-0c5a-43ef-ba22-e9c63f219fa4" />

## step 4-> go to you Twilio Home Account 
### copy teh Account SID, Token 

```
AccountSID
344ec4de0ef16496cf96577f008fb29b
```
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/f4544e3c-7602-4849-b52b-65a545fe04dd" />


## step 5-> go to you Postman Imported Curl request 
### (i) Authorization 
       -> Enter You Account SID as UserName 
       -> Enter You Access Token as Password 

<img width="1370" height="477" alt="Image" src="https://github.com/user-attachments/assets/ce4cc97c-320d-4cf9-89e6-16cf11b99d01" />

### (ii) In URL I mean API calling url 
      -> In Place of Account  $TWILIO_ACCOUNT_SID Enter You copied Account SID
      ```
      $TWILIO_ACCOUNT_SID= AC403e94afa7***************
      ```

### (iii) See 
Initial URL -> https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json
after Insert Account SID -> https://api.twilio.com/2010-04-01/Accounts/AC403e94afa7df9476***********/Messages.json 

<img width="1429" height="441" alt="Image" src="https://github.com/user-attachments/assets/088cbde7-f21c-4876-9431-d28abb302610" />


## step 5 -> add Body correct Data 
#### Add From , Body And To 
From will be the Your active Number 
To will be the you verified called ID Number of anyone 

<img width="775" height="164" alt="Image" src="https://github.com/user-attachments/assets/c0e69e35-e26d-4b67-9b7c-e470c5842f23" />
