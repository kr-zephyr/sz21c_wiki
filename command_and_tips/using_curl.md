## curl 사용법

- http url 호출하기  
❯ curl --data "message=Test" http://{{domain}}:6060/send -> POST로 호출됨

- curl post 호출하기  
❯ curl -X POST http://{{domain}}:6180/vcc/v1/optimum -d "{}" -H "Content-Type: application/json"

- TLS 버전을 지정하여 호출  
❯ curl --tlsv1.2 -v https://breeze-developer-prod.apigee.net

#### References
- [https://curl.haxx.se/docs/manual.html](https://curl.haxx.se/docs/manual.html)
