#### **We are exploring the field level security**

* In ReadMe_basic_security.Md file ,We have setup the elastic search with basic security and we are going to create user and roles to fetch only fields which are allowed as per roles now.
* Please follow below steps :
    * First of All basic elastic search licence does not support this field level and document level security is not supported
    * you can check more details here :  
        * https://discuss.elastic.co/t/security-exception-current-license-is-non-compliant-for-security-with-license-expired-feature-security/97351
        * You can make the existing elastic search for free trial a month : https://www.elastic.co/guide/en/elasticsearch/reference/current/start-trial.html
        
    * Once you started the free trial follow below steps
        * Using the ReadMe_input_kibana_query file, We will demonstrates the Role base ,Field level security
        * Create a document in customer index
        * Search all the document in customer index
        * create my_admin_role, query mentioned in files(ReadMe_input_kibana_query)
        * Create user (jacknich) mention in file(ReadMe_input_kibana_query)
        
        * You can verify the changes ,User is created in (User board of Kibana)
        * once the User is created and role is assigned to it. We are all setup.
    * Now time to verify the document fetch :
        ```
       curl -u jacknich:j@rV1s 'http://localhost:9200/customer/_search'
      ```        
      * response is :
        ```
         {"took":15,"timed_out":false,"_shards":{"total":1,"successful":1,"skipped":0,"failed":0},"hits":{"total":{"value":1,"relation":"eq"},"max_score":1.0,"hits":[{"_index":"customer","_type":"_doc","_id":"1","_score":1.0,"_source":{"title":"Titles from doucment 1","body":"body of document 1"}}]}}
        ``` 
        * You can see in response only   Title,Body is return,This is because ,We have given the index : customer and fields are ['title','body'']
        
 * This is how ,Field level security works
 * Links to refer :
    * https://www.elastic.co/guide/en/elasticsearch/reference/current/field-level-security.html
    * https://www.elastic.co/guide/en/elasticsearch/reference/current/field-and-document-access-control.html#multiple-roles-dls-fls
    * https://opendistro.github.io/for-elasticsearch-docs/docs/security-access-control/field-level-security/        
            
