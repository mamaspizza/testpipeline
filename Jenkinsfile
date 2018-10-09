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
            println yaml.text
           }
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            echo 'Failed'

        throw err
    }

}
