## 테스트 툴
데이터베이스의 표준 성능 테스트는 sysbench 1.0.20입니다.

#### 툴 설치
본 문서의 테스트에서는 Sysbench 1.0.20 버전을 사용하며, 설치 방법은 아래와 같습니다.
```
git clone https://github.com/akopytov/sysbench.git
git checkout 1.0.20
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
cd sysbench
./autogen.sh
./configure
make -j
make install
```

>?상기 내용은 부하 테스트를 CVM(CentOS 시스템)에 설치하는 방법입니다. 다른 운영 체제에 설치하려면 [Sysbench 공식 문서](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)를 참고하십시오.

## 테스트 환경
| 유형               | 설명                                                         |
| :----------------- | :----------------------------------------------------------- |
| 테스트 인스턴스 사양       | 4코어 8GB 메모리, 8코어 32GB 메모리, 16코어 128GB 메모리의 세 가지 일반적으로 사용되는 테스트 사양 선택 |
| 클라이언트 설정         | 64코어 128GB메모리                                                |
| 클라이언트 내부 네트워크 대역폭     | 23Gbps                                                       |
| 테스트 데이터 볼륨         | 데이터베이스 인스턴스 메모리 * 1.2                                           |
| 데이터베이스 인스턴스 버전 테스트 | 5.6 20210630, 5.7 20210630, 8.0 20210330                       |

- 클라이언트 사양 설명: 비교적 높은 사양의 클라이언트 기기를 사용하여 단일 클라이언트도 데이터베이스 인스턴스의 성능 부하 테스트를 수행할 수 있습니다. 클라이언트의 사양이 낮은 경우, 인스턴스에 대해 여러 클라이언트로 동시에 부하 테스트를 수행하여 데이터의 합계를 구하는 것을 권장합니다.
- 네트워크 딜레이 설명: 테스트 환경은 클라이언트 기기와 데이터베이스 인스턴스가 동일한 가용존에 있도록 설정해야 합니다. 테스트 결과는 네트워크 환경의 영향을 받지 않습니다.


## 테스트 방법
### 테스트 데이터 준비
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write prepare
```

### 성능 부하 테스트 명령어
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write run
```

성능 부하 테스트 매개변수 설명:
- `oltp_read_write`, /usr/share/sysbench/oltp_read_write.lua 스크립트를 호출하여 oltp 모드 테스트 진행.
- `--tables=xxxx`, 이 테스트에 사용된 테이블 수.
- `--table_size=xxxx`, 이 테스트에 사용된 테이블 행의 수.
- `--num-threads=128`, 이 테스트의 클라이언트 동시 접속 수.
- `--report-interval=1`, 테스트 결과가 1초마다 출력됨.
- `--percentile=95`, 샘플링 비율 설정. 기본값: 95%.
- `--time=600`, 이 테스트의 실행 시간. 600은 600초를 나타냄.

### 시나리오 모델
본문의 사용 사례는 모두 sysbench의 lua 스크립트를 사용합니다.
일반적인 구성 유형의 각 매개변수 템플릿에 대한 성능 테스트를 수행합니다. 테스트 결과는 다음을 참고하십시오.

## 테스트 결과
#### 5.6 20210630 버전
<table>
<thead><tr><th>CPU(코어)</th><th>메모리(GB)</th><th>threads</th><th>테스트 시간</th><th>템플릿</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>34428.69</td><td>1721.43</td><td>18.59ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>35917.50</td><td>1795.87</td><td>17.82ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>34834.04</td><td>1741.70</td><td>18.37ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>61210.19</td><td>3060.51</td><td>20.91ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>67719.55</td><td>3385.98</td><td>18.90ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>64910.09</td><td>3245.50</td><td>19.72ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>106965.44</td><td>5348.27</td><td>23.93ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>127955.48</td><td>6397.77</td><td>20.00ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>119509.02</td><td>5975.45</td><td>21.41ms</td></tr>
</tbody></table>

#### 5.7 20210630 버전
<table>
<thead><tr><th>CPU(코어)</th><th>메모리(GB)</th><th>threads</th><th>테스트 시간</th><th>템플릿</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>34428.69</td><td>1721.43</td><td>18.59ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>35917.50</td><td>1795.87</td><td>17.82ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>34834.04</td><td>1741.70</td><td>18.37ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>61210.19</td><td>3060.51</td><td>20.91ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>67719.55</td><td>3385.98</td><td>18.90ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>64910.09</td><td>3245.50</td><td>19.72ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>106965.44</td><td>5348.27</td><td>23.93ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>127955.48</td><td>6397.77</td><td>20.00ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>119509.02</td><td>5975.45</td><td>21.41ms</td></tr>
</tbody></table>

#### 8.0 20210330 버전
<table>
<thead><tr><th>CPU(코어)</th><th>메모리(GB)</th><th>threads</th><th>테스트 시간</th><th>템플릿</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>32594.79</td><td>1629.74</td><td>19.63ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>33383.77</td><td>1669.19</td><td>19.17ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>32071.90</td><td>1603.60</td><td>19.95ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>65718.22</td><td>3285.91</td><td>19.47ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>70195.37</td><td>3509.77</td><td>18.23ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>60704.69</td><td>3035.23</td><td>21.08ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10분</td>
<td>기본 템플릿(폐기)</td><td>132023.66</td><td>6601.18</td><td>19.38ms</td></tr>
<tr>
<td>고성능 매개변수 템플릿</td><td>151021.67</td><td>7551.08</td><td>16.95ms</td></tr>
<tr>
<td>고안정성 템플릿</td><td>132391.01</td><td>6619.55</td><td>19.33ms</td></tr>
</tbody></table>

