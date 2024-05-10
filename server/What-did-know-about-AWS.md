# What did know about AWS

1. 키 페어의 .pem은 safari에서 받아진다. 크롬에서는 .cer로 받아진다.
2. 반드시 키는 400 권한을 부여해라.
3. 키 페어로 ssh 접근 시 사용자 명은 ec2-user이다.
    - 다음과 같이 access 할 수 있다.
    - ```ssh -i {{key_file}} ec2-user@{{ec2-instance-public-domain}}```