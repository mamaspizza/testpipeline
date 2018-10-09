node {


    currentBuild.result = "SUCCESS"

    try {
       stage('Test'){
           echo 'Test'
           script{
            print(env.WORKSPACE)
            // File yaml = new File("test.yaml")
            // println yaml.text   
            writeFile file: "test.yaml", text: "Database: \n Type: PostgreSQL"
            def filename = "test.yaml"
            print(filename)
            File yaml = new File("$env.WORKSPACE\$filename")
            print(yaml.text)
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
