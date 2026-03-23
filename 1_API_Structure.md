# Structure of API

```
@RestResource(urlMapping='/createStudent')   /// that tell compiler that this is a API class 
global class createStudentApi {
    @HttpPost   /// that tell compiler that this is POST method on (/createStudent) route
    global static void myMethod(){
        /// handle the request


        /// process the request


        /// send the response 
    }


   
    @HttpGet
    global static String myMethod2(){
        return 'I am get method';
    }
}
```
