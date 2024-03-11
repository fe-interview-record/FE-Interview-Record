# CDN 이란?

CDN(콘텐츠 전송 네트워크)은 Content Delievery Network 약자로 지리적 제약 없이 전세계 사용자에게 빠르고 안전하게 컨텐츠를 전송 하는 기술입니다. CDN을 사용하면 HTML 페이지, 스타일시트, JavaScript등 콘텐츠를 로드하는데 필요한 자산을 빠르게 전송할 수 있습니다.

## CDN 장점

1. 웹사이트 로드 시간 개선 <br/>
   사용자와 가장 가까운 CDN서버에서 콘텐츠를 제공하므로 웹사이트 로드시간이 빨라지게 됩니다.
2. 대역폭 비용 절감 <br/>
   웹사이트 호스팅용 대역폭 소비비용은 웹사이트를 운영할때 발생하는 대표적인 비용입니다. CDN은 캐싱을 통해 원본 서버가 제공해야 하는 데이터양을 감소 시키므로 웹사이트 소유자의 호스팅 비용을 줄일 수 있습니다.
3. 콘텐츠의 가용성 및 이중화 <br/>
   대규모 트래픽이나 네트워크 장애로 웹사이트가 멈출 수 있는데 CDN은 분산되어 있기 때문에 더 많은 트래픽을 처리할 수 있고 하드웨어 장애를 견딜 수 있습니다.

## AWS의 CDN서비스인 CloudFront

<img src="https://github.com/chldmswnl/chldmswnl/assets/63483751/18c5e86f-af4c-4f38-bab2-8059077a8381" alt="aws cloudfront"/>

AWS의 CloudFront서비스를 이용하면 손쉽게 CDN서비스를 구축할 수 있습니다. AWS는 전세계에 300개 이상의 Edge locations를 구축했습니다. <b>Edge locations</b>는 CloudFront 서비스가 콘텐츠를 캐싱하고 Client에게 제공하는 지점 혹은 캐시 서버를 의미합니다. 그리고 <b>Reginal edge caches</b>라는 서버가 또 있는데 오리진과 Edge locations 사이에 위치해 있습니다. 상대적으로 덜 인기 있는 컨텐츠들의 캐싱이 남아있고 Edge locations보다 캐시 스토리지 용량이 더 큽니다. 이 REC덕분에 CloudFront가 오리진에 요청하는것을 줄여줍니다.

콘텐츠는 TTL(Time To Live)값 동안 Edge locations에 캐싱되어 낮은 지연시간으로 콘텐츠를 요청할 수 있습니다.

### 요청 순서

1. 유저가 웹사이트나 애플리케이션에 접속해 정적 콘텐츠를 요청합니다.
2. DNS가 요청을 제일 가까운 Edge location으로 라우팅합니다.
3. Edge locations에 캐싱이 되어 있는지 확인하고, 캐싱이 되어있으면 유저에게 리턴합니다.
4. 캐싱이 되어 있지 않으면 오리진 서버에 컨텐츠를 요청하고 오리진 서버는 컨텐츠들을 edge location으로 보냅니다. 오리진으로부터 첫번째 바이트들이 도착하면 바로 유저에게 컨텐츠를 전달하고 edge location에 컨텐츠를 캐싱합니다.

[참고: How CloudFront delivers content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowCloudFrontWorks.html)
