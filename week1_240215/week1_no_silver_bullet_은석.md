![Alt text](https://bryanmmathers.com/wp-content/uploads/2015/05/no-silver-bullet.png)
    
## **하드웨어의 발전에 비해 소프트웨어의 발전은 더디다**
- [무어의 법칙](https://ko.wikipedia.org/wiki/%EB%AC%B4%EC%96%B4%EC%9D%98_%EB%B2%95%EC%B9%99): 하드웨어는 2년 마다 두 배씩 발전하고 있다. but 소프트웨어는 아님.
- 이미 소프트웨어도 발전시키려고 많은 과정을 거쳤다.
- 그러나 하드웨어 개발과 소프트웨어 개발에는 본질적 차이가 있음
<br>

## 소프트웨어가 복잡한 이유!
- **본질적 복잡성(essential complexity)**
    - == 필수적 복잡성
    - 비지니스 문제를 풀어내는 데서 발생하는 복잡성
        - “추상적인 소프트웨어 실체를 구성하는 복잡한 개념 구조”.
            ex. 은행 계좌 이체 처리, 잔고 확인
        - 즉, 도메인 개념과 그 관계, 행동 및 의사결정 논리 등 소프트웨어의 필수 측면을 포착하고 처리하는 것입니다.
<br>

- **우발적 복잡성(accidental complexity)**
    - 책에서도 이렇게 해석하는데, 부수적 복잡성으로도 볼 수 있을 듯.
    - 실제 작업을 진행하면서 생기는 복잡성
        - 개발 환경 설정, 배포 구성 관리
    - 우발적인 복잡성을 해결하는 데 도움을 준 해법들
        - 요걸 제거하는 작업은 많이 발전해왔음. (1986년 기준인 것에 유의)
            - 고급 언어 - 기계 용어로 생각하고 쓰는 것에서 해방되어 프로그램의 "신뢰성, 단순성 및 이해성"이 향상
            - 시분할 방식 - 프로그램 응답 시간의 단축
            - 프로그래밍 환경의 통합 - 사용자를 위한 도구들의 증가, lib, 파일 형식 등
            - 객체 지향, 인공 지능 등
            - but 이것들은 실제 기술 혁신이 아닌 점진적인 개선만 제공한다.
                - ex. oop는 마법이 아님.. 설계자체의 복잡성은 필수적, 불분명한 요구 사항 또는 팀 커뮤니케이션 문제 등
                
                > but 지금은 이러한 해법들 자체가 많이 발전했다고 보임..
                > 
## ***소프트웨어가 복잡하고 어려운 이유! ⇒ 결국 본질적으로 어렵기 때문. 왜? 4가지로 정의***
- 복잡성 - 도메인 개념과 그 관계, 행동 및 의사결정 논리 등의 본질적 소프트웨어, 즉 비지니스를 정의하는 것
    
    > 소프트웨어 개체의 본질은 데이터 세트, 데이터 항목 간 관계, 알고리즘, 함수 호출처럼 서로 맞물리는 개념으로 이루어진 구조물이다. 표현 방법은 여러 가지로 달리 하더라도 개념적 구조물은 동일하다는 점에서 이 본질은 추상적이다. 추상적이라 해도 그 구조물은 고도로 정밀하며 풍부한 세부 내용을 담고 있다.
    > 
    - 소프트웨어를 만드는 데 있어 정말 어려운 부분은 개념적 구조물의 명세, 설계, 테스트이다.
    - 소프트웨어를 확장할 때, 이는 비선형적으로 증가할 수 있다.
        - 소프트웨어 엔티티의 확장은 단순히 동일한 요소를 더 크게 반복하는게 아니라 서로 다른 요소가 증가하기 때문.
        - 수학과 물리학은 복잡한 현상의 단순화 된 모델을 구성하여 그 모델에서 속성을 도출하고 실험을 통해 이러한 속성을 검증함으로써 큰 발전을 이룸. 그러나 이 패러다임은 복잡성이 본질 일 때는 작동하지 않음.
- **호환성** - 인간이 만든 것이기 때문, 동일한 문제를 해결하더라도 사용자 마다 다르게 설계하는 인터페이스에 따른 복잡함이 생김. 재설계만으로 단순화되기 어려움.
- **변경 가능성 -** 소프트웨어는 본질상 지속적으로 변경됨 - 응용 분야, 사용자, 법률, 장비 등에 따라..
- **비가시성 -** 제어 흐름, 데이터 흐름, 종속성 패턴, 시간 순서, 네임스페이스 관계를 나타낼 수 있는 여러 그래프는 일반적으로 평면적이지도 않고 계층적이지도 않습니다”
    - 보이는 공간에 있지 않기 때문에 구조를 가시적으로 보이도록 할 수 없음. 이는 설계 과정과 의사소통을 어렵게함..
        - 오늘날에는 ui적으로 이를 표현할 수 있는 많은 도구들이 생김. apm, kibana 등

- `이에 대한  은탄환은 없다!` 즉, 압도적으로 소프트웨어 개발의 생산성을 늘리는 것은 어려운 일이다.
    - **silver bullet?**
        - 소프트웨어를 평범한 인간의 모습을 하고 있다가 공포스러운 괴물로 변신할 수 있는 늑대인간에 비유
        - 소프트웨어 제작비용을 급격히 떨어뜨려줄 수 있는 마법의 아이템
    
    > **소프트웨어가 통제할 수 없는 괴물로 변하는 것을 막을 수 있는 확실한 방법을 찾을 수 있을지 회의적이다.**
    > 
    - 저자가 제시하는 괜찮은 해법들은 다음과 같다.
        - 복잡성 자체를 겨냥하는 해법들 (점진적이고 진화적인 접근 방식에 가까움)
            - ***소프트웨어를 만들지 않고, 소프트웨어 제품을 구매한다 - 너무 러프함 but 확실한 해결***
            - ***요구 사항 상세화와 고속 프로토타이핑***
                - 무엇을 만들지 정확히 클라이언트와 결정하는 것.
                - 고객들도 자기가 무엇을 원하는지 모르며, 고민하지 않는다
                - 따라서 고객과 설계자는 꾸준히 소통해야 한다.
                - 반복적으로 신속하게 프로토타입을 만들 수 있는 방법 및 도구를 개발해야 한다.
                    - 스프레드 시트, 노션 같은 거..
            - ***점진적 개발***
                - tdd?
                - 하향식 설계 접근 방식.
                - 기본 기능을 갖춘 MVP로 시작해서 사용자 피드백 기반으로 성장시키기 → 개발자에게도 좋음.
            - ***탁월한 설계자 육성, 즉 좋은 디자인 설계가 필요함***
                - • 체계적인 방식으로 최고의 설계자를 빨리 찾아내고, 성장시켜야 한다.
                - 테스트를 진행시켜야 한다.
        
        ⇒ 결국 소프트웨어 본질적 문제들을 직시하고 빠르게 풀어낼 것에 집중하라는 뜻..

<br>
                
“회의주의는 비관주의가 아니다. 비록 놀라운 돌파구는 보이지 않고 실제로 그러한 것이 소프트웨어의 본질과 일치하지 않는다고 생각하지만, 많은 고무적인 혁신이 진행되고 있습니다. 이를 개발, 전파 및 활용하기 위한 규율 있고 일관된 노력은 실제로 엄청난 수준의 개선을 가져옵니다. 왕도는 없지만 길은 있다.” ⇒ 꾸준히 해보라.

- 참고 : [NO SILVER BULLET- PDF](https://www.cgl.ucsf.edu/Outreach/pc204/NoSilverBullet.html), [이종립 블로그](https://johngrib.github.io/wiki/No-Silver-Bullet/)