node {


    currentBuild.result = "SUCCESS"

    try {
       stage('Test'){
           echo 'Test'
           script{
            writeFile file: "database.yaml", text: "Type: PostgreSQL"
            def filename = "test.yaml"
            print(filename)
            def fullp = "$env.WORKSPACE\\$filename"
            print(fullp)
            
            // Read write YAML
            def yaml = readYaml file: fullp
            yaml.Type = "Oracle"
            writeYaml file: "new.yaml", data: yaml
            
            // try to get docker information
            url = "http://192.168.23.124:8080/api/v1/docker/container/all"
            def client = new RESTClient(url)
            def response = client.get()
            print(response.data)
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
