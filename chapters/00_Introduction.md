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
이 문서의 핵심은 독자들에게 Infer.NET 을 안내하는 것입니다. 여러분은 점차 복잡해지는 일련의 Infer.NET 애플리케이션(applications) 코드 예제를 접하게 될것입니다. 예제들은 애플리케이션 이 어떻게 Infer.NET 의 핵심 기능들 사용하는지 보여주며 또한 그와 연관된 개념적, 수학적 토대들도 다룰것입니다.
<br>
<br>

**시나리오** 문서에서 다루는 모든 애플리케이션은 다음의 시나리오에 기반하고 있습니다.

- 당신과 여러 동료들은 매일 자전거로 출근을 합니다.
- 개개인이 매일 자전거로 이동하는데 걸리는 시간은 날마다 다르며 불확실 합니다.
- 이동시간의 불확실성은 확률분포로 표현될수 있습니다. 확률분포는 이동시간의 평균(average)과 평균이 매일 얼마나 다른지에 의해 정의됩니다.
- 애플리케이션은 여러날 동안의 이동시간 관찰을 통해서 확률분포를 학습한후, 습득된 지식을 이용해서 미래의 이동시간을 예측할것 입니다.

**예제** 예제를 통해 다음과 같은 애플리케이션을 다룹니다.

- CyclingTime1 은 한명의 싸이클리스트(cyclist) 이동시간 확률분포를 학습하며, 그 정보를 바탕으로 미래의 이동시간을 예측합니다.
- CyclingTime2 은 CyclingTime1 의 재구성 버전입니다. 모델 구현을 위한 표준이되는 기법들을 소개하며, 이 방법은 이후에 나오는 예제 애플리케이션에 적용됩니다.
- CyclingTime3 은 예상치 못한 사건이 발생할 경우를 다루며, 이를 위해 두개의 확률 분포를 혼합하여 이동시간 모델을 만듭니다.
- CyclingTime4 은 증거(evidence)를 사용해서 가장 적합한 모델을 선택하는 방법을 보여줍니다. 
- CyclingTime5 에서는 두 번째 싸이클리스트가 추가되며 더 복잡한 모델을 구성하는 방법을 보여줍니다.

**예제 코드** 모든 예제 코드는 Microsoft Visual Studio®를 이용한 solution인 InferNET101 에 포합되어 있으며, Infer.NET 소스 코드의 예제 폴더에서 찾을수 있습니다. InferNET101 solution 에 포합된 파일은 다음과 같습니다.

- InferNet101.cs <br>
간단한 콜손 애플리케이션 이며 5개의 예제를 순서대로 실행합니다.
- RunCyclingSamples.cs <br>
RunCyclingTime1 ~ RunCyclingTime5 로 이름지어진 5개의 static method 들로 구성되어 있으며 각각의 method는 그에 상응하는 예제를 실행시킵니다. 이는 모델을 만들고 트레이닝, 예측하는 등의 과정을 포함합니다. 
- CyclingTime2 ~ CyclingTime5 <br>
CyclingTime1 의 Infer.NET 모델은 RunCyclingSamples.cs 에 구현되어 있습니다. 나머지 4개의 예제에서는 개별적인 클라스 CyclingTime2.cs ~ CyclingTime5.cs 파일에 모델이 구현되었습니다. 

<br>

Infer.NET 애플리케이션의 빌드와 실행에 관한 일반적인 설명은 Appendix C를 참조하십시오.
<br>
<br>

**요구조건** 이 문서는 독자가 확률론적 프로그래밍(probabilistic programming) 의 기본 개념과 용어에 익숙하다는 전제를 바탕으로 합니다. 이 문서의 참고자료 목록에 있는 Infer.NET 안내 (An Introduction to Infer.NET) 를 참조하기 바랍니다.<br>
다음 조건들도 또한 최소한의 요구 조건들입니다.
- 기본적인 C# 프로그래밍 지식<br>
이것은 특별히 필요하며 그렇지 않으면 기존의 보통 C# 코드와 Infer.NET 코드를 구별하는데 어려움이 있을것입니다.
- C# 과 Microsoft Visual Studio 를 이용하여 Microsoft .NET Framework 애플리케이션을 만드는데 익숙함.
- 기본적인 통계 지식<br>
베이지안 추론 (Bayesian inference) 을 알고 있다면 도움이 되지만 필수적인 것은 아님.

