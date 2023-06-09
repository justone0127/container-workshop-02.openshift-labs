## Account Day - Container Workshop - OpenShift Labs

컨테이너 기술의 특징을 확인하고, 가상머신과의 차이점을 알아보는 데모입니다. 

```
목차
1. 환경 설명
2. OpenShift 환경 배포
3. Blue/Green 테스트
4. A/B 테스트
```

<br/>

### 1. 환경 설명

Workshop 환경은 OpenShift Cluster 환경에서 실행되며, 각 고유한 계정을 부여받게 됩니다.

- **OpenShift**
  - `Web Terminal` : OpenShift 환경에서 실행되는 VM접속 및 CLI를 실행 할 수 있는 Web Terminal 환경
  - 각 사용자마다 Lab을 실행할 수 있는 계정과 프로젝트가 제공됩니다. 
    - 프로젝트 : 애플리케이션을 배포할 수 있는 논리 단위로 실습 진행 시 프로젝트를 생성하실 때에는 `userx-`로 시작하도록 프로젝트를 생성하여 실습을 진행합니다.

**1-1) OpenShift Console 접속 방법**

- OpenShift Console 접속 : 제공 받은 Console URL 정보를 가지고 웹 브라우저를 통해 접속 합니다. 

  - 계정/비밀번호 : <span style="color: red"> userx / openshift </span>

  ![console_connect](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/01_creating_project.png)

**1-2) Web Terminal 실행 방법**

- OppenShift 콘솔에 접속하여 윗 쪽 상단의 아이콘을 통해 Web Terminal을 실행합니다. OpenShift CLI 및 명령어 사용을 위해 사용 할 Web Terminal 환경입니다.

  ![user_webterminal_icon](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/user_webterminal_icon.png)

- 아이콘을 누르면 하단에 Terminal 창이 활성화 됩니다. 

  ![user_webterminal_bottom](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/user_webterminal_bottom.png)

- 만약 새로운 창으로 Terminal을 실행하기를 원한다면 새 창으로 열기 아이콘을 선택합니다.

  ![user_webterminal_new_windows_icon](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/user_webterminal_new_windows_icon.png)

- 다음과 같이 새로운 창에서 Termianl이 열립니다.

  ![user_new_windows_webterminal](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/user_new_windows_webterminal.png)

  > 이렇게 활성화 된 Terminal에서 실습을 수행하실 때 명령어 수행을 진행하실 수 있습니다.

  

### 2. OpenShift 환경 배포
---

OpenShift에 애플리케이션을 배포하기 위해서 프로젝트를 생성합니다.

- 프로젝트 생성

- `프로젝트(네임스페이스)` : 쿠버네티스에서 용도에 따라서 오브젝트를 묶는 하나의 가상 공간 또는 그룹, 쉽게 말하면 애플리케이션의 도메인 단위

- 애플리케이션을 배포하기 위해 프로젝트를 생성합니다.

  ![01_creating_project](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/01_creating_project.png)

- `프로젝트 이름` : userx-demo 입력 (자신의 계정-demo)

  ![02_user1_demo_project](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/02_user1_demo_project.png)

- 애플리케이션 배포

  아래 화면에서 `Add page`를 선택하여 애플리케이션 배포를 계속 진행합니다.

  ![03_application_deployment_add_page](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/03_application_deployment_add_page.png)

- VM 및 컨테이너 환경 실습과 동일하게 Apache httpd 기반으로 애플리케이션을 실행하기 위해서는 Developer Catalog 화면에서 All Services를 선택합니다.

  ![04_developer_catalog](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/04_developer_catalog.png)

- 검색창에 `httpd`를 검색한 후, **Builder Images**의 **Apache HTTP Server (httpd)**를 선택합니다.

  ![05_builder_images](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/05_builder_images.png)

  

- **Create** 버튼을 눌러서 진행을 계속합니다.

  ![06_create_application](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/06_create_application.png)

- Git Repo URL은 아래 기입된 정보를 입력하여 계속 진행합니다. 다른 정보는 기본으로 두고 진행을 계속합니다.

  - Git Repo URL : https://github.com/ellisonleao/clumsy-bird/

  ![07_create_s2i_image_application](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/07_create_s2i_image_application.png)

- Topolozy에서 실행중인 Pod(Container)를 선택하면 상세 정보를 확인할 수 있습니다.

  ![08_pod_toplozy](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/08_pod_toplozy.png)

- 오른쪽 상세 정보에서 **Builds** 부분의 **View logs**를 선택합니다.

  ![09_builds_view_logs](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/09_builds_view_logs.png)

- **View logs**를 선택하면 상세로그를 확인 할 수 있습니다.

  ![10_view_logs](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/10_view_logs.png)

- **Open URL** 버튼을 선택하여 애플리케이션이 정상적으로 호출되는지 확인합니다.

  ![11_open_url](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/11_open_url.png)

