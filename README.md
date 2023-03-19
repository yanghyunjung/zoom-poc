# zoom-poc 및 개발

* 기능 구현 리스트   
``` 
비디오 on/off
오디오 on/off
화면공유 on/off
비밀번호 설정 -> 개발 논의중
```

발급 받은 SDK_KEY, SDK_SECRET를 입력      

1. start & join   
클라이언트쪽에서 토큰 생성이 필요함. 생성 방법은 zoom 문서를 찾아보면 아주 잘 나와있으므로 참고바람   
https://marketplace.zoom.us/docs/sdk/video/web/essential/create-join-session/#start-session


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
- 둘 다 비디오, 캔버스 요소를 사용하여 비디오를 그려야 한다        
- 문서에서 강조하는 게 있다면 remote user(상대방)에 대한 비디오를 그릴 땐 x,y 좌표값을 계산해서 입력해주어야 한다. 하지만 안넣어도 잘 표시되길래 0으로 적용해놓았다.. 나중에 문제가 생길시 변경하는 걸루...     

3. share screen 화면공유 시작    
* 비디오를 그릴때와 비슷한 방법으로 구현함 -> 내가 보는 화면에서는 video element를 사용해도 되지만 상대방을 보는 화면에서는 canvas element를 써줘야한다.   
