---

copyright:

  years:  2016, 2018

lastupdated: "2018-07-19"

---

# Cloud Foundation 인스턴스의 클러스터 추가, 보기 및 삭제

인스턴스를 주문할 때 구성한 ESXi 서버는 기본 클러스터 아래에서 그룹화됩니다. 기본 클러스터 이름은 다음과 같습니다.
* V2.1 이상 릴리스로 배치된 인스턴스의 경우: **MGMT-Cluster-`<subdomain_label>`**
* V2.0 이하 릴리스로 배치된 인스턴스의 경우: **SDDC-Cluster**

클러스터를 VMware Cloud Foundation 인스턴스에 추가하여 컴퓨팅 및 스토리지 용량을 확장할 수 있습니다. 클러스터 내에서 향상된 리소스 할당 및 고가용성을 위해 ESXi 서버를 관리할 수 있습니다. 더 이상 필요하지 않은 경우에는 인스턴스에서 추가된 클러스터를 삭제할 수 있습니다.

**가용성**:
* 클러스터 추가 기능은 V2.0 이상 릴리스로 배치된(또는 이러한 릴리스로 업그레이드된) 인스턴스에서만 사용 가능합니다.
* 클러스터 삭제 기능은 V2.3 이상 릴리스로 배치된(또는 이러한 릴리스로 업그레이드된) 인스턴스에서만 사용 가능합니다.  

## Cloud Foundation 인스턴스에 클러스터 추가

Cloud Foundation 인스턴스에는 최대 다섯 개의 클러스터를 추가할 수 있습니다.

### 시스템 설정

Cloud Foundation 인스턴스에 클러스터를 추가할 때는 다음 설정을 지정해야 합니다.

#### 클러스터 이름

클러스터 이름은 다음 요구사항을 충족해야 합니다.
* 영숫자 문자 및 대시(-) 문자만 사용할 수 있습니다.
* 클러스터 이름은 영숫자 문자로 시작하고 끝나야 합니다.
* 클러스터 이름의 최대 길이는 30자입니다.
* 클러스터 이름은 Cloud Foundation 인스턴스 내에서 고유해야 합니다.

#### 데이터 센터 위치

