## we have  a Response like below
```

{
  "distance": 0,
  "emailAddress": "address@email.com",
  "firstName": "Arpit",
  "headLine": "The World News",
  "pictureURL": "https://www.nylas.com/wp-content/uploads/JSON_Blog_Hero.png",
  "positions": {
    "total": 1,
    "values": [
      {
        "company": {
          "id": 451259,
          "industry": "Information Technology & Services",
          "name": "Tesla Inc.",
          "size": "1200+",
          "ticker": "TLA78541PU9",
          "type": "Public Domain"
        },
        "id": 54123659,
        "isCurrent": true,
        "location": {
          "latitude": 48.856613,
          "longitude": 2.352222
        },
        "title": "Engineer Department"
      }
    ]
  }
}
```

## Now we want to create a wrapper class for this 
we create the wrapper class to get the response like this above and we have given a jsonString 
so wrapper class is used to create a JSON structure details till nested child from a json string 
#### wrapper class
wrapper class will be created according to our required json above
```
public class wrapperForJson {
    public Integer distance;
    public String emailAddress;
    public String firstName;
    public string headLine;
    public String pictureURL;
    public String publicProfileURL;
    /// create a variable of class 
    public positionsClass positions;
    
    
    public class positionsClass{
        public Integer total;
        // public List<Values>values=new List<Values>();
        // or
        public Values[] values;
        
        
    }
    
    public class Values{
        public String id;
        public String isCurrent;
        public String title;
        /// create company class variable
        public companyClass company;
        public locationClass location;
    }
    
    public class companyClass{
        public String id;
        public String industry;
        public String name;
        public String size;
        public String ticker;
        public String type;
    }
    public class locationClass{
        public String latitude;
        public String longitude;
    }
}


```

## lets call and debug the json 
we have a JsonString 
```
'distance=0, emailAddress=address@email.com, firstName=Arpit, headLine=The World News, pictureURL=https://www.nylas.com/wp-content/uploads/JSON_Blog_Hero.png, positions=positionsClass:[total=1, values=(Values:[company=companyClass:[id=451259, industry=Information Technology & Services, name=Tesla Inc., size=1200+, ticker=TLA78541PU9, type=Public Domain], id=54123659, isCurrent=true, location=locationClass:[latitude=48.856613, longitude=2.352222], title=Engineer Department]) format in correct json'
```
### lets call this 
```
String jsonString='{\n    \"distance\" : 0,\n    \"emailAddress\" : \"address@email.com\",\n    \"firstName\" : \"Arpit\",\n    \"headLine\" : \"The World News\",\n    \"lastName\" : \"Gupta\",\n    \"pictureURL\" : \"https://www.nylas.com/wp-content/uploads/JSON_Blog_Hero.png\",\n    \"positions\" : {\n        \"total\" : 1,\n        \"values\" : [\n            {\n                \"company\" : {\n                    \"id\" : 451259,\n                    \"industry\" : \"Information Technology & Services\",\n                    \"name\" : \"Tesla Inc.\",\n                    \"size\" : \"1200+\",\n                    \"ticker\" : \"TLA78541PU9\",\n                    \"type\" : \"Public Domain\"\n                },\n                \"id\" : 54123659,\n                \"isCurrent\": true,\n                \"location\" : {\n                    \"latitude\" : \"48.856613\",\n                    \"longitude\" : \"2.352222\"\n                },\n                \"title\" : \"Engineer Department\"\n            }\n        ]\n    },\n    \"publicProfileURL\" : \"https://www.zip.com/9875/usad\"\n}';
wrapperForJson wfj=(wrapperForJson)JSON.deserialize(jsonString,wrapperForJson.class);
// companyClass cc=new companyClass();

System.debug(wfj.positions.values[0].company.industry);
```
