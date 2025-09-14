pipeline {
    agent {label 'ubuntu'}
    
    parameters {
        choice choices: ['BRANCH', 'TAG', 'BRANCH_and_TAG', 'REVISION', 'PULL_REQUESTS'], description: '', name: 'TYPE'
        gitParameter (  branch: '',
                        branchFilter: '.*',
                        defaultValue: 'main',
                        description: '',
                        name: 'BRANCH',
                        quickFilterEnabled: true,
                        selectedValue: 'NONE',
                        sortMode: 'NONE',
                        tagFilter: '*',
                        type: 'PT_BRANCH',
                        useRepository: 'git@github.com:Primero-QA/java_for_testers.git')
        gitParameter (  branch: '',
                        branchFilter: '.*',
                        defaultValue: 'main',
                        description: '',
                        name: 'TAG',
                        quickFilterEnabled: true,
                        selectedValue: 'NONE',
                        sortMode: 'NONE',
                        tagFilter: '*',
                        type: 'PT_TAG',
                        useRepository: 'git@github.com:Primero-QA/java_for_testers.git')
        gitParameter (  branch: '',
                        branchFilter: '.*',
                        defaultValue: 'main',
                        description: '',
                        listSize: '10',
                        name: 'BRANCH_and_TAG',
                        quickFilterEnabled: true,
                        selectedValue: 'NONE',
                        sortMode: 'NONE',
                        tagFilter: '*',
                        type: 'PT_BRANCH_TAG',
                        useRepository: 'git@github.com:Primero-QA/java_for_testers.git')
        gitParameter (  branch: '',
                        branchFilter: '.*',
                        defaultValue: 'main',
                        description: '',
                        name: 'REVISION',
                        quickFilterEnabled: true,
                        selectedValue: 'NONE',
                        sortMode: 'NONE',
                        tagFilter: '*',
                        type: 'PT_REVISION',
                        useRepository: 'git@github.com:Primero-QA/java_for_testers.git')
        gitParameter (  branch: '',
                        branchFilter: '.*',
                        defaultValue: 'main',
                        description: '',
                        name: 'PULL_REQUESTS',
                        quickFilterEnabled: true,
                        selectedValue: 'NONE',
                        sortMode: 'NONE',
                        tagFilter: '*',
                        type: 'PT_PULL_REQUEST',
                        useRepository: 'git@github.com:Primero-QA/java_for_testers.git')
    }
    
    stages {
        stage('Delete workdir') {
            steps {
                echo 'Deleting workdir...'
                deleteDir()
            }
        }
        stage('Print env') {
            steps {
                sh '''
                    echo Selected type of checkout: $TYPE
                    echo Selected Branch: $BRANCH
                    echo Selected Tag: $TAG
                    echo Selected Branch or Tag: $BRANCH_and_TAG
                    echo Selected Revision name: $REVISION
                    echo Selected Pull request: $PULL_REQUESTS
                '''
            }
        }
        stage('Checkout') {
            parallel {
                stage('BRANCH') {
                    when {
                        expression {params.TYPE == 'BRANCH'}
                    }
                    steps {
                        checkout(
                            [$class: 'GitSCM',
                            branches: [[name: "${params.BRANCH}"]],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            submoduleCfg: [], userRemoteConfigs:
                            [[credentialsId: 'github-ssh-creds',
                            url: 'git@github.com:Primero-QA/java_for_testers.git']]]
                        )
                    }
                }
                stage('TAG') {
                    when {
                        expression {params.TYPE == 'TAG'}
                    }
                    steps {
                        checkout(
                            [$class: 'GitSCM',
                            branches: [[name: "${params.TAG}"]],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            submoduleCfg: [], userRemoteConfigs:
                            [[credentialsId: 'github-ssh-creds',
                            url: 'git@github.com:Primero-QA/java_for_testers.git']]]
                        )
                    }
                }
                stage('BRANCH_and_TAG') {
                    when {
                        expression {params.TYPE == 'BRANCH_and_TAG'}
                    }
                    steps {
                        checkout(
                            [$class: 'GitSCM',
                            branches: [[name: "${params.BRANCH_and_TAG}"]],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            submoduleCfg: [], userRemoteConfigs:
                            [[credentialsId: 'github-ssh-creds',
                            url: 'git@github.com:Primero-QA/java_for_testers.git']]]
                        )
                    }
                }
                stage('REVISION') {
                    when {
                        expression {params.TYPE == 'REVISION'}
                    }
                    steps {
                        checkout(
                            [$class: 'GitSCM',
                            branches: [[name: "${params.REVISION}"]],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            submoduleCfg: [], userRemoteConfigs:
                            [[credentialsId: 'github-ssh-creds',
                            url: 'git@github.com:Primero-QA/java_for_testers.git']]]
                        )
                    }
                }
                stage('PULL_REQUESTS') {
                    when {
                        expression {params.TYPE == 'PULL_REQUESTS'}
                    }
                    steps {
                        checkout(
                            [$class: 'GitSCM',
                            branches: [[name: "pr/${params.PULL_REQUESTS}/head"]],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [],
                            submoduleCfg: [], userRemoteConfigs:
                            [[credentialsId: 'github-ssh-creds',
                            refspec: '+refs/pull/*:refs/remotes/origin/pr/*',
                            url: 'git@github.com:Primero-QA/java_for_testers.git']]]
                        )
                    }
                }
            }
        }
        stage('ls for dir') {
            steps {
                sh 'ls -la'
            }
        }
    }
}
