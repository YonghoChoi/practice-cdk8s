# practice-cdk8s
cdk8s 연습을 위한 repo입니다.

[CDK for Kubernetes](https://cdk8s.io/)

- 2020년 5월에 발표된 오픈소스 프로젝트
- CDK는 프로그래밍 언어로 CloudFormation을 만들어주는 도구인데, 이를 쿠버네티스 매니페스트에도 그대로 적용
- 조직 내 베스트 프랙티스를 만들어서 재사용할 수 있는 장점이 있음

## 사용 방법

1. 설치

    ```python
    npm install -g cdk8s-cli
    brew install pipenv
    ```

    - brew로 설치하는 방법도 있는데 python의 경우에는 brew로 설치 한 경우 cdk8s import 시 black 모듈에서 오류가 발생한다.
    - npm으로 설치하면 정상적으로 import 명령이 실행된다.
2. 프로젝트 초기화

    ```python
    cdk8s init python-app
    ```

3. k8s 패키지 import

    ```python
    cdk8s import --language python
    ```

4. cdk8s가 지원하는 프로그래밍 언어로 매니페스트 정의

    ![CDK8s%20fc57d7232e47426495e35b9dd78f97e8/_2020-09-12__2.20.15.png](CDK8s%20fc57d7232e47426495e35b9dd78f97e8/_2020-09-12__2.20.15.png)

5. syn으로 manifest 파일 생성

    ```python
    cdk8s synth
    ```

## 트러블슈팅

**Cannot find module '../lib/utils/unsupported.js'**

```python
NOTE: Temp directory retained due to an error: /var/folders/49/kn0wthh540v1bv2mrjs53_ym0000gn/T/temp-hT9JTh
Error: jsii compilation failed with non-zero exit code: 1
  | Error: Process exited with status 1
  | internal/modules/cjs/loader.js:583
  |     throw err;
  |     ^
  | Error: Cannot find module '../lib/utils/unsupported.js'
  |     at Function.Module._resolveFilename (internal/modules/cjs/loader.js:581:15)
  |     at Function.Module._load (internal/modules/cjs/loader.js:507:25)
  |     at Module.require (internal/modules/cjs/loader.js:637:17)
  |     at require (internal/modules/cjs/helpers.js:22:18)
  |     at /usr/local/lib/node_modules/npm/bin/npm-cli.js:19:21
  |     at Object.<anonymous> (/usr/local/lib/node_modules/npm/bin/npm-cli.js:155:3)
  |     at Module._compile (internal/modules/cjs/loader.js:689:30)
  |     at Object.Module._extensions..js (internal/modules/cjs/loader.js:700:10)
  |     at Module.load (internal/modules/cjs/loader.js:599:32)
  |     at tryModuleLoad (internal/modules/cjs/loader.js:538:12)
  |     at ChildProcess.child.once (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-pacmak/lib/util.js:57:31)
  |     at Object.onceWrapper (events.js:277:13)
  |     at ChildProcess.emit (events.js:189:13)
  |     at maybeClose (internal/child_process.js:970:16)
  |     at Process.ChildProcess._handle.onexit (internal/child_process.js:259:5)
  +----------------------------------------------------------------------------------
  | Command: /usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-pacmak/bin/jsii-pacmak --code-only
  | Workdir: /var/folders/49/kn0wthh540v1bv2mrjs53_ym0000gn/T/temp-hT9JTh
  +----------------------------------------------------------------------------------
    at newError (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-srcmak/lib/util.js:38:20)
    at ChildProcess.child.once.code (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-srcmak/lib/util.js:55:29)
    at Object.onceWrapper (events.js:277:13)
    at ChildProcess.emit (events.js:189:13)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:248:12)
```

아래 명령을 실행한다.

```python
sudo chown -R $(whoami):admin /usr/local/lib/node_modules/
brew postinstall node
```

**No module named 'black'**

```python
NOTE: Temp directory retained due to an error: /var/folders/49/kn0wthh540v1bv2mrjs53_ym0000gn/T/temp-oQri5p
Error: jsii compilation failed with non-zero exit code: 1
  | Error: Process exited with status 1
  | Traceback (most recent call last):
  |   File "/Users/yongho/.jsii-cache/python-black/.env/bin/black", line 5, in <module>
  |     from black import patched_main
  | ModuleNotFoundError: No module named 'black'
  |     at ChildProcess.child.once (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-pacmak/lib/util.js:57:31)
  |     at Object.onceWrapper (events.js:277:13)
  |     at ChildProcess.emit (events.js:189:13)
  |     at maybeClose (internal/child_process.js:970:16)
  |     at Socket.stream.socket.on (internal/child_process.js:389:11)
  |     at Socket.emit (events.js:189:13)
  |     at Pipe._handle.close (net.js:600:12)
  +----------------------------------------------------------------------------------
  | Command: /usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-pacmak/bin/jsii-pacmak --code-only
  | Workdir: /var/folders/49/kn0wthh540v1bv2mrjs53_ym0000gn/T/temp-oQri5p
  +----------------------------------------------------------------------------------
    at newError (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-srcmak/lib/util.js:38:20)
    at ChildProcess.child.once.code (/usr/local/Cellar/cdk8s/0.27.0/libexec/lib/node_modules/cdk8s-cli/node_modules/jsii-srcmak/lib/util.js:55:29)
    at Object.onceWrapper (events.js:277:13)
    at ChildProcess.emit (events.js:189:13)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:248:12)
```

아래 명령을 실행한다.

```python
pip install --upgrade git+https://github.com/psf/black.git
```