## Infer.NET 입문

<br>
<br>

### 예제로 배우는 Microsoft Infer.NET programming

<br>
<br>
<br>
Version 1.2 – October 2018
<br>
<br>
<br>

**소개**

---
이 문서는 마이크로소프트 Infer.NET 을 이용하여 확률론적 프로그램(probabilistic programs)을 다양한 예제를 통해 자세히 소개하고 있습니다. 
확룔론적 프로그램과 Infer.NET 의 기본 개념을 살펴보려면 참고자료 목록에 있는 'Infer.NET 입문' (An Introduction to Infer.NET)을 참고하기 바랍니다.

**다룰 내용** 

---
입문<br>
**1장** CyclingTime1 Application: 기초적 모수 학습<br>
**2장** 보충설명: 가우시안(Gaussian) 분포와 감마(Gamma) 분포, 팩터 그래프(Factor Graphs)<br>
**3장** CyclingTime2 Application: CyclingTime1의 재구성<br>
**4장** 보충설명: 사전확률(Priors)<br>
**5장** CyclingTime3 Application: 혼합 모델 (Mixture Models)<br>
**6장** 보충설명: 이산분포(Discrete Distributions)와 Inference Engine<br>
**7장** CyclingTime4 Application: 모델 비교<br>
**8장** CyclingTime5 Application: 2인 싸이클리스트 모델<br>
**9장** 보충설명: 확률변수 함수들 (Functions of Random Variables) <br>

**Note**
보내주실 피드백이 있으시면 [infersup@microsoft.com](mailto:infersup@microsoft.com) 로 이메일을 보내시기 바랍니다.

<br>
<br>
<br>
<br>
<br>
<br>

## 입문
<br>
<br>
이 문서는 마이크로소프트 Infer.NET을 이용하여 확률론적 프로그램(probabilistic programs)을 다양한 예제를 통해 자세히 소개하고 있습니다. 
만약 확률론적 프로그램이 생소하다면 참고자료 목록에 있는 'Infer.NET 입문' (An Introduction to Infer.NET)을 먼저 읽어보기를 권합니다. 'Infer.NET 입문' 은 확룔론적 프로그램과 Infer.NET 의 기본 개념을 다루고 있습니다.
<br>
이 문서의 핵심은 독자들에게 Infer.NET 을 안내하는 것입니다. 여러분은 점차 복잡해지는 일련의 Infer.NET applications 코드 예제를 접하게 될것입니다. 예제들은 application 이 어떻게 Infer.NET 의 핵심 기능들 사용하는지 보여주며 또한 그와 연관된 개념적, 수학적 토대들도 다룰것입니다.
<br>
<br>
**예제 시나리오** 문서에서 다루는 모든 application 들은 다음의 시나리오에 기반하고 있습니다.

- 당신과 여러 동료들은 매일 자전거로 출근을 합니다.
- 개개인이 매일 자전거로 이동하는 시간은 날마다 다르며 불확실 합니다.
- 이동시간의 불확실성은 확률분포로 표현될수 있습니다. 확률분포는 이동시간의 평균(average)과 평균이 얼마나 다른지에 의해 정의됩니다.
- application 은 여러번의 이동시간 관찰을 통해서 확률분포를 학습한후, 습득된 지식을 통해서 미래의 이동시간을 예측할것 입니다.