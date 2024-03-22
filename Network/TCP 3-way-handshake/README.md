## TCP 3-way-handshake (연결)

TCP 통신 과정에서 데이터를 전송하기 위해서는 먼저 ‘연결’ 상태를 확보해야 합니다. 이를 위해 3 way-handshake 과정이 필요합니다.

컴퓨터 A와 B가 있다고 가정하면,
첫 번째 단계로, 먼저 통신을 하기 위해서 A가 B에게 연결 요청을 합니다. 즉, A가 B에게 SYN 패킷을 보냅니다. 두 번째 단계로, 그럼 A의 연결 요청을 받은 B가 승인과 연결 요청으로 응답합니다. 즉, B가 A에게 ACK 패킷과 SYN 패킷을 보냅니다.
마지막으로, B의 요청을 받은 A가 연결 확립을 위해 승인을 응답합니다. 즉, A가 B에게 ACK 패킷을 보냅니다.  이와 같이 TCP는 연결을 확립하기 위해 패킷 요청을 세 번 교환하는 과정을 3 way-handshake라고 합니다.

<img width="1262" alt="image" src="https://github.com/BeMatthewsong/concepts_for_frontend/assets/98685266/e2418239-ae9d-4ba2-bccb-3e4e14638b8a">
