pipeline {
    agent {
        docker {
            image 'vinodavk/ana:node-10.15.0'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('getting the code and building the package') {
            steps {
              if [ ${git show --name-only --pretty=""} == packages/react-apps/mypeegu-pwa/* ];
              then
                    cd "${WORKSPACE}" && git pull origin master
                    cp "${WORKSPACE}"/.env.mp  ${WORKSPACE}/.env
                    cd "${WORKSPACE}" && npx lerna bootstrap --scope mypeegu-pwa
                    cd "${WORKSPACE}" && npx lerna run build --scope mypeegu-pwa

              elif [ ${git show --name-only --pretty=""} == packages/react-apps/anytime-clap-talk-pwa/* ];
              then
                  cd "${WORKSPACE}" && git pull origin master
                  cp "${WORKSPACE}"/.env.act  ${WORKSPACE}/.env
                  cd "${WORKSPACE}" && npx lerna bootstrap --scope anytime-clap-talk-pwa
                  cd "${WORKSPACE}" && npx lerna run build --scope anytime-clap-talk-pwa
            else 
                echo "These projects are not defined"
            fi
          }
        }
    }
}
