node {
    currentBuild.result = "SUCCESS"
    try {
       stage('Test'){
 
           echo 'Test'
           script{
            def docker_hostname = "192.168.23.124"
            def docker_port = "8080"
            def filename = "database.yaml"
            def fullpath = "${env.WORKSPACE}\\${filename}"
            def config = "some_conf.yaml"
           
            // Read write YAML
            def yaml = readYaml file: filename
            def confyaml = readYaml file: config
            def response
            def url
            // Get DockerID
            def mapDB = [
                "postgresql96": "docker.io/postgres:9.6"
                , "postgresql105": "docker.io/postgres:10.5"
                , "oracle": "docker.io/oraclelinux:latest"
                , "sqlserver": "mcr.microsoft.com/mssql/server:2017-latest"]

            url = "http://${docker_hostname}:${docker_port}/api/v1/docker/images/all"
            response = httpRequest "${url}"
            def baseImages = readJSON text:response.content
            def docker_id
 
            def docker_desc = mapDB["sqlserver"]
            for (def img: baseImages){
                print(docker_desc)
                print(img['description'])
                if ( docker_desc == img['description']) {
                  docker_id = img['id']  
                }
            }
            url = "http://${docker_hostname}:${docker_port}/api/v1/docker/container/${docker_id}"

            // Add docker Image
            response = httpRequest httpMode: "POST", url: "${url}", contentType: "APPLICATION_JSON", requestBody: "{\"keepForHours\": 2}"
            def db_info = readJSON text:response.content
            def instance_id = db_info['id']
            yaml['Installation'] = confyaml['Installation']
            yaml['Database']['Port'] = db_info['port']
            yaml['Database']['User'] = db_info['userName']
            yaml['Database']['Password'] = db_info['password']
            yaml['Database']['New'] = "This is a new attribute"
            
            writeYaml file: "new.yaml", data: yaml
            
            // Read write YAML
            def n_yaml = readYaml file: "new.yaml"
            print (n_yaml.Database['Test Me'])
            
               url = "http://${docker_hostname}:${docker_port}/api/v1/docker/container/${instance_id}"
               response = httpRequest httpMode: "DELETE", url: "${url}"
           }
       }
    }
    catch (err) {
        currentBuild.result = "FAILURE"
            echo 'Failed'
        throw err
    }

}
