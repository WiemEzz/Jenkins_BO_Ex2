pipeline {
  agent any
  stages {
    stage('stage1') {
      steps {
        sh '''cat /etc/passwd | cut -d: -f1,3 >userId
for i in `more /etc/passwd | cut -d: -f 1,3` ;
do
user=`echo $i | cut -d: -f1` ;
idgroup=`echo $i | cut -d: -f2` ;
group=`grep :$idgroup: /etc/group | cut -d: -f1` ;
echo " $user:$group" >> usergroup

done
'''
      }
    }

    stage('Stage2') {
      steps {
        sh ''' cat /etc/passwd |cut -d: -f4>idgroup
sort idgroup |uniq>idgroupf
'''
      }
    }

    stage('Stage3') {
      steps {
        sh ''' cat /etc/group |cut -d: -f3>allgroup
 sort allgroup |uniq>allgroupf

'''
      }
    }

    stage('stage4') {
      steps {
        sh '''diff -y -W 50 idgroupf allgroupf>result
exit [0]
'''
      }
    }

  }
}