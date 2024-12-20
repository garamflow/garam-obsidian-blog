# Redis에서 데이터 영속성을 위한 방법
레디스는 가끔 디스크를 사용한다. 데이터의 영속성을 위해 백업이 필요하다.
RDB와 AOF

## 1. RDB (Redis Database)
- 특정 시점마다 데이터를 스냅숏 형태로 저장한다.
- 정책 설정 시 주기적으로 디스크에 데이터를 저장한다.
- 디스크 사용량이 적다.
- 바이너리 형태로 저장한다.
	- 더 빠르게 메모리에 로딩이 가능하다.
- 일종의 잡 스케줄러나 Cron 형태이다.
- 주기가 실행되기전에 문제 발생 시 데이터 유실 가능성도 있다.
Cron의 형태로 데이터를 SnapShot하여 저장을 한다. ◦ 스케줄러의 형태이기 떄문에 일부 데이터 유실 가능 ◦ 하지만 빠르고 효과적이다.

## 2. AOF (Append Only File)
- 들어오는 요청마다 커맨드를 저장한다.
- 원본 데이터셋을 복원할 수 있다.
- 들어오는 요청 족족 변경을 일으켜서 리소스를 더 잡아먹는다.
모든 요청을 커맨드의 형태로 저장을 한다. ◦ 영속성을 절대적으로 보장하지만, 빈번한 처리라 리소스가 더 소요가된다.

## 3. AOF vs RDB
- **우선순위**: 두 가지를 병행할 수 있으며, 이 경우 AOF가 우선적으로 동작하여 데이터를 복원합니다.
- **유실 가능성**: 데이터 유실이 절대적으로 허용되지 않으면 AOF를 사용하고, 약간의 유실이 가능하거나 성능이 중요한 경우 RDB를 사용합니다.