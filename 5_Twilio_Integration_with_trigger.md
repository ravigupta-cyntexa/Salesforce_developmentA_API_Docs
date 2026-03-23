## step 1 lets create a trigger and Their Helper class first to achieve the requirement 
Requirement :-  when we create a student after create send a sms on their mobile number 
### let create trigger 
```
trigger sendSMSTrigger on Student__c (before insert, after insert) {
    if(trigger.isBefore){
        
    }else if(Trigger.isAfter){
        if(Trigger.isInsert){
              List<Student__c>stdList=Trigger.new;
             for(Student__c std:stdList){
                   sendMessageToStudent.myMethod(std.Student_Name__c, std.Student_Phone__c, std.Student_Email__c);
              }
        }
      
    }
}
```

### lets create a HelperClass for trigger 
```
public class sendMessageToStudent {
    
    public static void myMethod(String Name, String Phone, String Email){
        
        try{
             // HttpRequest is class
        HttpRequest req=new HttpRequest();
        req.setEndPoint('https://api.twilio.com/2010-04-01/Accounts/AC403e94afa7df9476*******************/Messages.json');
        
        req.setMethod('POST');
        
        
        // Authentication || Authorization 
        /// take username(AccountSID) + passoword(AuthToken) and create a Authorization access token using encryption
        /// create a blob string using (Account_SID:Auth Token)
        Blob b=Blob.valueOf('AC403e94afa7df9476d***************:344ec4de0ef16496cf96577f008fb29b');
        // convert b into BASE64 format using ->  EncodingUtil.base64Encode(Blob b);  
        String str=EncodingUtil.base64Encode(b);
        req.setHeader('Authorization','Basic '+str);
        
        // Request Parameter 
        String message='Hello'+Name;
        String body='From='+EncodingUtil.urlEncode('+15074805657','UTF-8')+
                    '&To='+Encodingutil.urlEncode(Phone,'UTF-8') +
                    '&Body='+EncodingUtil.urlDecode(Message,'UTF-8');
        req.setBody(body);
            
         /// HttpResponse is class used to store the response
         HttpResponse res=new HttpResponse();
         /// to send a request use Http class
         Http htp=new Http();
         /// here we send the request to twilio and store the response in res
         res=htp.send(req);
            System.debug(res);
        }catch(Exception e){
            System.debug(e.getMessage());
        }
    }
}
```

## step2 let test this 
### when you will create the Stduent record and see the log you will see a error 
      -> calling an api from trigger is not supported now

## step 3_ lets make this trigger as supported so add this below code before method 
```
    @future(callout=true) /// this is added so that calling an api from trigger is suppoted else without this we will get an error that calling an api from trigger is not supported now that method will be asynchronous that will in queue not mandatory that message will be send immediately

```

### Now full helper class Look like this below 
```
public class sendMessageToStudent {
    
    @future(callout=true) /// this is added so that calling an api from trigger is suppoted else without this we will get an error that calling an api from trigger is not supported now that method will be asynchronous that will in queue not mandatory that message will be send immediately
    public static void myMethod(String Name, String Phone, String Email){
        
        try{
             // HttpRequest is class
        HttpRequest req=new HttpRequest();
        req.setEndPoint('https://api.twilio.com/2010-04-01/Accounts/AC403e94afa7df9****************/Messages.json');
        
        req.setMethod('POST');
        
        
        // Authentication || Authorization 
        /// take username(AccountSID) + passoword(AuthToken) and create a Authorization access token using encryption
        /// create a blob string using (Account_SID:Auth Token)
        Blob b=Blob.valueOf('AC403e94afa7df9********************:344ec4de0ef16496cf96577f008fb29b');
        // convert b into BASE64 format using ->  EncodingUtil.base64Encode(Blob b);  
        String str=EncodingUtil.base64Encode(b);
        req.setHeader('Authorization','Basic '+str);
        
        // Request Parameter 
        String message='Hello'+Name;
        String body='From='+EncodingUtil.urlEncode('+15074805657','UTF-8')+
                    '&To='+Encodingutil.urlEncode(Phone,'UTF-8') +
                    '&Body='+EncodingUtil.urlDecode(Message,'UTF-8');
        req.setBody(body);
            
         /// HttpResponse is class used to store the response
         HttpResponse res=new HttpResponse();
         /// to send a request use Http class
         Http htp=new Http();
         /// here we send the request to twilio and store the response in res
         res=htp.send(req);
            System.debug(res);
        }catch(Exception e){
            System.debug(e.getMessage());
        }
    }
}
```

## step3 -> Now lets add the remote url inside our saleforce org so that this api is allowed to call 
  setup-> search(remote site setting)-> add remote site -> add twilio and url will be base url of twilio api 
  ```
https://api.twilio.com
```

## now go to create a student and you will see that you will get the message on mobile 
