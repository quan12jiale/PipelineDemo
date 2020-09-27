
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
				script 
				{
					def sGMPCmake = readFile "F:\\GTJ\\source\\CMake\\tools\\pkguser\\pkgs\\GMP.cmake"
					def zipURL = getRe(sGMPCmake, "URL\\s*\\\"([^\\\"]*)\\\"", 1)
					echo zipURL
					
					sWin32OrX64 = "Win32";
					def sDBuildType = (sWin32OrX64 == "Win32" ? "X64" : "Win32")
					echo sDBuildType
				}
            }
        }
    }
}

