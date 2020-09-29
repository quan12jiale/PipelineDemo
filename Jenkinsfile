
@NonCPS
def getRe(str, re, groupID) {
    def x = str =~ re
    if (x.find()) 
    {
        return x.group(groupID)
    }
    else
    {
        return ""
    }
}

pipeline {
    agent any
    
    options { timestamps() }
    
    environment {
        CodeDir = "F:\\Pipeline\\PipelineDemo"
    }
    
    stages {
        stage("Checkout GTJ")
        {
            steps
            {
				build job: 'PipelineDemoSingle'
				echo "build job success"
            }
        }
    }
}

