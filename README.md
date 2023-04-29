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