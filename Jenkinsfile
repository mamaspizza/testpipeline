node {
    currentBuild.result = "SUCCESS"
    try {
       stage('Test'){
           echo 'Test'
           script{
            def filename = "database.yaml"
            def fullp = "$env.WORKSPACE\\$filename"
            print(fullp)
            // Read write YAML
            def yaml = readYaml file: fullp
            
            // Create DB
            
            
            // try to get docker information
            def response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/container/all'
            print("Status: "+response.status)
            def json response.content
            print($json)
            print(json['userName'])
            
            
            //writeYaml file: "new.yaml", data: yaml
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