<br>

**용어** Infer.NET 과 이 문서에 사용된 용어 정의는 Appendix A 를 참조하십시오.
<br>
<br>

**설치** 시스템 요구사항과 설치에 관한 지시는 Appendix B 를 참조하십시오.


<br>
<br>
<br>
<br>

## Infer.NET 기초
---

첫번째 애플리케이션 예제를 시작하기 전에 이 장에서는 CyclingTime1 ~ CyclingTime5 예제의 기본 구조와 중요한 요소들 간단하게 살펴볼것 입니다. 용어와 개념들은 이후에 더 자세히 다루도록 하겠습니다.
<br>
<br>

## **모델 만들기**
<br>
Infer.NET 애플리케이션은 확률론적 모델(probabilistic model)을 중심으로 구축되었습니다. 확률론적 모델은 확률변수들(random variables)과 이들이 관계되는 방식을 정의합니다.  
<br>
<br>

확률변수(random variable)는 본질적으로 **double** 또는 **int** 같은 표준 타입에서 확장된 것이며, 불확실한 값(uncertain values)을 가질 수 있습니다. Infer.NET 에서 확률변수는 **Variable\<T\>** 클래스(class)의 인스턴스(instance)로 표현되며 이 클래스는 **Microsoft.ML.Probabilistic.Models** 네임스페이스(namespace) 에 속해 있습니다. 여기에서 **T** 는 변수(variable)의 도메인 타입(domain type) 을 나타냅니다.<br>

- 이산확률변수(Discrete random variables) 는 **bool** 또는 **int** 와 같은 도메인 타입처럼 정해진 특정 값들의 가능한 집합에서 그 값을 취할 수 있습니다.
- 연속확률변수(Continuous random variables) 는 **double** 같은 도메인 타입처럼 가능한 값들의 범위를 그 값으로 취할수 있습니다.<br>

확률변수는 *확률분포 (probability distribution)* 로 정의되며 확률분포에서의 확률을 변수의 가능한 값으로 할당합니다. (probability distribution 은 일반적으로 *distribution* 으로 약칭됩니다). 확률변수의 값이 관측되기 이전에는 변수 값에 대한 이해를 나타내는 *사전분포 (prior distribution)* 로 확률변수를 정의합니다. (prior distribution 은 일반적으로 *prior*로 약칭됩니다).

<br>

|             |
| ----------- | 
| <br > 확률변수는 최대 세 단계를 거쳐서 만들어질 수 있습니다. 예를 들면: <br ><br > 1. C# 선언(declaration): Variable\<bool\> x;<br><br >2. C# 정의(definition): x = Variable\<bool\>.New();<br><br >3. 통계적 또는 모델 정의: x = Variable\<bool\>.Random(someDist);<br ><br >통계적 추론의 언어에서 "정의(definition)" 또는 "정의한다(define)" 는 용어는 변수의 분포를 가르킬때 사용되며 이 문서도 이 방식을 따릅니다. 하지만 2단계와 3단계가 만약 별도의 명령문(statements)인 경우, 3단계에 대해 "통계적 정의" 또는 "통계적으로 정의한다"라는 표현을 사용하여 구분을 명확히 합니다.<br><br> 
|             | 

<br>
확률변수들 사이의 관계는 다양한 방식으로 정의될 수 있으며, 이 문서 후반부에서 다루도록 하겠습니다. 
<br>
<br>

## **확률변수 관측**
<br>

이 시점에서 모델을 통해 계산을 수행할 수 있지만 대부분 그렇게 흥미롭지는 않으며 단순히 선택한 사전분포(priors) 값들이 계산 결과로 반영됩니다. 무엇인가 새로운 것을 학습하기 위해서는 모델에 있는 한개 이상의 확률변수를 관측해야 하며, 이것은 확률변수의 **ObservedValue** property 에 관측 값들을 할당(assign)함으로써 이루어집니다. 관측이 된 후에 변수는 더 이상 확률변수가 아니며, 사실상 고정된 값을 가진 표준 타입(standard types)이 됩니다. 
<br>
<br>

