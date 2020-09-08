def runParallel = false
def buildStages

// SERVICE=""
SCALA_VERSION="2.12"
ASSEMBLY="-assembly"

AMI_VERSION=0
IsDeployToPROD = false
STAGES = "build_artifacts,build_ami,deploy_to_QA"
QA_REGIONS= ["us-west-2","us-east-1"]
PROD_REGIONS= ["ap-southeast-1","eu-west-1","us-west-2","us-east-1"]
common_envs = [ "API=${SERVICE}", "ASSEMBLY=${ASSEMBLY}" ]

buildAMIInfo = [:]

stage('Parameter Check'){
    node{

        println "$SERVICE"
        TAG = "${params.TAG}"

        try{
            if (TAG == "") {
                throw new Exception("Enter the artifact version for the build in TAG")
            }

            if(TAG.contains("RC") || TAG.contains("SNAPSHOT")){

            }else if(TAG.contains("RELEASE")){
                println "RELEASE"
                IsDeployToPROD = true
            }else{
                throw new Exception("The TAG must include one of name \"RC\", \"SNAPSHOT\", \"RELEASE\" to deploy QA or PROD")
            }
        }catch(e){
            currentBuild.result = "FAILURE"
    //             throw(e)
            println(e)
        }finally{
            common_envs.add("APP_VERSION=${TAG}")
        }

        println "${IsDeployToPROD}"
    }
}