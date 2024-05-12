### Visual Studio 2022 사용
<br>  
  
  
## 구현 단계
1. 단계. 가장 간단한 IOCP 서버. Echo 서버 코드 만들기  
    - IOCP API 동작에 대해서 이해할 수 있다.
2. 단계. OverlappedEx 구조체에 있는 `char m_szBuf[ MAX_SOCKBUF ]`를 stClientInfo 구조체로 이동 및 코드 분리하기
    - 앞 단계에는 OverlappedEx 구조체에 `m_szBuf`가 있어서 불 필요한 메모리 낭비가 발생함
3. 단계. 애플리케이션과 네트워크 코드 분리하기  
    - IOCP를 네트워크 라이브러리화 하기 위해 네트워크와 서버 로직 코드를 분리한다.
    - 연결, 끊어짐, 데이터 받음을 애플리케이션에 전달하기  
4. 단계. 네트워크와 로직(패킷 or 요청) 처리 각각의 스레드로 분리하기  
    - Send를 Recv와 다른 스레드에서 하기  
    - send를 연속으로 보낼 수 있는 구조가 되어야 한다.  
5. 단계. 1-Send 구현하기  
    - 버퍼에 쌓아 놓고, send 스레드에서 보내기.   
6. 단계. 1-Send 구현하기  
    - queue에 담아 놓고 순차적으로 보내기.    
7. 단계. 비동기 Accept 사용하기
    - 6단계까지는 Accept 처리를 동기 I/O로 했다. 이것을 비동기I/O로 바꾼다. 이로써 네트워크 동작이 모두 비동기 I/O가 된다
8. 단계. 채팅 서버 만들기
    - 패킷 구조 사용하기, 로그인
9. 단계. 로그인 때 Redis 사용하기       
    - C++에서 Redis를 사용하는 방법은 아래 링크들 참고.
        - http://redis.io/clients#c–
        - https://github.com/redis/hiredis
10. 단계. 방 입장, 방 나가기, 방 채팅 구현하기        
      
  
  
## 참고 글 모음
- [IOCP 기본 구조 이해](https://www.slideshare.net/namhyeonuk90/iocp )
- [IOCP에 대하여](https://www.joinc.co.kr/w/Site/win_network_prog/doc/iocp )
- [IOCP (I/O CompletionPort)](https://chfhrqnfrhc.tistory.com/entry/IOCP )
- [IOCP 정리](https://hmjo.tistory.com/159 )
- [IOCP](https://blog.naver.com/zzangrho/80150515226 )
- [IOCP 모델](https://blog.naver.com/handodos/140138259592 )
- [IOCP 모델 - 구조의 이해](https://zxwnstn.blog.me/221513630216 )
- [서버 모델 - 윈도우 IOCP](https://dev-ahn.tistory.com/114 )
- [IOCP 내용 정리](https://blog.naver.com/dkdldhekznal/221233789231 )
- [게임 서버를 제작하기 위한 IOCP 네트워크 클래스 만들기 Ver1](https://blog.naver.com/dkdldhekznal/221235469866 )
- [게임 서버를 제작하기 위한 IOCP 네트워크 클래스 만들기 Ver2](https://blog.naver.com/dkdldhekznal/221242411793 )
  
