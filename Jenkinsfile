/*
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing,
 * software distributed under the License is distributed on an
 * "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
 * KIND, either express or implied.  See the License for the
 * specific language governing permissions and limitations
 * under the License.
 */
/**
 *
 * Jenkins Pipeline configuration.
 *
 */
node('ubuntu') {

    stage ('Clone Sources') {

        git url: 'https://gitbox.apache.org/repos/asf/archiva-redback-components-parent.git'

    }

    stage ('Build') {
        withMaven(
                // Maven installation declared in the Jenkins "Global Tool Configuration"
                maven: 'Maven 3.5.2', jdk: 'JDK 1.8 (latest)') {
            // Run the maven build
            sh "mvn clean install -B -U -e -fae -Dmaven.compiler.fork=false"

        } // withMaven will discover the generated Maven artifacts, JUnit Surefire & FailSafe & FindBugs reports...
    }

    stage ('Deploy') {
        withMaven(
                maven: 'Maven 3.5.2',
                jdk: 'JDK 1.8 (latest)',
                mavenSettingsConfig: 'DefaultMavenSettingsProvider.1331204114925'
        ) {
            // Run the maven build
            sh "mvn clean deploy -Dmaven.test.skip=true -B -U -e -fae -Dmaven.compiler.fork=false"

        } // withMaven will discover the generated Maven artifacts, JUnit Surefire & FailSafe & FindBugs reports...
    }
}