- VM과 Container 환경에서 실행했던 동일한 애플리케이션이 OpenShift 환경에서도 동일하게 서비스 됨을 확인하였습니다.

  ![12_application_service](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/12_application_service.png)



### 3. Blue/Green 테스트

---

Blue / Green 배포는 두 가지 버전의 애플리케이션을 동시에 실행하고 이전 Pod를 삭제하지 않고 새로운 Pod가 생성됩니다. Pod의 새로운 버전이 모두 실행되면 이전 Pod에서 새로운 Pod로 트래픽을 전환할 수 있습니다. 롤링 전략 또는 전환 서비스를 경로(라우트)에서 사용할 수 있습니다.

명령어 작업은 웹 터미널을 실행하여 해당 터미널에서 작업을 수행합니다.

- 웹 터미널 실행

  ![user_webterminal_new_windows](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/user_webterminal_new_windows.png)

- 프로젝트 생성

  ```bash
  $ oc new-project userx-bluegreen --display-name="Blue-Green Deployments"
  ```

  > `userx`에 자신의 user로 수정하여 프로젝트를 생성합니다.

- 애플리케이션 생성

  ```bash
  $ oc new-app --docker-image=quay.io/gpte-devops-automation/ocp-probe:v0.4 --name=blue 
  ```

- Pod 상태 확인

  콘솔의 Topology 뷰 또는 CLI 명령을 통해 애플리케이션 Pod의 상태를 확인합니다.

  ```bash
  $ oc get pods
  NAME                   READY   STATUS    RESTARTS   AGE
  blue-dd7f969b4-5w48m   1/1     Running   0          5s
  ```

- 서비스 확인

  ```bash
  $ oc get svc
  NAME    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
  blue    ClusterIP   172.30.57.247   <none>        8080/TCP   55s
  ```

  > 이 서비스는 클러스터 내부의 클라이언트에만 표시됩니다. 클러스터 외부에서도 서비스를 확인할 수 있도록 `oc expose` 명령을 통해 경로(Route)를 생성합니다. --name 매개변수를 사용하여 경로(Route)의 이름을 지정합니다. 이 경로(Route)는 Blue 및 Green 배포를 모두 제공하므로 bluegreen이라고 합니다.

- 경로(Route) 생성

  ```bash
  $ oc expose svc blue --name=bluegreen
  route.route.openshift.io/bluegreen exposed
  ```

- 경로(Route) 확인

  ```bash
  $ oc get route
  NAME        HOST/PORT                                                              PATH   SERVICES   PORT       TERMINATION   WILDCARD
  bluegreen   bluegreen-user1-bluegreen.apps.cluster-tzmzd.sandbox2394.opentlc.com          blue       8080-tcp                 None
  ```

  > `curl`을 사용하여 이전 명령 출력에서 실제 애플리케이션의 경로(Route) URL을 사용하여 배포된 애플리케이션의 버전을 확인합니다. 또는 경로(Route)에 대한 환경 변수를 만드는 것이 좋습니다.

- 경로(Route) 변수 설정

  ```bash
  export ROUTE=$(oc get route bluegreen -o jsonpath='{.spec.host}')
  ```

- curl 명령어로 버전 확인

  ```bash
  $ curl $ROUTE/version
  0.4
  ```

- Blue Deployment 생성

  애플리케이션의 새로운 버전에 대한 배포(Deployment)를 생성하고 이름을 blue라고 지정합니다.

  ```bash
  oc new-app --docker-image=quay.io/gpte-devops-automation/ocp-probe:v0.5 --name=green
  ```

- 애플리케이션 상태 확인

  ```bash
  $ oc get pods
  NAME                     READY   STATUS    RESTARTS   AGE
  blue-dd7f969b4-5w48m     1/1     Running   0          49s
  green-56d6d79f86-ng46l   1/1     Running   0          10s
  ```

- 서비스 확인

  ```bash
  $ oc get svc
  NAME    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
  blue    ClusterIP   172.30.57.247   <none>        8080/TCP   55s
  green   ClusterIP   172.30.87.89    <none>        8080/TCP   16s
  ```

- Blue로 경로(Route) 전환

  이번에는 green 서비스를 가리키는 외부 경로(Route)가 이미 있으므로 서비스를 노출하기 위해 `oc expose`를 실행할 필요가 없습니다. 이번에는 경로(Route)를 blue 서비스로 전환합니다. 이를 수행하는 방법은 몇 가지가 있습니다. 먼저, 가장 쉬운 방법인 `oc edit` 명령을 사용하고 경로(Route)의 매니페스트에서 올바른 위치를 찾는 데 도움을 줍니다. 나중에 `oc patch` 명령을 사용하여 전환을 수행합니다. `oc patch` 명령을 사용하면 blue 배포와 green 배포 간 전환을 자동화하려는 경우에 유용합니다.

  `export EDITOR=/usr/bin/vim` 명령을 사용하여 YAML 구문을 강조 표시하고 쉽게 편집할 수 있습니다.

