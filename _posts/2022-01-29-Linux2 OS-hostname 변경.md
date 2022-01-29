[ec2-user@before-host-name] ` $ hostname `

before-host-name.internal

[ec2-user@before-host-name] ` $ cat /etc/hostname `

before-host-name.internal

[ec2-user@before-host-name] `$ sudo hostnamectl set-hostname new-host-name `

[ec2-user@before-host-name] `$ cat /etc/hostname `

new-host-name

[ec2-user@before-host-name] `$ sudo reboot `

[ec2-user@new-host-name ~] $ 



Linux2 OS 에서 ` hostnamectl set-hostname ` 명령어를 사용해 hostname 을 변경

