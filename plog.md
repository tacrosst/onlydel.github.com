---
layout: page
title: Programming log
permalink: /plog/
---

### Dec 24, 2015
* javascript가 더이상 웹 전용이 아니라는 사실을 확인시켜주는 자료들.
    - [node-webkit(nw.js) samples](https://github.com/nwjs/nw.js/wiki/List-of-apps-and-companies-using-nw.js)
* 나를 미치게 만들었던 게임, 심시티. 그를 능가하는 게임([시티바운스](http://cityboundsim.com))을 만들고 있는 또 한 사람([Anselm Eickhoff](http://aeplay.co))
* AWS에서 몇 백원씩 과금 되던 놈, 원인을 찾았다. 예전에 node를 설치한 AMI 이미지를 저장해 놓고 있었는데 snapshot을 저장하는 elastics block storage는 free tier에 해당사항이 없기 때문이었던것 같다. 이런 detail한 과금 체계는 장점인가? 단점인가?


### Dec 22, 2015
* ES6에서 mixins 지원하지 않는 다고 한다. 더 쉬운 방법으로 비슷한 기능을 제공한다고 하니 그때까진 어쩔 수 없겠구먼.

### Dec 11, 2015
* React 책을 하나 구입했다. 번역된 eBook이다. 일주일 목표로 읽어본다. 알고있는 내용은 스킵하고 이틀동안 러프하게 한 번 읽으면서 간단한것만 실습하고 , 3일간 다시 한번 보면서 나머지 실습한다.
* 

### Dec 1, 2015
* 나프다콘(10/31)이후 AWS에 계정을 만들고 이것저것 테스트를 진행 중이다. 물론 우리회사같은 구멍가게에서 클라우드는 언감생심(焉敢生心)이나 미래를 위한 준비라 생각하고 연구하고 있다. 게다가 1년간 제공되는 무료사용 서비스가 있고(물론 조금만 실수하면 과금이 되기도 하지만...) 2016년초에 한국내 리전(Region)을 개설한다는 소식때문에 약간 들떠 있는 분위기도 있다. 그렇지만, 회사내에 적용하려고 할때 동료들의 이유없는 반항에 대해 궂이 도입이유를 납득시켜야 하는 번거로움과 수고를 (또) 해야한다는 생각에 미리 지치기도 한다.

### Nov 23, 2015
* Javascript는 알면 알수록 어려운 언어인것 같다. 게다가 찾으면 찾을 수록 넘쳐나는 관련 기술들은 단숨에 확인하고 정리하기엔 너무도 광범위하다. 차근 차근 연구할 필요를 다시한번 느낀다.

### Nov 17, 2015
* ASP.NET 5에는 [common DI(Dependency Injection) 인터페이스](https://github.com/aspnet/DependencyInjection)가 만들어져 있고, 추가 라이브러리도 있는데, 
    - [https://github.com/structuremap/도.dnx](https://github.com/structuremap/structuremap.dnx)
    - [http://autofac.org/](http://autofac.org/) - 공장모양 로고가 깬다.
* 토비의 스프링 3.1 에서 IoC와 DI관련 내용을 다시 읽고 있다. DI에 대해 혼자 고민하고 삽질하면서 만든 구조 덕분인지 처음 보다 훨씬 이해하기 쉬웠다. 이해하기 쉽다기 보다는 몸에 와 닫는다는 표현이 적절하다. 책은 java로 구현하고 있지만 내용은 framework에 구애를 받지 않는다. 역시 읽어보고, 해보고, 다시 읽어보고, 다시 해보고... 의 방법으로 공부하는게 좋다. 개발도 마찬가지다. 만들고, 테스트하고, 수정하고, 다시 테스트 하고.. 의 과정으로...
* AMD기반 requery.js를 통해 동적으로 모듈을 로드할 때 

### Nov 16, 2015
* 3일동안 씨름하던 오류의 원인을 찾았다. 생각지도 못했던 곳에서 원인을 찾았고 이 문제를 해결하기 위해 많은 새로운 사실을 알게 되었다.
    - 아래 오류를 만났을때 처음엔 CORS설정에 문제가 있는 것으로 생각하고 Web API쪽 ICorsPolicyProvider를 상속받아 구현한 Attribute만 계속 쭈물딱 거리고 있었다. 구글링을 해도, StackOverfllow에서도 cors로 접근할때 어떤 문제가 있는건지 찾아다녔다.
        <pre>
        XMLHttpRequest cannot load http://winlocal:49238/api/licenses. 
        The 'Access-Control-Allow-Origin' <mark>header contains multiple values</mark> 'http://examples.onlydel.dev, http://examples.onlydel.dev', but only one is allowed. 
        Origin 'http://examples.onlydel.dev' is therefore not allowed access.</pre>
    - 알고 보니 지금 서버 사이드 구성은 ASP.NET Web API + Web Sites를 붙여서 서비스 하고 있는데, Site쪽과 Web API쪽 config에 모두 cors 설정을 해두어 Response header에 Origin정보가 두개씩 붙어서 나가게 되어 사실은 Request쪽 서버에서 이를 허용해 주지 않으면 오류가 발생하는 것이었다. 마킹된 부분을 좀더 세심하게 확인했어야 하는데, 오류메시지 하나하나에 세심하게 주의를 기울여야하는데 여전히 고쳐지지 않는다.
* 도움말이던, 메뉴얼이던, 책이던 한 번에 모든 내용을 이해하기는 어렵다. 처음볼때 이해해와 두번째 볼때 이해도가 다르다. 세번정도 보면 어느정도 이해가 되는것 같다.

### Nov 14, 2015
* XECON 2015에 참석 했다.
    - PHP는 알지도 못하면서, XE가 뭔지도 모르면서 AWS와 Git과 React.js에 대한 정보를 얻고자 다녀왔다.
    - 어떤 컨퍼런스나 밋업이 도움 안되는 경우는 없는것 같다. 새로운 경험과 동기부여를 위해서는 오프라인 참여가 꼭 필요하다.

### Nov 10, 2015
* npm 을 통해 github에 있는 application 들을 실행 하는 방법에 대해 알게 되었다.
    - package.js파일에 dependency들은 $ npm install로 일괄 설치가 가능하다.
    - gulp나 grunt로 빌드 및 실행까지 일괄로 처리가 가능하다.
* AWS에서 elastic beanstalk 서비스를 통해 웹 서비스 배포 관련 방법을 알게 되었다.
    - 이재홍님의 블로그에서 도움을 받았다. [http://pyrasis.com/aws.html](http://pyrasis.com/aws.html)
    - [http://testbed.elasticbeanstalk.com](http://testbed.elasticbeanstalk.com) (무료사용계정 시간조정을 위해 접속안될 수 있음.)

### May 20, 2015
* 슬랙과 깃헙을 전사적으로 활용하기 위해 아이디를 만들것을 동료들에게 제안했다. 이유없는 반발들이 돌아왔다. 회의적이다. 이 일이 정말 그렇게 귀찮은 일인가? 일을 위한 일을 만드는 것인가? 허탈하고 의지가 박탈된 기분이다. 슬랙과 깃헙에 혼자서 두개의 아이디를 만들어 이것 저것 연구했던 한달이란 시간이 이렇게 허무하게 느껴지다니... 나는 도대체 무엇 때문에 이런 짓을 하고 있는 것인가? 그냥 아무것도 안하고 회사의 프로세스가 어디로 흘러가건 상관없이 지켜보고 같이 표류하는게 옳은 일인가? 지친다.

### Apr 25
* 깃헙에 2013년 12월 18일 처음 아이디를 만들었었다. 사실 그 당시에 깃헙은 그냥 버전관리 저장소 정도로 생각했다. 더구나, 우리 회사는 이미 SVN을 사내서버에 구축해 사용하고 있었기 때문에 별다른 필요성을 느끼지 못했고, 깃헙에 대한 연구는 흐지부지 해졌다. 1년이 훌쩍 넘은 지금, 개인 블로그를 만들기 위해 여러가지 방법을 찾던 중 우연히 jekyll에 대해 알게 되었고, 깃헙을 기반으로 웹사이트를 구축 할 수 있다는 사실에 무작정 jekyll과 깃헙에 대한 공부를 시작하게 되었다. 이틀 만에 RealGrid의 document를 이곳에서 서비스하면 좋겠다는 생각을 하게 되었고 바로 준비작업에 들어갔다. 생각보다 쉬운 방법과 다양한 서비스의 연계를 경험하며 좀더 넓은 세계에 발을 들여놓은것 같다는 생각이 든다.