- 경로(Route) 편집

  `oc edit route bluegreen`으로 편집할 경로(Route)의 매니페스트를 열고 사양 섹션을 찾습니다.

  ```bash
  oc edit route bluegreen
  ```

  ```yaml
  spec:
    host: bluegreen-user1-bluegreen.apps.cluster-tzmzd.sandbox2394.opentlc.com
    port:
      targetPort: 8080-tcp
    to:
      kind: Service
      name: blue  // green로 변경
      weight: 100
    wildcardPolicy: None
  status:
    ingress:
    - conditions:
      - lastTransitionTime: "2023-06-08T08:37:41Z"
        status: "True"
  ```

  ![oc_edit_route_bluegreen](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/oc_edit_route_bluegreen.png)

  > name : blue 부분을 green으로 수정합니다.

- 콘솔에서 변경하는 방법

  웹 콘솔 접속 > 관리자 뷰 > Networking > Routes > Edit Route 선택
  
  ![console_edit_routes](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/console_edit_routes.png)
  
- 서비스를 green으로 변경 후 저장

  ![update_blue_route](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/update_green_route.png)
  
- curl로 버전 확인

  ```bash
  $ curl $ROUTE/version
  0.5
  ```

  출력된 메시지에서 0.5가 표시됩니다.

- 명령어를 통해 배포를 전환

  다시 명령어를 통해 경로(Route)를 편집하고 서비스를 blue로 전환합니다. 이번에는 `oc patch` 명령어를 통해 수행합니다.

  ```bash
  $ oc patch route/bluegreen -p '{"spec":{"to":{"name":"blue"}}}'
  route.route.openshift.io/bluegreen patched
  ```

- curl로 버전 확인

  ```bash
  $ curl $ROUTE/version
  0.4
  ```

  다시 blue 서비스인 0.4 버전으로 전환된 것을 확인할 수 있습니다.

  
### 4. A/B 테스트
---

A/B 배포 전략을 사용하면 프로덕션 환경에서 제한된 방식으로 새로운 버전의 애플리케이션을 시도할 수 있습니다. 프로덕션 버전에서 대부분의 사용자 요청을 가져오고 제한된 요청만 새로운 버전으로 이동하도록 지정할 수 있습니다.

각 버전에 대한 요청 분배를 사용자가 제어하므로 테스트를 진행하면서 새로운 버전에 대한 요청 비율을 늘려 결국 이전 버전의 사용을 중지할 수 있습니다. 각 버전에 대한 요청 부하를 조정할 때 필요한 성능을 제공하기 위해 각 서비스의 Pod 수도 스케일링해야 할 수 있습니다.

이 배포가 효과적이려면 이전 버전과 새로운 버전이 동시에 실행될 수 있을 정도로 충분히 유사해야 합니다. 버그 수정 릴리즈 및 새 기능이 이전 기능을 방해하지 않는 경우 일반적으로 사용됩니다. 

- A/B 테스트

  Spec: 섹션이 다음과 유사하게 보이도록 `alternateBackends`를 추가하도록 경로를 편집하여 A/B 테스트 모드에서 배포를 구성합니다.

  ```bash
  $ oc edit route bluegreen
  ```

  ```yaml
  --- 생략 ---
    to:
      kind: Service
      name: blue
      weight: 50
    alternateBackends:
    - kind: Service
      name: green
      weight: 50
  ```

  > 위와 같이 내용을 편집합니다.

  ![ab_test_edit_route](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/ab_test_edit_route.png)

- 콘솔에서 설정하는 방법

  웹 콘솔 접속 > 관리자 뷰 > Networking > Routes > Edit Route 선택 
  
  ![console_edit_routes](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/console_edit_routes.png)

-  Add alternate Service 선택

  ![add_alternate_service](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/add_alternate_service.png)

- green의 비율은 50으로 설정하고, blue를 Alternate Service target으로 다음과 같이 설정한 후 저장

  - blue Weight : 50

  - Alternative Service target : green

  - Alternative Service weight : 50

    ![add_alternate_service_02](https://github.com/justone0127/container-workshop-02.openshift-labs/blob/main/images/add_alternate_service_02.png)

- 명령어 수행

  WebTerminal에서 다음 명령을 수행합니다.
  
  ```bash
  $  while true; do curl $ROUTE/version ; echo ""; sleep 1; done
  0.5
  0.5
  0.4
  0.4
  0.5
  0.5
  0.4
  0.4
  0.5
  0.5
  
  명령어 수행 시 alternateBackends 서비스를 확인할 수 있으며, weight 비율 대로 요청이 들어가는 것을 확인할 수 있습니다.  
