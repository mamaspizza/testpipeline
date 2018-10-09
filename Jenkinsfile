node {
    currentBuild.result = "SUCCESS"
    try {
       stage('Test'){
           echo 'Test'
           script{
            def filename = "database.yaml"
            def fullpath = "$env.WORKSPACE\\$filename"
           
            // Read write YAML
            def yaml = readYaml file: fullpath
            def response
            // Get DockerID
            def mapDB = [
                PostgreSQL96: "docker.io/postgres:9.4"
                , PostgreSQL98: "docker.io/postgres:latest"
                , Oracle: "docker.io/oraclelinux:latest"
                , SQLServer: "mcr.microsoft.com/mssql/server:latest"]
            response = httpRequest 'http://192.168.23.124:8080/api/v1/docker/images/all'
            def baseImages = readJSON text:response.content
            def docker_id
            print yaml.Database.Type
            def docker_desc = mapDB[yaml.Database.Type]
            for (def img: baseImages){
                print(docker_desc)
                print(img['description'])
                if ( docker_desc == img['description']) {
                  docker_id = img['id']  
                }
            }            
            response = httpRequest httpMode: 'POST', url: 'http://192.168.23.124:8080/api/v1/docker/container/$docker_id', requestBody: "{\"keepForHours\": 2}"
                        
            response = httpRequest httpMode: 'DELETE', url: 'http://192.168.23.124:8080/api/v1/docker/container/$docker_id'
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
