<읽어주세요!!!^^>

소스공개에 대해 한말씀 드리겠습니다. ^^;;
허접한 소스지만, 퍼가셔서 공부는 하셔도 좋습니다.
이런 류의 프로그램을 만들때 도움이 되시라고 공개한 거니까요.^^; 
하지만 소스의 참고가 아닌, 소스를 일부만 수정해서
자신이 만든 것처럼 하신다면, 그건 훔친게 됩니다. ^^;;
그냥 참고만 해 주세요. ^^;;
거듭 말씀드리지만, 소스 공개는 저작권 포기가 아닙니다. ^^;;
제 소스를 막 훔쳐가시면 전 슬픕니다.. ㅜ.ㅠ 그냥 공부에만 써 주세요. ^^;

어쨌든 저는 여러분을 믿습니다.
그렇기에 소스를 공개했지요. ^^; 

--

EasyBBS Builder

구현 설명서


	I. BBS 구현





1. BBS 전반

   MAIN WINDOW --- SOCKET MESSAGE WINDOW <-- Request
                     |                          ^ 
                     V                output    |
              +- USER THREAD -------------------+
              +- USER THREAD
              +- USER THREAD



   이상과 같이 평상시엔 소켓 메시지를 받는 윈도우에서 메시지를 받아 해당하는 사용자 쓰레드를 활성화시켜주는 구조입니다.  사용자 한명당 하나의 쓰레드가 할당됩니다.

  Mainunit.pas : 메인 폼의 데이터와 데이터 로딩등을 관리합니다.
  Client.pas   : 기본적인 사용자 처리를 모두 담당합니다.
  Socket.pas   : 소켓 메세지를 받아 client.pas를 동작시켜줍니다. 
  Log.pas      : 로그기록 저장을 관리합니다.
  Envior.pas   : 환경설정을 관리합니다.
  Sockset.pas  : 소켓관련 설정을 관리합니다.
  

2. USER THREAD

           SUBROUTINE EXECUTER   <-------+
                  |                      |
       +------+---+--+-------+           |
       |      |      |       |           |
     BOARD  CHAT   READMAIL SENDMAIL     |
       |      |      |       |           |
       +------+------+-------+-----------+

 이상과 같이 해당하는 메뉴의 작업이 끝난 후 일정한 분기루틴으로 되돌아오게 설계되었습니다.

3. 다른 쓰레드와의 통신

  다른 쓰레드의 변수를 직접 건드리지 않고 그 쓰레드의 RECEIVER를 호출하여 메시지를 전달합니다.

4. 메뉴 구조
   메뉴는 그 구조대로 디렉토리의 형태로 저장됩니다.
   MENU\1\1\1         (1은 선택번호) 식입니다.

   ---+--+--  1    MENU\1\1\1
      |  +--  2    MENU\1\1\2
      +-----  3    MENU\1\1\3

  그리고 각 메뉴에는 MENU.DAT파일이 존재합니다. 그 디렉토리에 해당하는 메뉴의 종류, 특징 등을 기록합니다.


5. 게시물 파일의 구조
     +-----+
     |1.TXT|
     |-----+-------------------------+
     |HEADER                         |
     +-------------------------------+
     |본문                           |
     +-------------------------------+

6. HTTP구현
   현재 GET/POST명령(POST는 내부적으로)만을 지원합니다.



 
                                     
	II. BBS 인터페이스                
                                     
                                     
                                     
1. 접속시 인터페이스                 

   접속시의 기본 인터페이스는 나우누리의 그것을 따릅니다.


2. BBS프로그램의 인터페이스

   기본적인 모양은 다음과 같습니다.

   +-----------------------------+
   | 메뉴                        |
   +-----------------------------+
   | 아이콘                      |
   +-----------------------------+
   | 사용자 리스트               |
   |                             |
   |                             |
   +-----------------------------+

   현재 접속한 사용자에게 쪽지를 보내거나/ 접속을 끊을 수 있게 하였습니다.


3. 메뉴에디터 인터페이스

  +-----------------------------+
  | 메뉴                        |
  +-----------------------------+
  | 트리뷰                      |
  |                             |
  |                             |
  |                             |
  +-----------------------------+
  | 노드정보                    |
  +-----------------------------+

  트리뷰에 전체적인 BBS메뉴 구조를 표시하게 하였습니다.  그리고 현재 위치한 노드의 정보를 쉽게 알 수 있도록 정보를 즉시 표시해 줍니다.

4. 유저에디터 인터페이스
  
  +------------------------------+
  | 종료버튼                     |
  +------------------------------+
  | 아이콘                       |
  +------------------------------+
  | 사용자 리스트                |
  |                              |
  |                              |
  +------------------------------+

  사용자를 쉽게 선택하여 고칠 수 있게 하기 위해 아이디순으로 사용자 리스트를
정렬합니다. 별다른 점은 없습니다.





- 개인정보 -
이름	: 이청희(남자입니다-.-;)
나이    : 팔팔한..고3-_-;;
연락처	: 011-9981-0213 / innoboy@kornet.net / innoboy@nownuri.net
-
