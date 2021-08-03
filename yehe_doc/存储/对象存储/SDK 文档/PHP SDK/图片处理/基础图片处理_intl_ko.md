## 소개

Tencent Cloud COS(Cloud Object Storage)는 [Cloud Infinite(CI)](https://intl.cloud.tencent.com/document/product/1045)의 전문적인 일체형 멀티미디어 솔루션을 통합하여 다음과 같은 이미지 처리 기능을 제공합니다. 자세한 내용은 [이미지 처리 개요](https://intl.cloud.tencent.com/document/product/436/35280)를 참고하십시오.


<table>
   <tr>
      <th>서비스</td>
      <th>기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td rowspan=14>기본 이미지 처리 서비스</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">크기 조절</a></td>
      <td>동일 비율 조정, 타깃의 가로:세로 비율 설정 등 다양한 방법</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">자르기</a></td>
      <td>일반 자르기, 크기 조정 자르기, 내접원 자르기, 스마트 얼굴 자르기</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">회전</a></td>
      <td>자동 회전, 일반 회전</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">형식 변환</a></td>
      <td>포맷 변환, GIF 포맷 최적화, 점진적 표시</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">품질 변경</a></td>
      <td>JPG 및 WEBP 이미지 품질 변경</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">가우시안 블러</a></td>
      <td>이미지 가우시안 블러 처리</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/40647">밝기</a></td>
      <td>이미지 밝기 조절</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/40648">대비</a></td>
      <td>이미지 대비 조절</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">샤프닝</a></td>
      <td>이미지 샤프닝 처리</td>
   </tr>
   <tr>
      <td>워터마크 추가</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">이미지 워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">문자 워터마크</a></td>
   </tr>
   <tr>
      <td>이미지 정보 가져오기</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">기본 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">메인 컬러</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">메타 정보 삭제</a></td>
      <td>EXIF 정보 포함</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">빠른 섬네일 템플릿 </a></td>
      <td>이미지의 빠른 포맷 변환, 축소, 자르기 등 기능 구현 및 썸네일 생성</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36380">파이프 연산자</a></td>
      <td>순서에 따라 이미지에 여러 처리 효과 구현</td>
   </tr>
</table>




## 인스턴스화 Template

기본 이미지 처리 기능 사용 시, 먼저 Template 클래스를 인스턴스화하고, 메소드를 호출하여 CI 이미지 처리 매개변수를 생성한 후, 파일 리소스를 얻을 때 전달합니다. 아래의 모든 작업은 동일하므로 중복적으로 설명하지 않습니다.

#### 예시코드

```php
try{
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();//기본 이미지 처리 매개변수 템플릿 인스턴스 생성
        $imageMogrTemplate->thumbnailByScale(50);// 이미지의 너비와 높이는 원본 이미지의 50%로 지정
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(),//기본 이미지 처리 매개변수 생성
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |
| ImageHandleParam      | String      | CI 이미지 처리 매개변수. 예시: imageMogr2/thumbnail/!50p      | 예        |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [CacheControl] => max-age=2592000
            [ContentType] => image/jpeg
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
        )

)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 콘텐츠 다운로드                                                     | 없음     |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| CacheControl         | String | 캐시 정책. Cache-Control 설정                                 | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| ContentLength        | Int         | 응답 본문 길이                                                 | 없음     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |

## 크기 조정

### 백분율에 따라 확대/축소

```php
$imageMogrTemplate->thumbnailByScale(50);// 이미지의 너비와 높이는 원본 이미지의 50%로 지정.
$imageMogrTemplate->thumbnailByWidthScale(50);//이미지의 너비는 원본 이미지의 50%로 지정，높이는 변하지 않음.
$imageMogrTemplate->thumbnailByHeightScale(50);//이미지의 높이는 원본 이미지의 50%로 지정, 너비는 변하지 않음.
```

### 이미지 너비/높이의 확대/축소 지정

```php
$imageMogrTemplate->thumbnailByWidth(50);//대상 이미지의 너비는 50으로 지정，높이는 동일 비율 압축.
$imageMogrTemplate->thumbnailByHeight(50);//대상 이미지의 높이는 50으로 지정，너비는 동일 비율 압축.
$imageMogrTemplate->thumbnailByMaxWH(50, 50);//썸네일의 최대 너비과 높이를 각각 50과 50으로 제한하고 동일 비율로 확대/축소.
$imageMogrTemplate->thumbnailByMinWH(50, 50);//썸네일의 최소 너비과 높이를 각각 50과 50으로 제한하고 동일 비율로 확대/축소.
$imageMogrTemplate->thumbnailByWH(50, 50);//원본 이미지의 너비와 높이의 비율은 무시하고 이미지의 너비를 50으로, 높이를 50으로 지정. 이미지를 강제로 확대하면 대상 이미지가 변형될 수 있음.
```

### 동일 비율 축소/확대

```php
$imageMogrTemplate->thumbnailByPixel(1000);//이미지를 동일 비율로 확대/축소, 총 픽셀 수가 1,000을 초과하지 않음.
```

## 자르기


### 일반 자르기

```php
$imageMogrTemplate->cut(100, 300, 30, 30);//대상 이미지 너비, 높이, 이미지의 왼쪽 위 꼭지점을 기준으로 오른쪽으로 수평 이동, 이미지의 왼쪽 위 꼭지점을 기준으로 아래쪽으로 수평 이동하여 자르기.
```

### 축소/확대 자르기

포지셔닝에 대한 설명은, [3x3 그리드 포지셔닝](https://intl.cloud.tencent.com/document/product/436/36367)을 참고하십시오.

```php
$imageMogrTemplate->cropByWidth(100);//지정된 타깃 너비에 따라 크기 조정 및 자르기.
$imageMogrTemplate->cropByWidth(100, 'center');//지정된 타깃 너비에 따라 크기 조정 및 자르기, 작업 시작점 지정.
$imageMogrTemplate->cropByHeight(100);//지정된 타깃 높이에 따라 크기 조정 및 자르기
$imageMogrTemplate->cropByHeight(100, 'center');//지정된 타깃 높이에 따라 크기 조정 및 자르기, 작업 시작점 지정.
$imageMogrTemplate->cropByWH(100, 100);//지정된 타깃 너비와 높이에 따라 크기 조정 및 자르기.
$imageMogrTemplate->cropByWH(100, 100, 'center');//지정된 대상 너비와 높이에 따라 크기 조정 및 자르기, 작업 시작점 지정.
```

### 내접원 자르기

radius는 내접원의 반경이고 값 범위는 0보다 크고 원본 이미지의 가장 작은 변의 절반보다 작은 정수입니다. 내접원의 중심이 그림의 중심입니다. 이미지 형식이 GIF인 경우 이 작업은 지원되지 않습니다.

```php
$imageMogrTemplate->iradius(100);//예시: 반경을 100으로 지정.
```

### 둥근 모서리 자르기

radius는 이미지의 둥근 모서리의 반경이고 값 범위는 0보다 크고 원본 이미지의 가장 작은 변의 절반보다 작은 정수입니다. 둥근 모서리와 원본 이미지의 가장자리는 맞닿아 있습니다. 이미지 형식이 GIF인 경우 이 작업은 지원되지 않습니다.

```php
$imageMogrTemplate->rradius(1000);//예시: 둥근 모서리 반경을 100으로 지정.
```

### 스마트 얼굴 자르기

이미지에서 얼굴의 위치에 따라 크기를 조정하고 자릅니다. 대상 이미지의 너비는 Width, 높이는 Height입니다.

```php 
$imageMogrTemplate->scrop(100, 100);// 예시: 얼굴을 자르고 너비와 높이를 100으로 확대/축소하도록 지정.
```

### 회전


### 일반 회전

그림은 시계 방향으로 회전하고 값 범위는 0-360이며 기본 설정은 회전하지 않는 것입니다.

```php
$imageMogrTemplate->rotate(45);//예시: 45도 회전
```

### 자동 회전

원본 이미지 EXIF ​​정보에 따라 이미지가 자동으로 회전됩니다.

```php
$imageMogrTemplate->autoOrient();
```

## 형식 전환


### 일반 전환

대상 썸네일의 이미지 형식은 jpg, bmp, gif, png, webp, yjpeg 등일 수 있으며, 그 중 yjpeg는 jpeg 형식의 최적화되어 있으며 본질적으로 jpg 형식입니다. 디폴트 값은 원본 이미지 형식입니다.

```php
$imageMogrTemplate->format('png');//형식 png으로 전환
```

### GIF 형식 최적화

이 기능은 gif 형식의 원본 이미지에만 적용되며, gif 이미지 형식을 최적화하여 프레임과 색상을 줄입니다. 다음 두 가지 상황으로 나뉩니다.
- FrameNumber=1，기본 프레임 수 30에 따라 처리하며, 이미지 프레임 수가 해당 프레임 수보다 많으면 캡처합니다.
- FrameNumber 값 ( 1,100 ]，지정된 프레임 수로 이미지를 압축합니다 (FrameNumber).

```php
$imageMogrTemplate->gifOptimization(50);//지정된 프레임 수 50으로 압축
```

### 프로그래시브 JPG 형식 출력

이 작업은 출력 이미지 형식이 jpg 형식인 경우에만 유효합니다. 출력이 jpg 이미지 형식이 아닌 경우 이 매개변수는 무시됩니다. 값 범위는 0 또는 1입니다. 0: 프로그레시브 활성화 하지 않음, 1: 프로그레시브 활성화, 기본값 0.

```php
$imageMogrTemplate->jpegInterlaceMode(1);//프로그래시브 활성화.
```

## 품질 변환

품질 변환 기능은 절대 변환, 상대 변환, 최소 품질 변환 및 조정 가능한 화질의 세 가지 변환 유형을 제공합니다. 이 기능은 JPG 및 WEBP 형식의 이미지에만 적용됩니다.

### 절대 변환

이미지의 절대 품질을 설정하고 값의 범위는 0-100이며 기본값은 원본 이미지 품질입니다. 원본 이미지 품질과 지정된 품질의 최소값을 취합니다.
지정된 값을 강제로 사용할지 여부의 값 범위는 0 또는 1입니다. 0: 강제로 사용하지 않음, 1: 강제로 사용함, 기본값 0.

```php
$imageMogrTemplate->quality(90, 1);//강제 지정 품질 90
```

### 상대 변환

이미지의 상대적 품질을 설정하고, 값의 범위는 0-100 입니다. 수치는 원본 이미지 품질을 기준으로 합니다. 예를 들어 원본 이미지 품질은 80이고, rquality를 80으로 설정한 후 처리된 결과 이미지의 품질은 64(80x80%)입니다.

```php
$imageMogrTemplate->relativelyQuality(80);
```

### 최저 품질 변환

이미지의 최저 품질이며, 값의 범위는0 - 100입니다. 결과 이미지의 품질 매개변수 최소값을 설정합니다.
- 예를 들어 원본 이미지 품질이 85이고 lquality를 80으로 설정하면 처리 결과 이미지의 품질은 85입니다.
- 예를 들어 원본 이미지 품질이 60이고 lquality를 80으로 설정하면 처리 결과 이미지의 품질은 80으로 향상됩니다.

```php
$imageMogrTemplate->lowestQuality(90);
```

## 가우시안 블러

가우시안 블러 기능으로 블러 반경 값의 범위는 1-50입니다. 정규 분포의 표준 편차는 0보다 커야 합니다. 이미지 형식이 gif인 경우 이 매개변수는 지원되지 않습니다.

```php
$imageMogrTemplate->blur(20, 20);// 예시: 블러 반경 20，정규 분포의 표준 편차 20
```

## 밝기

이미지 밝기 조정 기능으로, 값 범위는 [-100, 100]의 정수입니다.

```php
//값＜0：이미지 밝기 낮추기.
//값 = 0：이미지 밝기 조정하지 않음.
//값＞0：이미지 밝기 높임.
$imageMogrTemplate->bright(50);// 이미지 밝기 50 높이기
```

## 대비

이미지 대비 조정 기능으로, 값 범위는 [-100, 100]의 정수입니다.

```php
//값＜0：이미지 대비 낮추기.
//값 = 0：이미지 대비 조정하지 않음.
//값＞0：이미지 대비 높이기.
$imageMogrTemplate->contrast(50);// 이미지 대비 50 높이기.
```

## 샤프닝

이미지 샤프닝 기능으로, 값 범위는 10-300 사이의 정수이며 70이 권장됩니다. 매개변수 값이 클수록 샤프닝 효과가 더 분명해집니다.

```php
$imageMogrTemplate->sharpen(70);// 예시: 샤프닝 값 70
```

## 워터마크 추가

포지셔닝에 대한 설명은, [3x3 그리드 포지셔닝](https://intl.cloud.tencent.com/document/product/436/36367)을 참고하십시오.

### 이미지 워터마크

지정된 워터마크 이미지는 아래의 3가지 조건을 동시에 만족시켜야 합니다.
1. 워터마크 이미지와 소스 이미지는 같은 버킷에 있어야 합니다.
2. URL은 COS 도메인 이름을 사용해야 하며(CDN 가속 도메인 이름은 사용할 수 없음. 예: examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png는 사용할 수 없음) 워터마크 이미지 액세스가 보장되어야 합니다. 워터마크 이미지 읽기 권한이 개인 읽기인 경우 유효한 서명을 보유해야 합니다.
3. URL은 `http://`로 시작해야 하고, HTTP 헤더는 생략할 수 없으며 HTTPS 헤더는 입력할 수 없습니다. 예: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`, ` https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png`는 불법 워터마크 URL입니다.

```php
try{
        $imageWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\ImageWatermarkTemplate();//이미지 워터마크 매개변수 템플릿 인스턴스 생성
        $imageWatermarkTemplate->setImage("imageurl");//워터마크 이미지 주소 설정.
        $imageWatermarkTemplate->setGravity('center');//워터마크 3x3 그리드 위치 설정.
        $imageWatermarkTemplate->setDx(10);//수평(가로축) 여백 설정.
        $imageWatermarkTemplate->setDy(10);//수직(세로축) 여백 설정
        $imageWatermarkTemplate->setBlogo(1);//워터마크 이미지 크기가 너무 큰 시나리오(워터마크 배경 등)에 적합한 워터마크 이미지 자동 조절 기능은 두 가지 유형이 있습니다: 1로 설정하면 워터마크 이미지의 크기가 원본 이미지와 비슷한 크기로 확대/축소된 후 추가되며, 2로 설정하면 워터마크 이미지가 원본 이미지와 비슷한 크기로 잘린 후 추가됩니다.
        $imageWatermarkTemplate->setScatype(1);//원본 이미지 크기에 따라 워터마크 이미지 크기를 조정합니다. 1: 너비 기준 확대/축소, 2: 높이 기준 확대/축소, 3: 면적 기준 확대/축소
        $imageWatermarkTemplate->setSpcent(100);//원본 이미지에 대한 워터마크 이미지의 천분율을 100/1000으로 설정하고, 값의 범위는 [1,1000]이며, 기본값은 원본 워터마크 이미지 크기입니다.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageWatermarkTemplate->queryString(),//이미지 워터마크 매개변수 생성.
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}

```

### 텍스트 워터마크

COS는 실시간 텍스트 워터마크 처리 기능을 제공합니다. 워터마크 폰트 목록은 [지원되는 폰트 목록](https://intl.cloud.tencent.com/document/product/1045/40681)을 참고하십시오. 폰트 색상 목록은 [RGB 코드표](https://www.rapidtables.com/web/color/RGB_Color.html)를 참고하십시오.

```php
try{
        $textWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\TextWatermarkTemplate();//텍스트 워터마크 매개변수 템플릿 인스턴스 생성
        $textWatermarkTemplate->setText("test");//워터마크 내용 설정
        $textWatermarkTemplate->setFont("tahoma.ttf");//워터마크 폰트 설정. 기본값 tahoma.ttf
        $textWatermarkTemplate->setFontsize(30);//워터마크 텍스트 폰트 사이즈 설정, 단위: pt, 기본값: 13.
        $textWatermarkTemplate->setFill("#3D3D3D");//폰트 색상을 설정하려면 16진수 RGB 형식(예: #FF0000)으로 설정해야 하며 기본값은 #3D3D3D(회색).
        $textWatermarkTemplate->setDissolve(90);//텍스트 투명도 설정, 값은 1-100, 기본값은 90(완전히 불투명).
        $textWatermarkTemplate->setGravity('center');//텍스트 워터마크의 위치 설정, 3x3 그리드 위치(3x3 그리드 위치 이미지 참고), 기본값은 southeast.
        $textWatermarkTemplate->setDx(10);//가로(가로축) 여백 설정, 단위는 픽셀, 기본값은 0.
        $textWatermarkTemplate->setDy(10); //세로(세로축) 여백 설정, 단위는 픽셀, 기본값은 0.
        $textWatermarkTemplate->setDegree(1);//​​워터마크 바둑판식 배열 기능을 설정하여 텍스트 워터마크를 전체 그림에 바둑판식으로 배열. 1로 설정 시 워터마크 바둑판식 배열 기능 활성화.
        $textWatermarkTemplate->setBatch(45);//텍스트 워터마크의 회전 각도 설정, 값의 범위: 0-360, 기본값: 0.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //포맷: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $textWatermarkTemplate->queryString(),//텍스트 워터마크 매개변수 생성.
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```


## 이미지 정보 가져오기

### 이미지 기본 정보 가져오기

이미지 기본 정보 조회.

#### 예시코드

```php
try{
        $result = $cosClient->ImageInfo(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"format": "jpeg", "width": "400", "height": "400"}
        )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 응답 본문                                                     | 없음     |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| ContentLength        | Int         | 응답 본문 길이                                                 | 없음     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
| Data                 | Json/String      | 이미지 기본 정보                            | 없음     |

### 이미지 EXIF 가져오기

이미지 EXIF ​​정보를 가져옵니다. 이미지 exif 정보가 없으면 {"error": "no exif data"}를 반환합니다.

#### 예시코드

```php
try{
        $result = $cosClient->ImageExif(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 32
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"error" : "no exif data"}
        )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 응답 본문                                                     | 없음     |
| RequestId             | String      | ID 식별 요청                                   | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| ContentLength        | Int         | 응답 본문 길이                                                 | 없음     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
| Data                 | Json/String      | 이미지 EXIF 정보                            | 없음     |

### 그림의 메인 색상 가져오기

이미지 메인 색상 정보를 가져옵니다.

#### 예시코드

```php
try{
        $result = $cosClient->ImageAve(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

#### 매개변수 설명

| 매개변수 이름             | 유형        | 설명                                                         | 필수 입력 여부 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket               | String      | 버킷 이름. 형식: BucketName-APPID                           | 예       |
| Key                  | String      | 여기서 Key는 객체 키로, 객체에 대한 버킷에서의 고유 식별자. 예시: 객체 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 `doc/pic.jpg` | 예       |

#### 반환 결과 예시

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 19
            [ContentType] => application/json
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => {"RGB": "0x483519"}
        )
)

```

#### 반환 결과 설명

| 매개변수 이름             | 유형        | 설명                                                         | 부모 노드 |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 응답 본문                                                     | 없음     |
| RequestId             | String      | ID 식별 요청                                | 없음     |
| ContentType          | String      | 콘텐츠 유형. Content-Type 설정                                  | 없음     |
| ContentLength        | Int         | 응답 본문 설정                                                 | 없음     |
| Key                  | String      | 객체 키                                     | 없음     |
| Bucket           | String | 버킷 이름. 형식: BucketName-APPID      | 없음     |
| Location             | String      | 리소스 주소 요청                                 | 없음     |
| Data                 | Json/String      | 이미지 메인 색상 정보                            | 없음     |



## 메타 정보 제거

EXIF 정보를 포함한 이미지 메타 정보를 제거합니다.

```php
$imageMogrTemplate->strip();//메타 정보 제거
```

## 빠른 썸네일 템플릿

자주쓰는 이미지 처리 템플릿을 제공하고 해당 썸네일을 생성합니다.

```php
try{
        $imageViewTemplate = new Qcloud\Cos\ImageParamTemplate\ImageViewTemplate();//빠른 썸네일 템플릿 매개변수 템플릿 인스턴스 생성
        $imageViewTemplate->setMode(1);//썸네일 모드 설정, 값 범위 [1, 5]:1: 썸네일 너비와 높이 최소값을 제한. 이 작업은 이미지 한 변이 설정된 최소값에 도달할 때까지 이미지를 동일 비율로 조정한 다음, 설정값에 도달할 때까지 다른 한 변을 센터 크롭. 한 변만 지정하면 너비와 높이가 같은 정사각형을 의미. 2: 썸네일 너비와 높이의 최대값을 제한. 이 작업은 너비와 높이가 설정된 최대값보다 작아질 때까지 이미지를 동일 비율로 확대/축소함. 3: 썸네일 너비와 높이의 최소값을 제한. 이 작업은 너비와 높이가 설정된 최소값보다 클 때까지 이미지의 크기를 동일 비율로 조정. 4: 썸네일의 긴 변과 짧은 변의 최소값을 제한하고 동일한 비율의 압축 진행. 만약 한 변만 지정하면 다른 한 변도 같은 값을 가짐 5: 썸네일의 긴 변과 짧은 변의 최대값을 제한하고, 동일한 비율의 압축 및 센터 크롭 진행. 한 변만 지정하면 동일한 너비와 높이의 정사각형을 의미함. 확대/축소 후 그 중 한 변의 여분 부분은 잘림.
        $imageViewTemplate->setWidth(400);//너비 설정.
        $imageViewTemplate->setHeight(600);//높이 설정.
        $imageViewTemplate->setFormat();//타깃 썸네일의 이미지 형식 설정. 가능한 형식: jpg, bmp, gif, png, webp, 기본값: 원본 이미지 형식.
        $imageViewTemplate->setQuality(1, 85);//이미지 품질 유형 및 이미지 품질 설정. 이미지 품질 유형: 1: 절대 품질, 2: 상대 품질, 3: 최저 품질.
        $imageViewTemplate->setQuality(1, 85, 1);//이미지 품질 유형이 절대 품질일 경우 지정된 값을 강제로 사용할 수 있음.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageViewTemplate->queryString(),//빠른 썸네일 템플릿 매개변수 생성.
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```


## 파이프 연산자

CIParamTransformation은 여러 작업 그룹을 지원합니다.

```php

try{
    $ciParamTransformation = new Qcloud\Cos\ImageParamTemplate\CIParamTransformation();//파이프라인 매개변수 템플릿 인스턴스 생성
    $ciParamTransformation = new Qcloud\Cos\ImageParamTemplate\CIParamTransformation("#");//파이프 연산자가 "|"이 아닌 경우 인스턴스를 생성할 때 지정해야 함.
    $ciParamTransformation->addRule($imageMogrTemplate);//기본 이미지 처리 매개변수 설정.
    $ciParamTransformation->addRule($imageWatermarkTemplate);//이미지 워터마크 처리 매개변수 설정.
    $ciParamTransformation->addRule($textWatermarkTemplate);//텍스트 워터마크 처리 매개변수 설정.
    $ciParamTransformation->addRule($imageViewTemplate);//빠른 썸네일 템플릿 매개변수 설정.
$result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //형식: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $ciParamTransformation->queryString(),//파이프라인 스티칭 매개변수 생성
    ));
    // 요청 완료
    print_r($result);
} catch (\Exception $e) {
    // 요청 실패
    echo($e);
}
```

