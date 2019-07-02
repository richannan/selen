#!groovy

pipeline {
  agent {
    docker {
      image 'geodynamics/selen-buildenv-bionic:latest'
      alwaysPull true
    }
  }

  options {
    timeout(time: 2, unit: 'HOURS')
  }

  stages {
    stage('Build') {
      steps {
        sh -c 'cd src ; make'
      }
    }

    stage('Test') {
      steps {
        sh -c 'cd DATA ; gunzip *R44*.gz'
        sh -c './sha.exe 44 128 DATA/px-R44.dat DATA/px-lat-R44.dat DATA/sh-R44L128.bin'
        sh -c 'make_sle.sh config.sle.I6G-R44-L128-I33'
      }
    }
  }

  post { always { cleanWs() } }
}
