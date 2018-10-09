node {
    currentBuild.result = "SUCCESS"
    try {
       stage('Test'){
 
           echo 'Test'
           script{
            def docker_hostname = "192.168.23.124"
            def docker_port = "8080"
            def filename = "database.yaml"
            def fullpath = "$env.WORKSPACE\\$filename"
           
            // Read write YAML
            def yaml = readYaml file: filename
            def response
            def url
            // Get DockerID
            def mapDB = [
                PostgreSQL96: "docker.io/postgres:9.6"
                , PostgreSQL98: "docker.io/postgres:10.5"
                , Oracle: "docker.io/oraclelinux:latest"
                , SQLServer: "mcr.microsoft.com/mssql/server:latest"]
            url = "http://$docker_hostname:$docker_port/api/v1/docker/images/all"
            response = httpRequest "$url"
            def baseImages = readJSON text:response.content
            def docker_id
 
            def docker_desc = mapDB[yaml.Database.Type]
            for (def img: baseImages){
                print(docker_desc)
                print(img['description'])
                if ( docker_desc == img['description']) {
                  docker_id = img['id']  
                }
            }
            url = "http://$docker_hostname:$docker_port/api/v1/docker/container/$docker_id"

            // Add docker Image
            response = httpRequest httpMode: "POST", url: "$url", contentType: "APPLICATION_JSON", requestBody: "{\"keepForHours\": 2}"
            def db_info = readJSON text:response.content
            def instance_id = db_info['id']
            yaml.Database.Port = db_info['port']
            yaml.Database.User = db_info['userName']
            yaml.Database.Password = db_info['password']
            print (yaml.Database.Test Me)
            writeYaml file: "new.yaml", data: yaml
            
            url = "http://$docker_hostname:$docker_port/api/v1/docker/container/$instance_id"
            response = httpRequest httpMode: "DELETE", url: "$url"
           }
       }
    }
    catch (err) {
        currentBuild.result = "FAILURE"
            echo 'Failed'
        throw err
    }

}
