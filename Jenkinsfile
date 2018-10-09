node {


    currentBuild.result = "SUCCESS"

    try {
       stage('Test'){
           echo 'Test'
           script{
            print(env.WORKSPACE)
            // File yaml = new File("test.yaml")
            // println yaml.text   
            writeFile file: "test.yaml", text: "Type: PostgreSQL"
            def filename = "test.yaml"
            print(filename)
            def fullp = "$env.WORKSPACE\\$filename"
            print(fullp)
            //File raw = new File(fullp)
            //print(raw.text)
            //raw.text.replaceFirst("Type: PostgreSQL", "Type: Oracle")
            //print(raw.text)
            // Read write YAML
            def yaml = readYaml file: fullp
            yaml.Type = "Oracle"
            writeYaml file: "new.yaml", data: yaml
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
