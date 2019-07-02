//需要編譯的紀錄,因為沒有set,因此用Map作為替代
def waitForCompile = [:]

node {
        stage('偵測需編譯的部分') {
            //取得現在的版本
            checkout scm                 
            //取得這次的變動資訊
            def changeLogSets = currentBuild.changeSets
                for (int i = 0; i < changeLogSets.size(); i++) {
                        def entries = changeLogSets[i].items
                                for (int j = 0; j < entries.length; j++) {
                                def entry = entries[j]
                                entry.getAffectedPaths().each {                      
                                        //echo "Change detected: ${it}"
                                        //如果更動內容的路徑符合條件,則記錄該資料夾名稱
                                        if(it.startsWith("microservice")){
                                             def subproject = it.substring(0,it.indexOf("/"))
                                             echo "${subproject} is need to compile"
                                             waitForCompile.put(subproject,"");   
                                        }
                                }
                        }
                    }
        }
        stage('開始編譯') {
             checkout scm
             echo "Strat compile"
             def keys =  waitForCompile.keySet();
             //按資料夾分別執行其中的pom檔案   
             for (folder in keys) {        
                echo "Compile... ${folder} start"
                //sh 'mvn -f microservice-discovery-eureka/pom.xml package'        
                sh 'mvn -f '+folder+'/pom.xml package'
                echo "Compile... ${folder} end"   
             }
             echo "End compile"
            //sh 'mvn package'
        }        
}


