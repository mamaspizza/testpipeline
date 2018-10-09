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
            def response
            // Create DB
            response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/images/all'
            def baseImage = readJSON text:response.content
            print(baseImage)
            for (String img: baseImages){
               println img
            }
            
            // try to get docker information
            response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/container/all'
            print("Requested")
            print("Status: "+response.status)
            def json = readJSON text:response.content
            print('j')
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
