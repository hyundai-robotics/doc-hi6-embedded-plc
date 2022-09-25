# 1. Overview

Hi6 제어기의 내장PLC(Embedded PLC)는 PLC(Programmable Logic Controller)의 기능을 제어기 내부에 소프트웨어적으로 탑재한 것입니다. PLC에서 흔히 사용되는 래더(ladder) 프로그램을 사용자가 작성하여 구동시킬 수 있습니다.

래더(ladder) 프로그램은 현대로봇 전용의 래더 편집 PC 소프트웨어인 HRLadder로 작성/편집하여, 이더넷으로 연결된 Hi6제어기에 다운로드할 수 있습니다. 반대로 Hi6 제어기에서 실행되고 있는 래더 프로그램을 PC의 HRLadder로 업로드 할 수 있으며, 제어기에서 실행되고 있는 PLC 모드나 릴레이 값 등의 상태를 HRLadder에서 원격 모니터링 하는 것도 가능합니다.

* HRLadder는 현대로보틱스 웹사이트(https://www.hyundai-robotics.com) - 고객지원 - 응용소프트웨어 화면에서 다운로드 받으실 수 있습니다.
* HRLadder의 사용법은 HRLadder의 도움말 메뉴에 연결된 기능설명서를 참조하십시오.
* HRLadder는 Hi4~Hi5a의 구모델 제어기용으로도 사용 가능합니다. 다만 래더 프로그램은 Hi6와 구모델 간 차이가 있어 호환되지 않음을 유의하십시오.

Hi6제어기의 I/O는 필드버스나 리모트I/O 장치를 통해 필드버스 마스터를 가진 상위 공정PLC, 혹은 하위 필드버스 슬레이브 장치들과 연결할 수 있습니다. 내장PLC 기능은 이렇게 연결된 I/O 신호들을 Ladder Logic으로 제어하는 기능입니다.
