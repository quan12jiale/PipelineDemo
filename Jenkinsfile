
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
    
    parameters {
        choice(name: 'BuildType', choices: 'X86\nX64', description: '构建类型')
        choice choices: ['VS2015'], description: 'VS的版本', name: 'VsVersion'
        choice choices: ['GTJ2021', 'GTJ2018'], description: '产品版本', name: 'ProductName'
        
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Build库分支名，有feature/ 、 bugfix/等前缀的话需要带上', name: 'GIT_BRANCH_Build', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Resource库分支名，有feature/ 、 bugfix/等前缀的话需要带上', name: 'GIT_BRANCH_Resource', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Source库分支名，有feature/ 、 bugfix/等前缀的话需要带上', name: 'GIT_BRANCH_Source', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'UnitTest库分支名，有feature/ 、 bugfix/等前缀的话需要带上，<font color="red">不构造做法对比工具时用不到</font>', name: 'GIT_BRANCH_Unittest', trim: true)
        
        booleanParam(defaultValue: false, description: '是否构造做法对比工具', name: 'IsBuildWorkCompareTool')
        
        string(defaultValue: 'shangls-a@glodon.com', description: '任务运行完成的邮件发送列表，用分号隔开', name: 'MailList', trim: true)
        
        string(defaultValue: '', description: '自动化任务名（任务需要调整为使用\\\\gtcftp.glodon.com\\Installers\\software\\Pipeline_Memory_Leak 路径下的最新版本安装包），留空则不运行', name: 'AutoTestTask', trim: true)
    }
    
    environment {
        CodeDir = "F:\\Pipeline\\PipelineDemo"
    }
    
    stages {
        stage("Checkout GTJ")
        {
            steps
            {
	echo "start build"
                echo "current branch: ${env.BRANCH_NAME}"
                script {
                    // 测试bat returnStdout: true
                    sVersionInfo = bat returnStdout: true, script: """
@echo off
echo "huadian"
@echo on
                    """
                    echo sVersionInfo
                }
            }
        }
        
        stage('构建GMPSDK') {
            steps {
                script {
                    echo "构造GMPSDK"
                    
                    def sText = readFile "${CodeDir}\\branch1.txt"
                    echo sText
                    def sGLDPath = getRe(sText, "GLDVer\\=(\\S*)", 1)
                    if (sGLDPath.indexOf("ftp") != 0)
                    {
                        sGLDPath = sGLDPath.replaceAll("\\/", "\\\\")
                    }
                    echo sGLDPath
                    
                    echo "end build"
                }
            }
        }
    }
}

