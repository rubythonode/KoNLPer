KoNLPer
================

How to use
----------

### docker

KoNLPer는 [reticulate](https://rstudio.github.io/reticulate/)와 [Flask](flask-docs-kr.readthedocs.io)를 이용해서 [KoNLP](https://cran.r-project.org/web/packages/KoNLP/vignettes/KoNLP-API.html)의 함수를 POST 요청으로 결과를 받을 수 있도록 구성된 API 서버입니다.
docker image는 [mrchypark/konlper](https://hub.docker.com/r/mrchypark/konlper/)로 바로 사용 가능합니다.

    docker run -p 80:5000 mrchypark/konlper

`ENV`로 사전의 범위를 설정할 수 있습니다. S는 세종사전, N은 NIA사전, W는 우리샘사전입니다. `ENV=S`인 경우 세종사전 추가, `ENV=N`인 경우 NIA사전 추가입니다. `ENV=SNW`는 전체 사전 추가입니다. (로 만들고 있는 중입니다.)

### api

현재 테스트 서버가 운영중이며 [google app engine](https://appengine.google.com/)에 올리고 [duckdns.org](https://www.duckdns.org/)로 주소를 확보했습니다.

아래 쉘 명령으로 동작 가능한 함수의 리스트를 받을 수 있습니다.

    curl -X GET "http://konlper.duckdns.org/list"

R에서는 `curl`이나 `httr`에서 제공하는 함수를 바탕으로 요청할 수 있습니다.

``` r
tar<-"http://konlper.duckdns.org/list"
GET(tar)
```

    ## Response [http://konlper.duckdns.org/list]
    ##   Date: 2017-05-28 01:19
    ##   Status: 200
    ##   Content-Type: text/html; charset=utf-8
    ##   Size: 265 B

[KoNLP](https://cran.r-project.org/web/packages/KoNLP/vignettes/KoNLP-API.html)를 확인해서 어떻게 사용하는지 확인하세요. 아직 옵션이 있는 함수는 제대로 동작하지 않거나 기본 옵션으로만 동작합니다.

POST 요청으로 결과를 JSON 형태로 받을 수 있습니다.

현재 세종사전만 반영되어 있습니다. 무료 티어를 사용해서 속도가 매우 느립니다.
