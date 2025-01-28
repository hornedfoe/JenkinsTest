pipeline {
    agent any

    parameters {
        string(name: 'NAMES', defaultValue: 'one,two,three', description: 'Enter comma-separated names')
        string(name: 'VERSIONS', defaultValue: '1.0,2.0,3.0', description: 'Enter comma-separated versions')
    }

    stages {
        stage('Parallel Builds') {
            steps {
                script {
                    // Split the comma-separated parameters into lists
                    def names = params.NAMES.split(',')
                    def versions = params.VERSIONS.split(',')
                    
                    // Create a map to hold the parallel stages
                    def parallelStages = [:]

                    // Loop through the names and versions to create parallel stages
                    for (int i = 0; i < names.size(); i++) {
                        def name = names[i].trim()
                        def version = versions[i].trim()
                        
                        // Add each parallel stage to the map
                        parallelStages["Build ${name} ${version}"] = {
                            stage("Build ${name} ${version}") {
                                echo "Building... Name: ${name}, Version: ${version}"
                                // Add your build, test, deploy steps here
                            }
                        }
                    }

                    // Run the stages in parallel
                    parallel parallelStages
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
