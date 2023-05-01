## NestJS에서 Socket.io 사용

```
$ npm i --save @nestjs/websockets @nestjs/platform-socket.io
```

## Gateway 파일 생성

```
$ nest g gateway <file-name>
```

## Socket.io의 메소드

### emit

emit 메소드는 클라이언트나 서버에서 이벤트를 보낼 때 사용

### on

on 메소드는 클라이언트나 서버에서 이벤트를 받을 때 사용

## GateWay 생명주기

### OnGatewayInit

OnGatewayInit은 constructor 이후에 실행되는 함수

```
export class ChatsGateway implements OnGatewayInit {
  afterInit() {
    this.logger.log('init');
  }
}
```

### OnGatewayConnection

OnGatewayConnection 클라이언트가 실행되자마자 실행되는 함수

```
export class ChatsGateway implements OnGatewayConnection {
  handleConnection(@ConnectedSocket() socket: Socket) {
    this.logger.log(`connected : ${socket.id} ${socket.nsp.name}`);
  }
}
```

### OnGatewayDisconnect

OnGatewayDisconnect 클라이언트를 새로고침하거나 종료시에 실행되는 함수

```
export class ChatsGateway implements OnGatewayDisconnect {
  handleDisconnect(@ConnectedSocket() socket: Socket) {
    this.logger.log(`disconnected : ${socket.id} ${socket.nsp.name}`);
  }
}
```

## Broadcast

Broadcast는 일반적으로 하나의 송출자가 다수의 수신자에게 정보나 콘텐츠를 전달하는 것을 의미한다. Socket.io에서도 이와 같은 역활을 수행한다.

```
socket.broadcast.emit("user_connected", username)
```

## Chat DB 설계

### sockets.model

```
{
  _id: fskldfjksljfk31356d(ObjectId),
  id: socket.id,
  username: 사용자 이름
}
```

### chattings.model

```
{
  _id: 1231561hf45648u,
  user: {
    _id: fskldfjksljfk31356d(ObjectId),
    id: socket.id,
    username: 사용자 이름
  },
  chat: 채팅 메세지
}
```
