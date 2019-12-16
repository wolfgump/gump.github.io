# Camunda QA

Q:[Gateway Default Flow](https://forum.camunda.org/t/gateway-default-flow/447)

A:Just mark the sequence flow and click the wrench symbol in the mouse menu and select ‘default flow’.

Q:http-connector-rest-post-payload

A:https://forum.camunda.org/t/http-connector-rest-post-payload/4947

Q:send email

A:

URL:http://open-test.zmlearn.com/api/bus/push

Method:POST

headers:Map  content-type:application/json accept:application/json

Payload:

``` 
var traceId= execution.getId();
var request='{"data": "{\\\"email\\\":\\\"19878787534\\\"}","event": "flow-test","source": "客户端","traceId": "'+traceId+'"}';
execution.setVariable("request",request);
'{"data": "{\\\"email\\\":\\\"19878787534\\\"}","event": "flow-test","source": "客户端","traceId": "'+traceId+'"}';```
```