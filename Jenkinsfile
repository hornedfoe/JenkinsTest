pipeline {
    agent any

    parameters {
        string(name: 'NAMES', defaultValue: 'one,two,three', description: 'Enter comma-separated names')
        string(name: 'VERSIONS', defaultValue: '1.0,2.0,3.0', description: 'Enter comma-separated versions')
        string(name: 'PLATFORMS', defaultValue: 'Mac,Win', description: 'Enter comma-separated versions')
    }

    stages {
        stage('Parallel Builds') {
            
            steps {
                script {
                    def platforms = params.PLATFORMS.split(",")
                    
                    def parallelPlatforms = [:]
                    
                    for (int i = 0; i < platforms.size(); i++) {
                      
                        def platform = platforms[i].trim()
                      
                        steps {
                          
                            script {
                                // Split the comma-separated parameters into lists
                                def names = params.NAMES.split(',')
                                def versions = params.VERSIONS.split(',')
                                
                                // Create a map to hold the parallel stages
                                def parallelStages = [:]
            
                                // Loop through the names and versions to create parallel stages
                                for (int j = 0; j < names.size(); j++) {
                                    def name = names[j].trim()
                                    def version = versions[j].trim()
                                    
                                    // Add each parallel stage to the map
                                    parallelStages["Build ${name} ${version}"] = {
                                        stage("Build ${name} ${version}") {
                                            echo "Building... Name: ${name}, Version: ${version}"   
                                        }
                                        stage("Test ${name} ${version}") {
                                            echo "Testing... Name: ${name}, Version: ${version}"
                                        }
                                        stage("Deploy ${name} ${version}") {
                                            echo "Deploying... Name: ${name}, Version: ${version}"
                                        }
                                    }
                                }
                                
                                parallelPlatforms["${platform}"] = parallelStages
                            }
                        }
                    }
                    parallel parallelPlatforms
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
