@Library('jenkinslib') _

def tools =  new org.devops.tools()




pipeline {
    agent any

    options {
        timestamps()
        skipDefaultCheckout()
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
    }

    stages {
        stage('拉取代码') {
            when { environment name:'test', value:'abcd'}
            steps{
                timeout(time: 5, unit: 'MINUTES'){
                    script{//填写运行代码
                        println('代码仓库获取代码')
                    }
                }
            }
        }
        stage('测试并行') {
            failFast true
            parallel{
                stage('maven构建') {
                    steps{
                        timeout(time: 5, unit: 'MINUTES'){
                            script{//填写运行代码
                                println('MVN打包构建')
                            }
                        }
                    }
                }
                stage('发布镜像') {
                    steps{
                        timeout(time: 5, unit: 'MINUTES'){
                            script{//填写运行代码
                                println('DOCKER发布镜像')
                                //input id: 'Test', message: '我们是否要继续？', ok: '是，我们继续吧', parameters: [choice(choices: ['a', 'b'], name: 'test')], submitter: 'shilf,root'
                            }
                        }
                    }
                }
            }
        }



        stage('部署到k8s集群') {
            steps {
                timeout(time: 5, unit: 'MINUTES'){
                    script{//填写运行代码
                        println('部署k8s集群')
                        tools.PrintMes('this is a jenkinslib!')
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                println('总是执行的脚本片段')
            }
        }

        success {
            script {
                currentBuild.description = '\n 构建成功'
            }
        }

        failure {
            script {
                currentBuild.description = '\n 构建失败'
            }
        }

        aborted {
            script {
                currentBuild.description = '\n 构建取消'
            }
        }
    }
}
