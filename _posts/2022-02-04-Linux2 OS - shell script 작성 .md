``` shell
#!/bin/bash

REPOSITORY=/home/ec2-user/app/back/booking_service_back
PROJECT_NAME=booking_service_01
PACAKE_NAME=board_web_00-0


cd $REPOSITORY/$PROJECT_NAME/

echo "> git pull"
git pull
./mvnw clean install
cd $REPOSITORY

echo "> Build 파일 복사"
cp $REPOSITORY/$PROJECT_NAME/target/*.jar $REPOSITORY/

echo "> 현재 구동중인 애플리케이션 pid 확인"
CURRENT_PID=$(pgrep -f ${PACAKE_NAME}.*.jar)

echo "현재 구동 중인 애플리케이션 pid: $CURRENT_PID"

if [ -z "$CURRENT_PID" ]; then
        echo "> 현재 구동 중인 애플리케이션이 없으므로 종료하지 않습니다."
else
        echo "> kill -9 $CURRENT_PID"
        kill -9 $CURRENT_PID
    sleep 5
fi

echo "> 새 애플리케이션 배포"

JAR_NAME=$(ls -tr $REPOSITORY/ | grep jar | tail -n 1)
echo "> JAR Name: $JAR_NAME"

nohup java -jar $REPOSITORY/$JAR_NAME 2>&1 &

sleep 10
netstat -tnlp
```