## **사후분포(Posteriors) 추론**
<br>

관측이 되기 전에는 사전분포(prior)가 모델의 특정 확률변수의 분포를 직접 또는 간접적으로 정의합니다. 한 개 이상의 변수가 관측되면 그 변수에 대해 더 많은 정보를 얻게되며 그 변수는 *사후분포* (posterior distribution) 라는 새로운 분포를 가지게 됩니다 (posterior distribution 은 *posterior* 로 약칭됩니다). 사후분포는 기존의 사전분포에 관측결과에서 얻은 정보를 통합한 결과이며 이것은 변수 값에 대한 지식이 새롭게 향상된 것을 보여줍니다.
<br>
<br>

사후분포의 계산에는 Infer.NET 추론 엔진 (inference engine) 을 사용합니다. 추론 엔진은 모든 복잡한 수학적 계산작업을 담당하며 **Microsoft.ML.Probabilistic.Models** 네임스페이스에서 **InferenceEngine** 클래스로 구현되어 있습니다.
<br>
<br>

추론엔진은 모델에서 다른 확률변수들이 받은 영향을 합산(summing out)하여 특정 확률변수의 사후분포를 계산합니다. 일반적으로 이런 유형의 분포를 *한계분포* (marginal distribution)라고 합니다 (marginal distribution 은 *marginal* 로 약칭됩니다). 특정 확률변수의 사후분포는 모델에서 한 개 이상의 다른 확률변수를 관측한 후 추론엔진이 계산한 한계분포를 통해 얻을수 있습니다. 이 한계분포는 이제 그 특정 확률변수의 사후분포이며, 다른 변수들의 관측을 통해 얻은 새로운 정보에 따라 이 특정 변수의 사전분포가 업데이트 된것을 의미합니다. 한계분포, 사전분포 및 사후분포 에 대한 자세한 내용은 "Infer.NET 소개"를 참조하십시오.
<br>
<br>

## **사후분포(Posteriors)의 활용**
<br>
사후분포는 다목적으로 활용됩니다. 가장 두드러진 용도는 변수가 앞으로 어떤 방향으로 변화할지 예측하는 것입니다. 그러나 관측된 수가 충분하지 못하면 사후분포는 변수의 실제 변화를 정확하게 반영하지 못할 수 있으며 따라서 예측값 또한 정확하지 않을 수 있습니다. 다음과 같이 추가적인 관측을 수행하고, 관측 결과를 다시 변수들의 분포에 반영함으로써 사후분포에 대한 이해를 향상시킬 수 있습니다.

<br>
<br>
1. 얻어진 사후분포(posterior)를 변수의 새로운 사전분포(prior)로 사용합니다.
<br>
2. 추가적인 관측을 수행합니다.
<br>
3. 새로운 사후분포(posterior)를 다시 계산합니다.
<br>
<br>
새로 계산된 사후분포는 관측 전의 사전분포와 이후의 모든 관측값들이 통합된 결과입니다. 이러한 절차는 필요한 만큼 무한히 반복해서 수행하는 것이 가능합니다. 충분한 관측이 수행될수록 사후분포는 변수의 실제 값을 더 정확히 반영합니다. 

<br>
<br>
<br>
<br>

## 앞으로 다룰 내용은?
---
확률분포는 한개 이상의 모수(parameters)에 의해 결정됩니다. 때로는 모수의 적절한 사전분포를 추정할수 있지만 추정된 모수치가 후속 관측치와 정확히 일치하는 경우는 거의 없습니다. 또한 모수에 대한 사전 지식이 거의 없거나 전혀 없을 경우도 있습니다. 즉, 모수값은 불확실성을 지닙니다.

베이지안(Bayesian) 통계의 관점에서 볼때 모든 것은 - 확률분포의 모수를 포함해서 - 불확실하며 따라서 확률변수 처럼 다루어질 수 있습니다. 이제 변수에 할당하는 사전분포(prior)는 모수값에 대한 사전 지식(또는 지식의 부족)을 변수에 반영할 것이며, 이후의 관측과 확률론적 프로그래밍을 통해서 모수값의 확률분포에 대해 더 정확히 알게됩니다.