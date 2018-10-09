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
            def fullp = "$env.WORKSPACE\\$filename"
            print(fullp)
            File yaml = new File(fullp)
            print(yaml.text)
            def newType = "Oracle"
            yaml.text = yaml.text.replaceFirst(/Type: '.*'/, "Type: '${newType}'")
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
