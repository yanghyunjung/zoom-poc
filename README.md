# zoom-poc

제일 먼저 SDK_KEY, SDK_SECRET 발급을 받는다.   
일단 서버 도움이 없이 오로지 클라이언트쪽에서만 처리를 하였다.   

1. start & join   
먼저 토큰을 만들어줘야함. 토큰 만드는 방법은 zoom 깃허브나 구글링을 해보면 아주 잘 나와있음   
발급받은 sdk 관련 키까지 넣으면 video sdk를 사용할 준비 완료!


2. video 그리기     
* local user 비디오 연결할 때
```  
 videoChatClient
    .getMediaStream()
    .startVideo({ videoElement }) // 파라미터 잘 넣기
    .then(() => {
      if (!(typeof (window as any).MediaStreamTrackProcessor === 'function')) {
        attachVideoChatCard(canvasElement, userId);
      }
    });
```    
* remote user 비디오 연결할 때   
```
 videoChatClient
    .getMediaStream()
    .renderVideo(canvasElement, userId, 0, 0, 0, 0, 2);
```    
- 둘 다 캔버스 요소를 사용하여 비디오를 그린다. 다른 점이 있다면 remote user에 대한 비디오를 그릴 땐 x,y 좌표값을 계산해서 입력해주어야 한다. 하지만 굳이 안넣어도 잘 나와서 0으로 적용해놓았다.. 나중에 문제가 생길시 변경하는 걸루...   
