# 2026 관통PJT - 웹기술(WebRTC)

## 기술 이론 정리

### WebRTC
: P2P(Peer to Peer) 방식으로 동작하며, 서버 없이 브라우저끼리 직접 연결된다.
- `getUserMedia()`: 카메라/마이크 접근
- `RTCPeerConnection`: 영상/음성 스트리밍 연결
- `RTCDataChannel`: 텍스트나 파일 같은 데이터 전송

```
navigator.mediaDevices.getUserMedia({ video: true, audio: true})
  .then(stream=>{
    // LiveKit room에 스트림 추가
    console.log('카메라/마이크 연결!')
  })
```

### LiveKit
: WebRTC 기반 오픈소스 플랫폼으로, 실시간 영상/음성 통화와 데이터 교환을 쉽게 구현할 수 있게 해주는 도구. WebRTC의 복잡한 부분(서버 설정, 연결 관리)를 대신 처리해준다.
- SFU 서버: 여러 사용자가 참여할 때 영상/오디오를 효율적으로 중계
- 클라이언트 SDK: 브라우저(Vue.js)나 서버(Django)에서 쉽게 연결

[예시]
- Web Speech API로 음성 -> 텍스트로 변환 후, LiveKit Data Channel로 상담원 측 store(Pinia)에 실시간 전달.
- 고객 음성 인식 결과 -> `publishData()` -> 상담원 `on('dataReceived')` -> store 저장

```
// Vue.js에서 간단히 연결
import { connect } from '@livekit/client';
const foom = await connect(url, token)
room.on('connected', () => console.log('통화 시작'))
```

### LiveKit Data Panel
: WebRTC 연결 위에서 `비디오/오디오` 외의 데이터(텍스트, json)를 실시간으로 주고 받는 통로.

`LiveKit의 데이터 패널을 통해 상담원 측에 store로 데이터를 전달한다`: 실시간 통화 중 발생한 데이터를 '상담원 화면'으로 바로 보내 저장소에 넣는 과정.

[전달 -> Store 과정]
- LiveKit 룸에서 발생: 클라이언트가 `localParticipant.publishData(data,'kind')로 데이터 전송
- 상담원 측 수신: 상담원 PC의 Livekit 클라이언트가 `room.on('dataReceived', callback)`으로 받음
- Store에 저장: 받은 데이터를 Vue.js Pinia나 Redux 같은 store에 넣는다.

```
room.on('dataReceived', (payload, participant)=>{
  const chatData = JSON.parse(payload)
  store.commit('addChat', chatData)
  console.log('고객 말:', chatData.text')
})
```
=> 상담원이 실시간 채팅창에서 보고, 나중에 DB에 저장 가능.



### Web Speech API(STT)
: 웹 브라우저에서 음성 기능을 쉽게 추가할 수 있는 JavaScript API.
- 음성인식(SpeechRecognition): 마이크로 들은 말을 텍스트로 바꾼다.
- 음성합성(SpeechSynthesis): 텍스트를 소리로 읽는다.

[사용법]
Chrome: `webkitSpeechRecognition` 혹은 `speechSynthesis` 객체 사용.

```
// 음성 인식 예시
if ('webkitSpeechRecognition' in window) {
  const recognition = new webkitSpeechRecognition();
  recognition.onresult = function(event) {
    console.log(event.results[0][0].transcript)
  }
  recognition.start();
}
```