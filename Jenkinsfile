pipeline {
    agent any

    stages {
        
        stage("Build_Dev") {
            when { expression { env.BRANCH_NAME == 'dev'} }
            steps {
                echo "Building Testing Lab!"
                sh """
                source /home/kamil/yetAnotherVirtualEnv/testing_env/bin/activate

                """
                //python3 /var/lib/jenkins/workspace/Hons_Project_dev/eve_api.py -ip 192.168.78.148 -t /Uni2021/hons_test.unl -u
                //sleep 480
            }
        }
        stage("Deploy_Dev") {
            when { expression { env.BRANCH_NAME == 'dev'} }
            steps {
                echo "Deploying Configuration To The Testing Lab"
                sh """
                source /home/kamil/yetAnotherVirtualEnv/testing_env/bin/activate
                python3 /var/lib/jenkins/workspace/Hons_Project_dev/NETCONF_jinja_push_test.py
                """
            }
        }
        stage("Test_Dev") {
            when { expression { env.BRANCH_NAME == 'dev'} }
            steps {
                echo "Testing The Deployed Configuration"
                sh """
                source /home/kamil/yetAnotherVirtualEnv/testing_env/bin/activate
                python3 /home/kamil/Hons/test_interfaces.py
                python3 /home/kamil/Hons/test_ospf.py
                python3 /home/kamil/Hons/test_bgp.py
                python3 /home/kamil/Hons/test_vpn.py
                """
                //python3 /var/lib/jenkins/workspace/Hons_Project_dev/eve_api.py -ip 192.168.78.148 -t /Uni2021/hons_test.unl -d
            }
        }
    }
}
