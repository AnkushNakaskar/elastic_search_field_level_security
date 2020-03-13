#### **Field level authentication in elastic search**
* Steps :
    * Install elastic search using 
        * curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.6.1-darwin-x86_64.tar.gz
        * tar -xvf elasticsearch-7.6.1-darwin-x86_64.tar.gz
        * open config/elasticsearch.yml -> add (xpack.security.enabled: true)
            * This adds the security for elastic search and kibana in the same way,I will explain the Kibana in different file.
            * Since  we are not aware of password for build in users for elasticsearch
                * Run the below cmd to reset the elastic search username and password
                    * CMD (./bin/elasticsearch-setup-passwords auto -u "http://localhost:9200")
                    * It will print the username and password for build in user
                    * for every query, we will invoke in elastic search ,We need to provide the user(Build in user)
                        * You can use the build in user(which has roles as superuser) is : **elastic**
         * Test configuration by invoking :
            * ```curl -u elastic:<password for elastic> http://localhost:9200/```
            * We should get response as health and details of elastic search
            
     * Setup Kibana :
        * Install Kibana Steps :
            *  curl -O https://artifacts.elastic.co/downloads/kibana/kibana-7.6.1-linux-x86_64.tar.gz
            *  curl https://artifacts.elastic.co/downloads/kibana/kibana-7.6.1-linux-x86_64.tar.gz.sha512 | shasum -a 512 -c - 
            *  tar -xzf kibana-7.6.1-linux-x86_64.tar.gz
            *  cd kibana-7.6.1-linux-x86_64/ 
        * Since we have added security using config ( xpack.security.enabled: true)
            * This has disable the kibana to connect with elasticsearch
            * We need to setup built in user for kibana to connect with elastic search as below :
                * open ./config/kibana.yml
                * Add below details :
                    ```
                  elasticsearch.username: "kibana"
                  elasticsearch.password: "<The password for kibana generated while settting password for elastic>"
                  ```
                                      
        * Now connect the Kibana using 
            ```http://localhost:5601```
        * Since we have added the security details in elastic and kibana ,You can view these details in Kibana board as (security -> Users,Roles)
    * Now we will proceed for User base(Field level security) in next document
    * Link for refer : https://medium.com/@Sushil_Kumar/setting-up-rbac-in-elasticsearch-with-kibana-195f07cd74a9                                                                                    