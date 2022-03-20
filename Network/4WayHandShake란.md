# 4 Way Handshake
## 정의
: 네트워크 환경에서 서버와 클라이언트의 세션을 종료하기 위한 프로세스

## 방식
### 1. Client             ------ FIN -----> Server
    클라이언트가 서버로 연결을 종료하겠다는 플래그인 FIN flag를 던진 뒤, FIN Wait상태로 변경된다.
    
### 2. Client( FIN WAIT ) <----- ACK ------ Server
     FIN Flag를 받은 서버는 응답 패킷인 ACK를 보낸 뒤, Close wait 상태가 된다.
     
### 3. Client( FIN WAIT ) <----- FIN ------ Server( CLOSE WAIT )
    서버가 통신이 끝나면(연결을 종료할 준비가 되면) 클라이언트에게 FIN 패킷을 보낸 뒤, Last Wait 상태가 된다.
    
### 4. Client             ------ ACK -----> Server ( LAST WAIT )
    클라이언트는 서버로 응답패킷(ACK)을 보낸 뒤, TIME WAIT 상태가 된다.
    
### 4. Client( TIME WAIT )------ ACK -----> Server 
    서버로부터 FIN보다 ACK가 늦게 온다면 FIN을 받고 세션을 종료할 것이기에 ACK가 드롭되고 데이터가 유실이 된다.
    때문에 클라이언트는 FIN을 받고도 일정시간(기본 240초)동안 잉여패킷을 기다린다. (= TIME WAIT 상태)
    
### 6. Client( CLOSE WAIT)                  Server 
    TIME WAIT상태가 종료(세션 완료 + 연결 종료)되면 클라이언트는 CLOSE WAIT 상태가 된다.
    
# Additional...
// 이와 함께 언급되는 개념으론 TCP연결 초기화에 사용되는 3 Way Handshake가 있다.
