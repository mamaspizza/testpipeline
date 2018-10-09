node {
    currentBuild.result = "SUCCESS"
    try {
       stage('Test'){
           echo 'Test'
           script{
            def filename = "database.yaml"
            def fullp = "$env.WORKSPACE\\$filename"

            // Read write YAML
            def yaml = readYaml file: fullp
            def response
            // Create DB
            response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/images/all'
            def baseImages = readJSON text:response.content

            for (def img: baseImages){
               println img['id']
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