클러스터의 {{site.data.keyword.CloudDataCent}} 위치는 기본적으로 Cloud Foundation 인스턴스의 {{site.data.keyword.CloudDataCent_notm}}로 설정됩니다. 배치된 인스턴스와 다른 {{site.data.keyword.CloudDataCent_notm}}에 클러스터를 배치할 수 있으나 두 {{site.data.keyword.CloudDataCents_notm}} 간의 네트워크 대기 시간이 150밀리초 미만인지 확인해야 합니다. 네트워크 대기 시간을 확인하기 위해 [SoftLayer IP Backbone Looking Glass](http://lg.softlayer.com/){:new_window}와 같은 도구를 사용할 수 있습니다.

사용 가능한 데이터 센터는 배치에 선택된 Bare Metal Server 구성에 따라 달라집니다. **사용자 정의됨** 구성을 선택하는 경우 선택된 데이터 센터에 추가 팟(Pod)이 포함되어 있으면 다른 {{site.data.keyword.cloud}} 인프라 팟(Pod)에도 클러스터를 배치할 수 있습니다. 이는 초기 인스턴스가 배치된 기본 {{site.data.keyword.cloud_notm}} 인프라 팟(Pod)이 최대 용량에 도달한 경우 유용합니다.

**참고:** 표준화된 **소형** 및 **대형** Bare Metal Server 구성은 변경할 수 없는 기본 팟(Pod)을 사용합니다.

다른 데이터 센터 또는 팟(Pod)에 클러스터를 배치하는 경우 주문된 {{site.data.keyword.baremetal_short}}에 사용할 세 개의 추가 VLAN이 주문됩니다.

### Bare Metal Server 설정

**사용자 정의됨** 또는 **사전 구성됨**을 선택할 수 있습니다.

#### 사용자 정의됨

**사용자 정의됨** 설정의 경우에는 **CPU 모델** 및 **RAM**에 대한 몇 가지 옵션이 있습니다. 사용 가능한 옵션은 인스턴스가 처음에 배치된 버전에 따라 다를 수 있습니다.

표 1. 사용자 정의된 {{site.data.keyword.baremetal_short}}의 옵션

|CPU 옵션   |RAM 옵션   |
|:------------- |:------------- |
| 듀얼 Intel Xeon E5-2620 v4 / 총 16개의 코어, 2.1GHz |128GB, 256GB, 512GB, 768GB, 1.5TB |
| 듀얼 Intel Xeon E5-2650 v4 / 총 24개의 코어, 2.2GHz |128GB, 256GB, 512GB, 768GB, 1.5TB |
| 듀얼 Intel Xeon E5-2690 v4 / 총 28개의 코어, 2.6GHz |128GB, 256GB, 512GB, 768GB, 1.5TB |
|듀얼 Intel Xeon Silver 4110 프로세서 / 총 16개의 코어, 2.1GHz | 128GB, 192GB, 384GB, 768GB, 1.5TB |
|듀얼 Intel Xeon Gold 5120 프로세서 / 총 28개의 코어, 2.2GHz | 128GB, 192GB, 384GB, 768GB, 1.5TB |
|듀얼 Intel Xeon Gold 6140 프로세서 / 총 36개의 코어, 2.3GHz | 128GB, 192GB, 384GB, 768GB, 1.5TB |

#### 사전 구성됨

**사전 구성됨** 설정의 경우에는 자신의 요구사항에 따라 **Bare Metal Server 구성**을 선택할 수 있습니다.
* 소형(듀얼 Intel Xeon E5-2650 v4 / 총 24개의 코어, 2.2GHz / 128GB RAM / 12개의 디스크)
* 대형(듀얼 Intel Xeon E5-2690 v4 / 총 28개의 코어, 2.6GHz / 512GB RAM / 12개의 디스크)

### vSAN 스토리지 설정

**사전 구성됨** Bare Metal Server 구성의 경우에는 vSAN 스토리지 설정을 변경할 수 없습니다.
* **소형** 구성의 경우, 두 개의 1.9TB SSD SED 디스크 드라이브가 주문됩니다.
* **대형** 구성의 경우, 네 개의 3.8TB SSD SED 디스크 드라이브가 주문됩니다.

**사용자 정의됨** Bare Metal Server 구성의 경우에는 vSAN 용량 디스크의 수, 자신의 스토리지 요구사항을 만족시키는 디스크 유형 및 크기를 지정하여 vSAN 스토리지를 사용자 정의할 수 있습니다.

### 라이센스 부여 설정

VMware vSphere 및 VMware vSAN을 포함한 클러스터의 VMware 컴포넌트에 대한 라이센싱 옵션을 지정할 수 있습니다.
* 비즈니스 파트너 사용자의 경우, vSphere 라이센스(Enterprise Plus 에디션) 및 vSAN 라이센스가 사용자를 대신하여 포함 및 구매됩니다. 그러나 vSAN 라이센스의 에디션은 지정해야 합니다.
* 비즈니스 파트너가 아닌 사용자의 경우에는 **구매에 포함**을 선택하여 컴포넌트에 대해 IBM 제공 VMware 라이센스를 사용하거나, **라이센스를 제공함**을 선택하고 자신의 라이센스 키를 입력하여 컴포넌트에 대해 BYOL(Bring Your Own License)을 사용할 수 있습니다.

## Cloud Foundation 인스턴스에 클러스터를 추가하는 프로시저

1. {{site.data.keyword.vmwaresolutions_short}} 콘솔의 왼쪽 탐색 분할창에서 **배치된 인스턴스**를 클릭하십시오.
2. **Cloud Foundation 인스턴스** 테이블에서 클러스터를 추가할 인스턴스를 클릭하십시오.

   **참고:** 인스턴스가 **사용할 준비** 상태인지 확인하십시오. 그렇지 않으면, 클러스터를 인스턴스에 추가할 수 없습니다.

3. 왼쪽 탐색 분할창의 **인프라**를 클릭하고 **클러스터** 테이블의 오른쪽 상단 모서리에 있는 **추가**를 클릭하십시오.
4. **클러스터 추가** 페이지에서 인스턴스 이름을 입력하십시오.
5. 인스턴스가 호스팅되는 {{site.data.keyword.CloudDataCent_notm}}와 다른 IBM Cloud Data Center에서 클러스터를 호스팅하려면 **Bare Metal Server**에서 **다른 위치 선택** 선택란을 선택하고 인스턴스를 호스팅할 {{site.data.keyword.CloudDataCent_notm}}를 선택하십시오.
6. Bare Metal Server 구성을 완료하십시오.
   * **사용자 정의됨**을 선택한 경우에는 **CPU 모델** 및 **RAM** 크기를 선택하십시오.
   * **사전 구성됨**을 선택한 경우에는 **Bare Metal Server 구성**을 선택하십시오.
7. 스토리지 구성을 완료하십시오.
   * Bare Metal Server 구성에 대해 **사용자 정의됨**을 선택한 경우에는 **vSAN 용량 디스크 수** 및 **vSAN 용량 디스크의 디스크 유형 및 크기**를 지정하십시오.
   * Bare Metal Server 구성에 대해 **사전 구성됨**을 선택한 경우에는 **소형** 및 **대형** Bare Metal Server 구성의 스토리지 설정을 변경할 수 없다는 점을 참고하십시오.
8. 라이센스 키의 제공 방법을 지정하십시오.
   * 비즈니스 파트너 사용자의 경우, vSphere 라이센스(Enterprise Plus 에디션) 및 vSAN 라이센스가 사용자를 대신하여 포함 및 구매됩니다. 그러나 vSAN 라이센스의 에디션은 지정해야 합니다.
   * 비즈니스 파트너가 아닌 사용자의 경우에는 다음 옵션 중 하나를 선택할 수 있습니다.
       * 사용자 대신 새 라이센스를 구매하려는 경우 컴포넌트에 대한 **구매에 포함**을 선택하십시오. VMware vSAN의 경우에는 라이센스 에디션도 선택하십시오.
       * 컴포넌트에 고유한 VMware 라이센스를 사용할 경우 **제공함**을 선택하고 컴포넌트의 라이센스 키를 입력하십시오.
9. 클러스터를 추가하기 전에 **주문 요약** 페이지에서 클러스터 구성을 확인하십시오.
   1. 클러스터의 설정을 검토하십시오.
   2. 클러스터의 예상 비용을 검토하십시오. PDF 요약을 생성하려면 **가격 책정 세부사항**을 클릭하십시오. 주문 요약을 저장하거나 인쇄하려면 PDF 창의 오른쪽 상단에 있는 **인쇄** 또는 **다운로드** 아이콘을 클릭하십시오.
   3. 주문에 적용되는 이용 약관에 대한 링크를 클릭하고, 클러스터를 추가하기 전에 이러한 이용 약관에 동의하는지 확인하십시오.
   4. **프로비저닝**을 클릭하십시오.

### Cloud Foundation 인스턴스에 클러스터를 추가한 후의 결과

1. 클러스터의 배치가 자동으로 시작되며 클러스터의 상태가 **초기화 중**으로 변경됩니다. 인스턴스 요약 페이지의 배치 히스토리를 보고 배치 상태를 확인할 수 있습니다.
2. 클러스터를 사용할 준비가 되면 클러스터의 상태가 **사용할 준비**로 변경됩니다. 새로 추가된 클러스터는 vSphere HA(High Availability) 및 vSphere DRS(Distributed Resource Scheduler)로 사용 가능합니다.

**중요**: 클러스터 이름을 변경할 수 없습니다. 클러스터 이름을 변경하면 클러스터의 ESXi 서버 오퍼레이션을 추가하거나 제거하는 데 실패할 수 있습니다.

## Cloud Foundation 인스턴스의 클러스터 보기

1. {{site.data.keyword.vmwaresolutions_short}} 콘솔의 왼쪽 탐색 분할창에서 **배치된 인스턴스**를 클릭하십시오.
2. **Cloud Foundation 인스턴스** 테이블에서 클러스터를 볼 인스턴스를 클릭하십시오.
3. 왼쪽 탐색 분할창에서 **인프라**를 클릭하십시오. **클러스터** 테이블에서 클러스터에 대한 요약을 보십시오.
   * **이름**: 클러스터의 이름입니다.
   * **ESXi 서버**: 클러스터에 있는 ESXi 서버의 수입니다.
   * **CPU**: 클러스터에 있는 ESXi 서버의 CPU 스펙입니다.
   * **사용자 정의된 vSAN 디스크**: 클러스터에 있는 vSAN 디스크의 수로, 디스크 유형 및 용량이 포함됩니다.
   * **메모리**: 클러스터에 있는 ESXi 서버의 총 메모리 크기입니다.
   * **데이터 센터 위치**: 클러스터가 호스팅되는 데이터 센터입니다.
   * **팟(Pod)**: 클러스터가 배치된 팟(Pod)입니다.
   * **상태**: 클러스터의 상태입니다. 상태는 다음 값 중 하나를 포함할 수 있습니다.
   <dl class="dl">
       <dt class="dt dlterm">초기화 중</dt>
       <dd class="dd">클러스터가 작성 및 구성 중입니다.</dd>
       <dt class="dt dlterm">수정 중</dt>
       <dd class="dd">클러스터가 수정 중입니다.</dd>
       <dt class="dt dlterm">사용할 준비</dt>
       <dd class="dd">인스턴스를 사용할 준비가 되었습니다.</dd>
       <dt class="dt dlterm">삭제 중</dt>
       <dd class="dd">클러스터가 삭제되는 중입니다.</dd>
       <dt class="dt dlterm">삭제됨</dt>
       <dd class="dd">클러스터가 삭제되었습니다.</dd>
   </dl>
   * **조치**: **삭제** 아이콘을 클릭하여 클러스터를 삭제하십시오.
4. 클러스터 이름을 클릭하여 ESXi 서버 및 해당 정보의 목록을 보십시오.

   * **이름**: ESXi 서버의 이름으로, 형식은 `<host_prefix><n>.<subdomain_label>.<root_domain>`이며 여기서

      `host_prefix`는 호스트 이름 접두부입니다.
      `n`은 ESXi 서버의 순서입니다.
      `subdomain_label`은 하위 도메인 레이블입니다.
      `root_domain`은 루트 도메인 이름입니다.

   * **버전**: ESXi 서버의 버전입니다.
   * **신임 정보**: ESXi 서버에 액세스하는 데 사용되는 사용자 이름 및 비밀번호입니다.
   * **사설 IP**: ESXi 서버의 사설 IP 주소입니다.
   * **상태**: ESXi 서버의 상태이며, 다음 값 중 하나가 될 수 있습니다.
        <dl class="dl">
        <dt class="dt dlterm">추가됨</dt>
        <dd class="dd">ESXi 서버가 추가되었으며 사용할 준비가 되었습니다. </dd>
        <dt class="dt dlterm">추가 중</dt>
        <dd class="dd">ESXi 서버가 추가 중입니다. </dd>
        <dt class="dt dlterm">삭제 중</dt>
        <dd class="dd">ESXi 서버가 삭제 중입니다.</dd>
        </dl>
   * vSAN 라이센스 및 vSphere 라이센스의 세부사항입니다. vSphere 라이센스 세부사항은 클러스터 주문 중에 자신의 VMware 라이센스를 사용(BYOL)하도록 선택한 경우에만 사용 가능합니다.
       * **라이센스 유형**: vSAN 라이센스 또는 vSphere 라이센스입니다.
       * **주문 유형**: 라이센스가 사용자에 의해 제공(BYOL)되거나 사용자 대신 구매됩니다.
       * **라이센스 에디션**: 라이센스의 에디션입니다.
       * **라이센스 키**: 라이센스 키입니다.
       * **총 용량(CPU)**: 라이센스에 의해 제공되는 총 용량 또는 CPU 수입니다.
       * **사용 가능한 용량(CPU)**: 라이센스에서 현재 사용 가능한 용량입니다.

## Cloud Foundation 인스턴스에서 클러스터 삭제

더 이상 필요하지 않은 경우 인스턴스에서 클러스터를 삭제할 수 있습니다.

### 삭제하기 전에

* 이 프로시저는 V2.3 이상 릴리스로 배치된 인스턴스에서 클러스터를 삭제하는 데 사용하십시오.
* V2.2 이하 인스턴스에 배치된 클러스터의 경우에는 인스턴스에 추가한 클러스터를 삭제하려면 인스턴스를 V2.3으로 업그레이드해야 합니다.
* 한 번에 하나의 클러스터를 삭제할 수 있습니다. 여러 클러스터를 삭제하려면 이들을 순서대로 삭제해야 합니다(즉, 다음 클러스터를 삭제하려 시도하기 전에 이전 클러스터가 삭제되기를 기다려야 함).
* 클러스터를 삭제하기 전에 클러스터의 모든 노드가 켜져 있으며 가동 상태인지 확인하십시오.
* 클러스터를 삭제하면 클러스터의 모든 가상 머신(VM) 또한 삭제되며 이는 복구할 수 없습니다. VM을 보존하려는 경우에는 이들을 다른 클러스터로 마이그레이션하십시오.
* 기본 클러스터는 삭제할 수 없습니다.

## Cloud Foundation 인스턴스에서 클러스터를 삭제하는 프로시저

1. {{site.data.keyword.vmwaresolutions_short}} 콘솔의 왼쪽 탐색 분할창에서 **배치된 인스턴스**를 클릭하십시오.
2. **Cloud Foundation 인스턴스** 테이블에서 클러스터를 삭제할 인스턴스를 클릭하십시오.

   **참고**: 인스턴스가 **사용할 준비** 상태인지 확인하십시오. 그렇지 않으면 인스턴스에서 클러스터를 삭제할 수 없습니다.

3. 왼쪽 탐색 분할창에서 **인프라**를 클릭하십시오. **클러스터** 테이블에서 삭제할 클러스터를 찾고 **삭제** 아이콘을 클릭하십시오.
4. 해당되는 경우에는 다른 클러스터로의 VM 마이그레이션을 완료했는지 확인하고, 클러스터를 삭제할지 확인하십시오.

### 관련 링크

* [Cloud Foundation 인스턴스 보기](sd_viewinginstances.html)
* [Cloud Foundation 인스턴스에 대한 용량 확장 및 축소](sd_addingremovingservers.html)
