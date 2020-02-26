젠킨스 설정 하는법


# jenkins사용자를 만듭니다 (이는 배포시 사용할 유저 입니다.)
sudo useradd -g tomcat -d /opt/tomcat jenkins

# jenkins의 비밀번호 설정시 잠시 멈추고 사용자의 입력을 기다리므로 입력바람.
sudo passwd jenkins
##### 패스워드 입력


# jenkins(group:tomcat)가 /opt/tomcat/webapps에 *.war파일을 업로드(쓰기)할 수 있도록 권한주기
sudo chmod g+w /opt/tomcat/webapps

# jenkins에게 sudo를 비밀번호 없이 입력하게 허용
sudo nano /etc/sudoers
# 마지막줄에 추가.
# systemctl 명령어만 sudo 권한을 줌.

# for jenkins deploy
jenkins ALL=NOPASSWD: /bin/systemctl * tomcat
# 그냥 jenkins만 추가하고 ssh를 reload하게 되면 ubuntu와 jenkins 모두 로그인 못하게 된다.
#Edit /etc/ssh/sshd_config and set PasswordAuthentication to yes.
sudo nano /etc/ssh/sshd_config
# update ssh
sudo service ssh reload
