
# Wrapper Class In Salesforce


```
public class WrapperClass {
    public string HospitalName;
    public string HospitalLocation;
    
    List<Doctor> docList = new List<Doctor>();   // data type claaa list
    
    public void adddoctor(String Name, Integer Age, String Speciality ){    // normal data get method
        Doctor doc =new Doctor(Name,Age,Speciality);             // passing values to constructor
        docList.add(doc);    // storing data in list
    }
    
    public void getdoctor(){         // to get data this method used
        for(doctor d: docList){        // iterate over data
            System.debug(d.Name);
             System.debug(d.Age);
             System.debug(d.Speciality);
            
        }
    }

   
     Private class Doctor{      // class 
        private String Name;
        private Integer Age;
        private String Speciality;
        
        Doctor( String Name, Integer Age, String Speciality ){   // constructorr
            this.Name =Name;
            this.Age =Age;
            this.Speciality =Speciality; 
        }
    }
}

```

```
public with sharing class AccountContactWrapper {
    @AuraEnabled(cacheable=true)
    public static List<WrapperClass> getWrapAccountList() {
        return fetchAccountContactData();
    }

    private static List<WrapperClass> fetchAccountContactData() {
        List<WrapperClass> wrapAccountList = new List<WrapperClass>();
        for (Account acc : [SELECT Id, Name, (SELECT Id, Name, Email FROM Contacts) FROM Account LIMIT 100]) {
            wrapAccountList.add(new WrapperClass(acc, acc.Contacts, acc.Contacts.size()));
        }
        System.debug(wrapAccountList);
        return wrapAccountList;
    }

    // This wrapper class 
    public class WrapperClass {
        @AuraEnabled
        public Account acc { get; set; }
        @AuraEnabled
        public List<Contact> conList { get; set; }
        @AuraEnabled
        public Integer contactSize { get; set; }
        @AuraEnabled
        public Boolean isCheck { get; set; }

        public WrapperClass(Account a, List<Contact> cont, Integer countContact) {
            this.acc = a;
            this.conList = cont;
            this.contactSize = countContact;
            this.isCheck = false;
        }
    }
}


```




# To gave data to another org/ we can acces in postman

<img width="518" alt="Screenshot 2024-01-02 111219" src="https://github.com/gaurravlokhande/Javascript-for-Salesforce-Developers-Lwc-Components-1.md/assets/119065314/f28565b5-5507-4a59-9ae2-5902a2c21f45">



# Wrapper Class Selected Accounts multiple
```
https://youtu.be/CWoAGoLjr7c?si=pQvNB5ZwemP7-JiW
```
<img width="510" alt="Screenshot 2024-01-02 125914" src="https://github.com/gaurravlokhande/Javascript-for-Salesforce-Developers-Lwc-Components-1.md/assets/119065314/26cf1200-15e3-4f46-8c3d-5050ab4c4255">

