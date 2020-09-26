
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
        choice(name: 'BuildType', choices: 'X86\nX64', description: '��������')
        choice choices: ['VS2015'], description: 'VS�İ汾', name: 'VsVersion'
        choice choices: ['GTJ2021', 'GTJ2018'], description: '��Ʒ�汾', name: 'ProductName'
        
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Build���֧������feature/ �� bugfix/��ǰ׺�Ļ���Ҫ����', name: 'GIT_BRANCH_Build', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Resource���֧������feature/ �� bugfix/��ǰ׺�Ļ���Ҫ����', name: 'GIT_BRANCH_Resource', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'Source���֧������feature/ �� bugfix/��ǰ׺�Ļ���Ҫ����', name: 'GIT_BRANCH_Source', trim: true)
        string(defaultValue: 'r_202006_PublicTrunk', description: 'UnitTest���֧������feature/ �� bugfix/��ǰ׺�Ļ���Ҫ���ϣ�<font color="red">�����������Աȹ���ʱ�ò���</font>', name: 'GIT_BRANCH_Unittest', trim: true)
        
        booleanParam(defaultValue: false, description: '�Ƿ��������Աȹ���', name: 'IsBuildWorkCompareTool')
        
        string(defaultValue: 'shangls-a@glodon.com', description: '����������ɵ��ʼ������б��÷ֺŸ���', name: 'MailList', trim: true)
        
        string(defaultValue: '', description: '�Զ�����������������Ҫ����Ϊʹ��\\\\gtcftp.glodon.com\\Installers\\software\\Pipeline_Memory_Leak ·���µ����°汾��װ����������������', name: 'AutoTestTask', trim: true)
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
                    // ����bat returnStdout: true
                    sVersionInfo = bat returnStdout: true, script: """
@echo off
echo "huadian"
@echo on
                    """
                    echo sVersionInfo
                }
            }
        }
        
        stage('����GMPSDK') {
            steps {
                script {
                    echo "����GMPSDK"
                    
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

