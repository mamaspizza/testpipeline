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
            // remove the file first
            def oldfile = "$env.WORKSPACE\\new.yaml"
            bat """
                del  $oldfile
            """
            writeYaml file: "new.yaml", data: yaml
            
            // try to get docker information
            def response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/container/all'
            print("Status: "+response.status)
            print("Content: "+response.content)
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
