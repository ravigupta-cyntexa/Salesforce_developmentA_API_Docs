## let first write an API
```
@RestResource(urlMapping='/createStudent')
global class createStudentApi {
    @HttpPost
    global static String myMethod(){
        /// handle the request
        
        
     try{
        // RestContext.request  -> include Header and body of Request and we are putting it inside a object called req(RestContext is a class and request is a variable of RestContext class )
        RestRequest req=RestContext.request;
        // as body is comming in JSON format do we conver it in string format because we need to convert the body in map as we need keyvalue pair to crrate a record so first convert it into string
        String str=req.requestBody.toString(); /// string in JSON format
        // convert string into Map
        // json.deserializeUntyped(str) // that will convert it into json 
        // we do typecastign of map to convert it into map
        Map<String,Object>mapObj=(Map<String,Object>)json.deserializeUntyped(str);
        
        System.debug(mapObj.get('Name'));
        
        /// process the request
         // first check required field 
        if(String.valueOf(mapObj.get('Name'))==null ||String.valueOf(mapObj.get('Email'))==null ){
             return 'Required field Missing ';
        }
         
        Student__c std=new Student__c();
        std.Student_Name__c=String.valueOf(mapObj.get('Name'));
        
        std.Age__c=Integer.valueOf(mapObj.get('Age'));
        
        std.Student_Phone__c=String.valueOf(mapObj.get('Phone'));
        
        std.Student_Email__c=String.valueOf(mapObj.get('Email'));
        
        
         
         // insert std;
         Database.saveResult sr=Database.insert(std,false);
         
         
         
        /// creating response 
         Map<String,Object>resultMap=new Map<String,Object>();
         if(sr.isSuccess()){
             resultMap.put('Status','Success');
             resultMap.put('Id',sr.getId());
             resultMap.put('Name',std.Student_Name__c);
             
         }else{
             List<Database.Error>er=sr.getErrors();
             String error='';
             for(Database.Error err:er){
                 error+=err.getMessage();
             }
             resultMap.put('Status','Error');
             resultMap.put('Message',error);
         }
        /// send the response 
        // converting mapped res structure into string
        String jsonString=JSON.serialize(resultMap);
        return jsonString;
       //  return 'Record is created successfully'+'Student Id is '+ std.id;
            
      }catch(Exception e){
            return e.getMessage();
      }
           
    }
    
    
    @HttpGet
    global static String myMethod2(){
        return 'I am get method';
    }
}
```

## let call this api using (Workbench)
### go to workbench->login with salesforce->Rest Explorer->
### route will be (/services/apexrest/createStudent)
```
```
<img width="1253" height="489" alt="Image" src="https://github.com/user-attachments/assets/01ac6ce2-0052-4666-89ec-8e17f5dd4806" />
